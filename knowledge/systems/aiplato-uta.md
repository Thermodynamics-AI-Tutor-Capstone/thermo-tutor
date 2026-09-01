# aiPlato — UT Arlington + Harvard

**Type:** system
**One line:** A stepwise-feedback physics homework platform whose usage data answers a question
this whole knowledge base kept getting wrong: **students don't want hints and don't want to chat —
they want their own work checked.**
**Why we care:** It is the closest deployed analogue to our design in an adjacent quantitative
domain, its outcome measure is a **cumulative final exam** rather than in-app performance, and its
tool-usage breakdown is the clearest design signal we have found.

> **Verification: `[read]` — full text, 34 pp., 2026-09-01.**

Dange, A., Lopez, R. E., Shah, N. & **Deslauriers, L.** (2026). *"aiPlato: A Novel AI Tutoring and
Stepwise Feedback System for Physics Homework."* arXiv:2601.09965. Deployed in a large
introductory physics course at the **University of Texas at Arlington**; Deslauriers is at
**Harvard**, and is a co-author of the well-known work on students' *feeling* of learning
diverging from their actual learning — which is the same tension
[TUM measured as the comfort trap](../evidence/tum-dissociation-2025.md).

## ⭐⭐ The usage breakdown — the finding

On the first problem of Extra Credit 4, with **61 students attempting**:

| Tool | Students who used it | Total uses |
|---|---|---|
| ⭐ **"Evaluate My Work"** | **61 — all of them** | **152** |
| "Next Step" (directive) | **9** | 33 |
| "AI Tutor Chat" | *"rarely used"* | — |
| "Hint" | *"rarely used"* | — |

**Every single student used "check my work." Roughly one in seven asked for the next step. Almost
nobody used the chatbot or the hints.** And 152 uses across 61 students means **most students went
through multiple rounds of revision and self-correction.**

The authors' reading: *"These usage patterns support the idea that students engaged in productive
struggle."*

### This resolves an apparent contradiction in our own base

We had two irreconcilable-looking findings:

| Source | Finding |
|---|---|
| [PeteChat](petechat-purdue.md) | **Hint utilisation 0.0%** across 284 messages |
| [CycleTalk](cyclepad-cycletalk.md) | Help requests on **14%** of actions |
| [RAG + SRL tutor](rag-tutor-southeast.md) | **Guided support was the most-used mode** |
| **aiPlato** | **100% used "evaluate my work"; hints and chat rarely used** |

**They agree once you stop treating "help" as one thing.** Students reliably decline to be *told*
— hints, chat, next steps — and reliably accept having **their own work evaluated**. The RAG+SRL
result fits too: its "guided support" was a *distinct selectable mode attached to a specific
problem*, not a hint button buried behind a request.

> **The unit students want is not a hint. It is a verdict on what they already did.**

That is [the Answer Verifier design](../concepts/grounding-and-verification.md), it is what
[a UIC student described unprompted](../evidence/student-ai-perceptions-2025.md) — *"I always ask
for answers to questions after solving it by myself first"* — and it is what
[behavioural evaluation measures](../evaluation/behavioral-evaluation.md). **Four independent
lines converging on the same interaction primitive.**

**Design consequence: "Evaluate my work" should be the front door of our tutor, not a feature
behind a hint menu.**

## The outcome, and its honest caveat

**Effect size ≈ 0.81** on the **cumulative final exam** between high- and low-engagement groups,
**after controlling for prior academic performance.**

⭐ **Note the outcome is distal** — a cumulative final exam, not in-app scores. Given
[the proximal/distal collapse documented across six studies](../concepts/vanlehn-2011.md), a
0.81 on a real exam is a genuinely notable number.

⚠⚠ **But the authors disclaim causality in their own abstract:** *"As a quasi-experimental pilot
study, these findings do not establish causality and **may reflect self-selection effects**."*
Engagement was voluntary, on **optional extra-credit** assignments — so the students who engaged
most are plausibly the ones who would have scored highest anyway. **This is the same shape as
[the RAG+SRL tutor's dose-response](rag-tutor-southeast.md), and it must be read the same way.**

**Both papers are honest about it, and both leave the same gap: nobody has randomised.** That
remains [our clearest opening](../PAPER.md).

## Deployment facts worth knowing

- **114 students enrolled; 87 consented** to data analysis under IRB. Nobody was excluded from
  using the platform — **consent governed the data, not the access.** That is the right ethical
  shape and a usable template for our own IRB application. → [IRB](../../admin/irb.md)
- **Within-assignment attrition is real:** 61 students attempted the first problem of an
  assignment, **46 the last.** The authors note instructors can use these analytics to *"identify
  potential drop-off points and adjust problem sequencing or pacing."*
  → [engagement decay](../concepts/engagement-decay.md)
- The instructor gets **usage logs and learning analytics at assignment and problem level** —
  the [dual-user, instructor-facing view](../practice/institutional-landscape.md) that the Porto
  review names as the standing gap.

## Open questions

- [ ] What exactly does "Evaluate My Work" check against — a rubric, a worked solution, or a
      solver? For physics with numerical answers this is the whole design, and the paper's
      description is functional rather than architectural.
- [ ] Is aiPlato available to other institutions? If it takes arbitrary problem sets, **piloting
      it on thermodynamics problems is a far cheaper first experiment than building.**
- [ ] Why do students avoid chat so strongly? The authors flag this themselves as needing research
      — *"why students prefer certain modes of assistance over others."* Our
      [interview protocol](../../research/student-interviews/protocol-draft.md) could answer it.

## Connects to

- [Grounding and verification](../concepts/grounding-and-verification.md) — the Answer Verifier loop
- [PeteChat](petechat-purdue.md) — 0% hint uptake, now explicable
- [The RAG + SRL tutor](rag-tutor-southeast.md) — the other honest dose-response
- [TUM dissociation](../evidence/tum-dissociation-2025.md) — Deslauriers' feeling-vs-learning tension
- [Productive failure](../concepts/productive-failure.md) — what "evaluate my work" preserves
- [Student AI perceptions](../evidence/student-ai-perceptions-2025.md) — the same workflow, described by a student

## Sources

- [Dange, Lopez, Shah & Deslauriers (2026), "aiPlato: A Novel AI Tutoring and Stepwise Feedback System for Physics Homework," arXiv:2601.09965](https://arxiv.org/pdf/2601.09965) `[read — full text, 34 pp., 2026-09-01]`
