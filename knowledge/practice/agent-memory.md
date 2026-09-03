# Agent memory — what a student model actually is, as an engineering problem

**Type:** practice
**One line:** The memory architecture that wins at three weeks of history **loses** at nine weeks —
and a semester is fifteen.
**Why we care:** A [student model](../concepts/knowledge-tracing.md) that persists across a course
*is* long-horizon agent memory. This literature has measured what happens to it over time, and the
education literature has not.

> ⚠ Two 2026 preprints, unreviewed, both evaluating on general assistant tasks rather than
> tutoring. Take the failure modes seriously and the numbers provisionally.
> → [standing gaps](../../CLAUDE.md)

---

## ⭐⭐ Memory rankings invert with history length

*"Ground Truth First: A Longitudinal Evaluation Instrument for Agent Memory"* (arXiv:2607.21962).

Their methodological complaint first, because it is the same one this repository keeps making:

> *"Benchmarks for LLM-agent memory typically **generate conversations first and extract answer
> keys from them afterwards** — a pipeline with **documented label-error and contamination
> problems** — and they **overwhelmingly measure short interaction histories**."*

**They invert it.** A deterministic seeded sampler emits **facts before any text exists** — each
with **validity intervals, volatility classes, and source channels** — an LLM renders chat and
email from per-event fact manifests, a fidelity verifier confirms every planted fact, and questions
are instantiated mechanically from the script. Gold answers are *"script-valid by construction."*

~380 validated questions, 15 question types, with features they say are absent from the benchmarks
they surveyed: **per-fact validity intervals, sent/received trust distinctions, injection probes
inside a benign harness, and as-of-date question sets.**

**Five memory architectures against a no-memory control**, fixed answerer, versioned judge, three
stochastic replicates, **two horizons.** And:

> ⭐ **"Backend rankings **invert with history length**: the budgeted curated-map memory that leads
> at three weeks of history **loses recall of evicted content by nine weeks**."**

**A semester is fifteen weeks.** If we evaluate a student-model architecture over a few weeks of
pilot data and pick the winner, **we will pick the one that fails in the second half of the
course** — and we will not find out until the second half of the course.

This is the same shape as three other findings already here:
[EduClaw's 30-day horizon](../evaluation/simulated-learners.md) where almost nothing survives,
[the geometric reliability law](agent-architecture.md), and
[scaffolding collapse delayed rather than prevented](../concepts/guardrails.md).
**Short evaluations systematically select the wrong design.**

⭐ **Their "validity intervals" and "volatility classes" are exactly what a student model needs.**
*"This student did not understand entropy generation"* has a validity interval — it was true in
week 4 and may be false by week 9. **A student model that stores beliefs without expiry is storing
a fossil**, and this is the vocabulary for fixing that.
→ [knowledge tracing](../concepts/knowledge-tracing.md), [spaced repetition](../concepts/spaced-repetition.md)

## The write phase is where the problem is

*"Dual-Layer Agentic Memory with Fast Write Routing and Slow Consolidation"* (arXiv:2608.22215)
identifies the failure that a naive student model would walk straight into:

> *"Existing memory systems typically treat external memory as a **monotonically growing
> repository**, inevitably leading to **retrieval degradation and increasing computational costs
> over time**."*

> *"The core challenge is **not retrieval alone**, but **managing the knowledge lifecycle: deciding
> what to externalize, update, or ultimately internalize**."*

Their framework, borrowing **Complementary Learning Systems** theory from neuroscience, moves the
decision to the **write** phase:

| Stage | What happens |
|---|---|
| **Epistemic routing** | Every incoming item classified **non-write / write-new / write-update** |
| **Model cascade** | Routed small-to-large, so most decisions are made cheaply |
| **Slow consolidation** | A periodic write-back phase folds high-value external memories **into model parameters** via supervised fine-tuning |

Results: a **1.7B/8B cascade prunes up to 68% of redundant external memory** while escalating
**fewer than 50% of inputs**, and still retains **over 98% of the downstream QA Exact Match** of an
exhaustive-retention baseline.

**Two-thirds of what a naive system would store is redundant**, and a small model can decide that.

### Why the three-way write decision matters for a tutor

*Non-write / write-new / write-update* is not a technical detail — it is a pedagogical judgement:

- **write-new** — the student demonstrated a new knowledge component
- ⭐ **write-update** — the student now understands something they previously did not. **This is the
  entire point of a student model** and it is the case naive append-only memory handles worst: the
  old belief stays and competes with the new one.
- **non-write** — most turns. A student asking to restate a question changes nothing about what
  they know.

**A tutor whose memory cannot distinguish "learned something new" from "corrected an earlier
misconception" cannot do the one thing a student model is for.**

⚠ **The parametric consolidation half does not transfer to us.** Fine-tuning a model on an
individual student's history is a privacy and cost problem we should not take on. **Take the write
routing; leave the SFT.** → [assessment integrity](assessment-integrity.md)

## What follows for us

1. **Design the student model with expiry from the start.** Validity intervals and volatility
   classes, not a growing log of observations.
2. **Classify every write.** Three-way routing is cheap and it is what makes "update" possible.
3. ⚠ **Do not pick a memory architecture on a short pilot.** Rankings invert. If we can only
   evaluate over weeks, say so and treat the choice as provisional.
4. **Expect most turns to be non-write.** Storing everything degrades retrieval, and
   [Jill Watson's 57% retrieval-failure rate](../systems/jill-watson.md) is what degraded retrieval
   looks like in a deployed tutor.
5. **This is a reason to log the raw ledger separately from the student model.** The
   [append-only event ledger](agent-observability.md) keeps everything; the student model keeps
   only what is currently believed true. Different stores, different retention.

## Open questions

- [ ] Does knowledge tracing already solve this better? **BKT and DKT are decades of work on
      exactly "what does this student currently know," with expiry built into the model.** The
      agent-memory literature seems unaware of it. **Which of the two is the right substrate for a
      tutor is a real question and we should not assume the newer one wins.**
      → [knowledge tracing](../concepts/knowledge-tracing.md)
- [ ] What is the volatility class of a thermodynamics misconception? Some persist all semester;
      some resolve in one session. Unknown, and measurable.
- [ ] Neither paper evaluates on tutoring. **Assume nothing transfers until checked.**

## Connects to

- [Knowledge tracing](../concepts/knowledge-tracing.md) — the education literature's answer to the same problem
- [Agent architecture](agent-architecture.md) — long-horizon, long-context and long-term memory are three different axes
- [Agent observability](agent-observability.md) — the ledger versus the model
- [ALEKS](../systems/aleks.md) — knowledge states with formal structure
- [Simulated learners](../evaluation/simulated-learners.md) — how to test memory over 30 days without students

## Sources

Both held in `course-materials/papers/`.

- ["Ground Truth First: A Longitudinal Evaluation Instrument for Agent Memory," arXiv:2607.21962](https://arxiv.org/pdf/2607.21962) `[read]` — rankings invert with history length
- ["Dual-Layer Agentic Memory with Fast Write Routing and Slow Consolidation," arXiv:2608.22215](https://arxiv.org/pdf/2608.22215) `[read]` — the three-way write decision
