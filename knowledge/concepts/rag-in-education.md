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

## ⭐ A concrete ingestion toolchain for engineering course material

Most RAG-in-education papers say "we chunked the PDFs." **ARIA** (Luo, Roy Sarkar & Goswami —
Dalian University of Technology + **Johns Hopkins**, arXiv:2604.06179, read in full 2026-09-01)
names the actual components, and they are the three problems engineering material creates:

| Problem | Their tool |
|---|---|
| Structured document layout | **Docling** |
| ⭐ **Mathematical formula recognition** | **Nougat** |
| ⭐ **Engineering diagram interpretation** | **GPT-4 Vision API** |
| Embedding | **e5-large-v2** (open-source), chosen for *"high semantic performance and low query latency"* |

**This is the stack we would otherwise have to discover ourselves.** A thermodynamics course is
lecture slides full of equations, T–s diagrams and property tables — precisely the content that
naive PDF chunking destroys. Nougat for the equations and a vision model for the figures is a
starting architecture, not a research question.
→ [diagram reading](../domain/diagram-reading.md),
[property data tools](../domain/property-data-tools.md)

**Evaluated on** *Statics and Mechanics of Materials*, a **sophomore civil engineering course at
Johns Hopkins** — the same course position in the curriculum as our thermodynamics course.
Benchmarked against ChatGPT-5.

**Reported results:** **97.5% accuracy at domain-specific question filtering** (deciding whether a
question is even in scope — a real and underrated function), and it *"correctly answered all 20
relevant course questions,"* with better conceptual explanation quality and more structured
problem-solving than the baseline.

⚠ **n = 20 again.** This is the third engineering-education paper in this base
([GPThermo](../systems/gpthermo-wpi.md), ARIA, and the Calgary MCQ work) whose headline rests on
about twenty items. **Twenty-question evaluations are the norm in this venue and they are not
benchmarks.** Take the pipeline, not the number.

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

- [Luo, Roy Sarkar & Goswami, "ARIA: Adaptive Retrieval Intelligence Assistant — A Multimodal RAG Framework for Domain-Specific Engineering Education," arXiv:2604.06179](https://arxiv.org/pdf/2604.06179) `[read — full text, 20 pp., 2026-09-01]` — Dalian UT + Johns Hopkins; the Docling / Nougat / GPT-4V ingestion stack

- [Georgia Tech Jill Watson evaluation (2025)](https://news.research.gatech.edu/2025/09/02/georgia-techs-jill-watson-outperforms-chatgpt-real-classrooms) `[skimmed]` — retrieval failure rates
- [Ethel: A Virtual Teaching Assistant (ETH Zurich), arXiv:2407.19452](https://arxiv.org/pdf/2407.19452) `[read]` — now has its own node: [Ethel](../systems/ethel-eth.md) — RAG over course PDFs, LangChain
- [ARIA: Adaptive Retrieval Intelligence Assistant — multimodal RAG for engineering education, arXiv:2604.06179](https://arxiv.org/html/2604.06179) `[read]`
- [A Large-Scale Real-World Evaluation of LLM-Based Virtual Teaching Assistant, arXiv:2506.17363](https://arxiv.org/pdf/2506.17363) `[read]` — full treatment in [KAIST](../evidence/kaist-vta-2025.md)
- [Machine Assistant with Reliable Knowledge: Enhancing Student Learning via RAG-based Retrieval, arXiv:2506.23026](https://arxiv.org/pdf/2506.23026) `[found]`
