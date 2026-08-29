# RAG in Education

**Type:** concept
**One line:** Retrieval-augmented generation over course materials — the near-universal
first layer of every LLM course tutor, and the one most often mistaken for the whole system.
**Why we care:** It's table stakes, it's the layer everyone builds first, and the published
failure rates should temper expectations considerably.

## Why everyone builds this first

It's the cheapest way to make a general model course-specific. Index the syllabus, slides,
textbook, and problem sets; retrieve relevant chunks; put them in context. No fine-tuning,
no training data, a weekend of work.

Deployments using it: [Jill Watson](../systems/jill-watson.md),
[Stan](../systems/stan-udel.md), [Cogniti](../systems/cogniti-sydney.md),
[U-M Maizey](../systems/umich-maizey.md), Ethel (ETH Zurich), ARIA, and essentially every
engineering AI-TA pilot published in 2025–26.

## The failure rates nobody quotes

[Jill Watson](../systems/jill-watson.md) — one of the most carefully engineered systems in
the field — has a **43.2% retrieval failure rate.** (OpenAI's Assistant on the same task:
68.3%.)

Read that again. The best-documented educational RAG system in the literature fails to
retrieve appropriate content **more than four times in ten**, and still ends up at 78.7%
correct — because the [verification layer](grounding-and-verification.md) catches much of
what retrieval misses.

**RAG is a necessary layer that fails a lot.** Systems that treat it as the whole
architecture are relying on the model's weights far more than their diagrams admit.

## Why educational retrieval is harder than it looks

- **Student queries are bad queries.** "im confused about problem 3" retrieves nothing
  useful. Query understanding matters more than embedding quality.
- **The answer is often not in the corpus.** A student's specific confusion usually isn't a
  passage in the textbook.
- **Chunking destroys worked examples.** A solved problem split across chunks is worse than
  useless — the retrieval returns half a derivation.
- **Tables and diagrams don't embed.** Steam tables are the canonical case: the single most
  retrieval-relevant artifact in a thermodynamics course is a *numerical table*, which
  chunked text retrieval handles terribly. This is a strong argument for
  [tool calls over retrieval](../domain/property-data-tools.md) for property data.
- **Notation is course-specific and invisible to embeddings.** Whether the instructor writes
  *w* or *W*, uses *u* or *e*, matters to a student and not to a retriever.

## What good practice looks like

From the deployments and the RAG literature generally:

- **Hybrid search** (dense + keyword). Engineering notation and variable names are exactly
  what dense retrieval loses.
- **Reranking** after retrieval.
- **Structured content over chunked PDFs.** Course material authored as retrievable units
  beats chunking a textbook — this is a content-authoring cost, and it's where
  [OATutor's spreadsheet pipeline](../systems/oatutor-berkeley.md) is instructive.
- **Route around retrieval where a tool is better.** Property lookup should be a function
  call, not a search. → [property data tools](../domain/property-data-tools.md)
- **Always verify.** → [grounding and verification](grounding-and-verification.md)

## Open questions

- [ ] What's in Jill Watson's 43.2%? Nobody has published a breakdown.
- [ ] Does hybrid + rerank measurably help on *educational* corpora specifically?
- [ ] How should worked examples be represented so retrieval doesn't break them?
- [ ] Is retrieval even the right frame for a course tutor, versus a structured
      course model plus tools? (Genuine question — the retrieval failure rates suggest it
      may not be.)

## Connects to

- [grounding and verification](grounding-and-verification.md) — what catches RAG's misses
- [Jill Watson](../systems/jill-watson.md) — the published failure rates
- [property data tools](../domain/property-data-tools.md) — where tools beat retrieval
- [Stan](../systems/stan-udel.md) — RAG over Sandler, our domain

## Sources

- [Georgia Tech Jill Watson evaluation (2025)](https://news.research.gatech.edu/2025/09/02/georgia-techs-jill-watson-outperforms-chatgpt-real-classrooms) `[skimmed]` — retrieval failure rates
- [Ethel: A Virtual Teaching Assistant (ETH Zurich), arXiv:2407.19452](https://arxiv.org/pdf/2407.19452) `[found]` — RAG over course PDFs, LangChain
- [ARIA: Adaptive Retrieval Intelligence Assistant — multimodal RAG for engineering education, arXiv:2604.06179](https://arxiv.org/html/2604.06179) `[found]`
- [A Large-Scale Real-World Evaluation of LLM-Based Virtual Teaching Assistant, arXiv:2506.17363](https://arxiv.org/pdf/2506.17363) `[skimmed]`
- [Machine Assistant with Reliable Knowledge: Enhancing Student Learning via RAG-based Retrieval, arXiv:2506.23026](https://arxiv.org/pdf/2506.23026) `[found]`
