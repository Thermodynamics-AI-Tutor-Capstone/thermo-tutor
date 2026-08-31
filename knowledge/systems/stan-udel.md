# Stan — University of Delaware

**Type:** system
**One line:** A locally-hosted LLM tool suite for a chemical engineering thermodynamics
course, whose main contribution is **instructor-facing lecture analytics** — not student
tutoring.
**Why we care:** We assumed this was our closest competitor. Having read it in full: **it
is not.** Stan deliberately stops at "point to the right textbook page," and explicitly
places tutoring, guided problem solving, and Socratic dialogue out of scope. That leaves
our project's territory largely open, and hands us a superb engineering failure-mode
taxonomy for free.

> **Verification: `[read]` — full text, 2026-08-31.** This node previously contained
> several errors drawn from an automated summary: it claimed Stan used "Socratic prompting
> with explicit refusal to solve problems." **That is wrong.** Corrections below.

## The paper

Eric M. Furst and Vasudevan Venkateshwaran, Department of Chemical and Biomolecular
Engineering, University of Delaware. arXiv:2603.04657, dated 6 March 2026.
Course: **CHEG231 (Chemical Engineering Thermodynamics I)**, Fall 2025.
Textbook: **Sandler, *Chemical, Biochemical, and Engineering Thermodynamics*** (2017).
Code: [github.com/entropiclearners/stan](https://github.com/entropiclearners/stan)

## What Stan actually is

The paper's own capability scale — a six-level taxonomy of "Learning Assistant
Intelligence" — is the most useful single artifact in it, and it is where the correction
lives:

| Level | Title | Role |
|---|---|---|
| **1** | **Resource Pointer** | Points to textbook sections; smart search, no explanations |
| **2** | **Content Summarizer** | Summarizes textbooks, lectures, documents |
| 3 | Concept Explainer | Explains in plain language; answers why/how |
| 4 | Guided Problem Solver | Step-by-step; hints and guiding questions; identifies mistakes |
| 5 | Exercise Generator | Custom practice problems |
| 6 | Autonomous Learning Companion | Socratic dialogue; metacognition; cross-subject integration |

> *"At this point in time, our goal for Stan is to build a system operating at the level of
> a Resource Pointer (Level 1) and Content Summarizer (Level 2)."*

**Stan is Levels 1–2. Our brief describes Levels 4–6.** Socratic dialogue appears in their
taxonomy only as Level 6 — the thing they have not built.

The paper's actual thesis is different from tutoring altogether: student-facing AI is
over-discussed, and **instructor-facing tools built on the same infrastructure are the
neglected opportunity.**

## Architecture

**Two hardware tiers**, both local, no cloud APIs:
- **GPU workstation** — Linux, single NVIDIA RTX 4090 (24 GB). Batch: Whisper
  transcription, structured extraction.
- **Consumer laptop** — interactive query pipeline via Ollama. 7–13B models.

**Transcription:** faster-whisper (CTranslate2) running Whisper **large-v3** in float16,
Silero VAD. **39 lectures, 35.7 hours, transcribed in 43.7 minutes** — 49× realtime,
~4.3 GB VRAM. 35 lectures produced full transcripts; 2 were exams; 2 yielded nothing.

**Inference:** **Llama 3.1 8B** via Ollama, 16,384-token context, temperature 0.6.

**Retrieval — and this is a deliberate, interesting choice: not vector RAG.** They use the
textbook's own **back-of-book index** (~1,500 entries as hierarchical JSON) plus a
table-of-contents navigation tree. Their reasoning:

> *"the textbook's back-of-book index is itself a high-quality retrieval artifact... Embedding-based
> retrieval over raw textbook text would require chunking decisions, an embedding model, a
> vector store, and careful tuning of similarity thresholds—added complexity without clear
> benefit when a professionally curated index is available."*

Query matching runs **two extractors in parallel** — a deterministic regex extractor and an
LLM extractor (which does query expansion: "entropy" → entropy change, entropy generation,
entropy balance) — merged by **max-score**, deliberately asymmetric so a match found by
only one path isn't penalized. An earlier weighted average (0.7 LLM + 0.3 regex) was
abandoned because it suppressed valid single-path matches.

Grounding is threefold: **architectural** (the model sees only 5 retrieved entries, never
the full text), **prompt-level** (use only provided context, never fabricate chapter or
section numbers), and **temperature** (0.6).

Contrast with [CS50](cs50-duck.md), which does vector RAG over 30-second lecture caption
segments in ChromaDB. Two credible, opposite retrieval philosophies in the same year.
→ [RAG in education](../concepts/rag-in-education.md)

## The instructor-facing half (the paper's real contribution)

Four analyses run over each lecture transcript, all 35 lectures in ~15 minutes:
**summaries**, **question identification** (speaker, type, pedagogical significance),
**confusion detection** (topic, evidence, severity), and **anecdotes/analogies** catalog.

Use cases they name: content reinforcement (material said aloud but never written down),
lecture analytics ("when did I first discuss fugacity?"), course evolution across
semesters, and **question mining** — a passive, continuous feedback channel capturing
student confusion in real time rather than via end-of-semester evaluations.

**Worth noticing for our own project:** their confusion detector flagged, on the entropy
lecture, *"Entropy and its relation to disorder or randomness — students seem unfamiliar
with the concept."* The authors call this out as an important reminder to address students'
preconceptions. That is **verbatim the misconception in
[our catalogue](../../research/domain/skill-graph-draft.md)**, surfaced automatically from
a lecture recording.

## The engineering failure taxonomy — the most reusable part

Running structured extraction on an 8B local model over 35 lecture transcripts produced a
practical taxonomy any team doing this will hit:

| Failure | What happened | Fix |
|---|---|---|
| **Context truncation** | Ollama's default context is 2,048 tokens; transcripts are ~13,000. The model silently received the **first ~15%**. Output was valid JSON with plausible content that bore no relation to the lecture — including fabricated exam problems and fictional Q&A with example.com URLs. **The only external signal was anomalously fast inference (~2s vs ~60s).** | `num_ctx = 16384` |
| **Placeholder echoing** | Schema example `"timestamp": "H:MM:SS"` was copied literally — all 35 lectures | Concrete example + "Do NOT use placeholder text" |
| **Over-classification** | Filler ("right?", "okay?") classified as substantive questions; routine examples tagged as anecdotes | Accepted — biases recall over precision, better for downstream filtering |
| **Schema drift** | Different field names, unexpected fields, bare strings where objects expected. JSON mode guarantees *syntax*, not *schema* | Defensive parsing |
| **Bimodal output** | **26 of 35 lectures produced exactly 8 questions** with fabricated timestamps; 5 produced 64–108. The model defaulted to a fixed output length rather than analyzing | **Two-pass**: extract (high-recall, full transcript) then filter (candidates only, ~1–2k tokens). Distribution became smooth: range 2–15, mean 8.8 |
| **Repetitive output** | 28 consecutive identical confusion entries for one topic | Deduplication (not yet implemented) |

**The silent-truncation failure is the one to internalize.** A plausible, well-formed,
entirely fabricated output with no error signal is the worst failure mode a tutoring system
can have, and the only tell was latency.

Separately, **Whisper hallucination loops**: a baseline lecture had 53 of 826 segments
(6.4%) as hallucinated repetitions — *"Elizabeth."* repeated 37 times across 50.5 seconds.
A three-layer mitigation (repetition penalty 1.1, 3-gram blocking, `condition_on_previous_text=False`,
post-hoc dedup) cut this to **0.02%** across the full corpus.

**Domain vocabulary prompting** mattered enormously: out of the box Whisper rendered
*fugacity* as **"GASB"**, the *Antoine equation* as **"Anaconda equation"**, and
*Peng-Robinson* as **"time-Robinson"**. Whisper's `initial_prompt` with thermodynamic terms
fixed most of it. Both Kaltura and Whisper still failed on *Helmholtz* ("compulse").

## What Stan does not have — the gaps that define our space

Confirmed by full reading:

- **No property-data tools.** Porting Peng-Robinson/UNIFAC from MATLAB, VLE flash solvers,
  and root-finding are listed under *future work*. → [property data tools](../domain/property-data-tools.md)
- **No student model, no mastery tracking, no personalization.**
- **No LMS integration.**
- **No Socratic dialogue, no hint ladder, no guided problem solving** (Levels 4–6, explicitly).
- **No evaluation of any kind.** No usage data, no learning outcomes, no student survey.
  Their own words: *"systematic evaluation remains essential. Future work will include
  defining measurable learning outcomes..."*

That last point deserves emphasis: **this paper reports zero outcome data.** It is a
system-description paper. Our earlier note asking "what usage numbers?" has an answer:
none.

## Practical warnings they hand us

- **Copyright.** Using the textbook's back-of-book index is flagged by the authors
  themselves as likely fair use for development but questionable to deploy to students.
  Their recommendation: get publisher permission, or **replace it with an
  instructor-generated topic list from the syllabus and lecture notes** — which is also
  better tailored to the course. Directly relevant to our
  [skill graph](../../research/domain/skill-graph-draft.md), which is exactly such a list.
- **LMS vendor lock-in.** The university's Kaltura lecture capture has **no bulk download
  API**; recordings must be pulled one at a time, manually, even for administrators. This
  blocked their per-lecture workflow entirely. Their workaround: a **USB lapel/headset
  microphone** worn by the instructor — better audio, no vendor, immediate processing.
  → [LMS integration](../practice/lms-integration.md)
- **Local models have an equity cost.** The authors are candid: *"Hardware heterogeneity
  across student devices limits model size and performance... Performance variability may
  introduce pedagogical inequities even if financial barriers are avoided."* And local
  deployment shifts cost from subscriptions to **instructional support time** — installation,
  dependencies, cross-platform troubleshooting. → [equity](../practice/equity.md)

## The model-capability question

Stan runs **Llama 3.1 8B**. In the same research area,
[Loubet et al.](../domain/thermo-problem-benchmark.md) measured **Llama 3.1 70B** at
**40.7%** on advanced thermodynamics problems.

This is *not* a criticism of Stan as built — an 8B model pointing at textbook pages is a
sensible fit for Levels 1–2, and the grounding architecture keeps it in scope. But it does
mean the architecture **cannot be scaled up the capability ladder** without changing the
model, and the local-only commitment is what constrains it. Anyone tempted by "just run it
locally" should price that trade-off honestly.
→ [LLM capability in thermodynamics](../domain/llm-thermodynamics-capability.md)

## Revised competitive position

**Stan is not competing with our brief.** It is a lecture-transcript infrastructure paper
with a Level-1 student query tool attached. What it does that we don't plan to: instructor
analytics, lecture transcription, question mining. What we plan that it explicitly doesn't:
tutoring dialogue, hint ladders, mastery tracking, property tools, LMS context, evaluation.

The overlap is the domain and the grounding idea. **Their instructor-facing analytics is
genuinely good and we should consider whether a version of it belongs in our project** —
question mining in particular is a cheap, high-value feedback channel and a strong offer to
an instructor sponsor. → [faculty adoption](../practice/faculty-adoption.md)

## Remaining open questions

- [ ] Did students actually use it? (Unreported — possibly unmeasured.)
- [ ] Would the authors share usage data or collaborate? Same subject, adjacent year.
      `furst@udel.edu`
- [ ] Is the GitHub repo maintained, and is the index-extraction pipeline reusable?
- [ ] Does the index-over-embeddings choice actually outperform vector RAG? They assert it;
      nobody measured it. **This is a testable comparison and a real small contribution.**

## Connects to

- [LLM capability in thermodynamics](../domain/llm-thermodynamics-capability.md)
- [property data tools](../domain/property-data-tools.md) — the gap Stan leaves open
- [RAG in education](../concepts/rag-in-education.md) — index vs. embeddings
- [CS50 Duck](cs50-duck.md) — the opposite retrieval philosophy
- [Loubet et al.](../domain/thermo-problem-benchmark.md) — what Llama-class models score
- [equity](../practice/equity.md) — local-model hardware heterogeneity

## Sources

- [Furst & Venkateshwaran, "Stan: An LLM-based thermodynamics course assistant," arXiv:2603.04657](https://arxiv.org/abs/2603.04657) `[read]` — full text
- [github.com/entropiclearners/stan](https://github.com/entropiclearners/stan) `[found]` — **clone and evaluate**
