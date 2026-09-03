# Evaluating a tutor without students

**Type:** evaluation
**One line:** Two independent 2026 systems tune and benchmark tutors using **scripted personas** and
**knowledge-tracing-grounded simulated learners** — no human subjects, no IRB.
**Why we care:** [IRB is a standing blocker on this project](../../admin/irb.md). An evaluation
loop that needs no students lets us build, tune and measure the entire guardrail and pedagogy layer
*before* approval exists. That is worth more to our schedule than most findings here.

> ⚠ Both sources are 2026 preprints, unreviewed. And a simulated learner is a model of a student,
> not a student — see the limits at the bottom.

---

## Approach 1 — scripted personas through the live pipeline

From [the answer-withholding supervisor architecture](../concepts/guardrails.md)
(arXiv:2608.12292):

> *"We tune the behavior with an automated evaluation that **uses no human subjects**: **scripted
> student personas are driven through the live pipeline and re-scored by a stronger model**, and we
> record **each rejection's stated reason so failures are fixed by cause**."*

Three properties worth copying exactly:

1. **Through the *live* pipeline** — not against a prompt in isolation. The thing under test is the
   deployed system, guardrails and all.
2. **Re-scored by a stronger model.** A cheap tutor, an expensive judge.
3. ⭐ **Every rejection carries a stated reason**, so failures are grouped by cause rather than
   counted. This is what surfaced their **"over-help ladder"** — *"from blatant solution leaks, to
   naming the exact bug, to over-citing general facts, **with each fix exposing the next**."*

**Adversarial personas are the obvious extension**, and we have the attack model already:
[22% of PeteChat's homework messages were boundary probes](../systems/petechat-purdue.md), and
[course-framed hostile prompts dropped a stock assistant's refusal rate from 68% to 5%](../systems/jill-watson.md).
A "frustrated student the night before a deadline" persona is not a hypothetical.

## Approach 2 — a simulated learner grounded in knowledge tracing

**EduClaw-Bench** (arXiv:2608.03206) goes considerably further:

> *"Tutoring is long-horizon, since **a learner improves over days and weeks rather than in a
> single turn**, and no benchmark evaluates an agent tutor across a sustained relationship."*

| | |
|---|---|
| Setting | A **continuous 30-day relationship** with a simulated learner |
| The learner | Grounded in **knowledge tracing** — *"knowledge-concept mastery, from a KT model trained on real-student data, drives its answers"* and is probed for learning gain |
| Scale | **55 scenarios**, 10 agent adapters, three base-model tiers |
| Scored on | **learning gain, responsiveness, helpfulness**, plus two curriculum-design axes (**Gagné** and **Rosenshine**) |
| Judging | Helpfulness and curriculum axes by a **cross-family panel of three LLM judges** |

⭐ **The simulated learner's mastery is driven by a KT model trained on real students**, so its
answers change as it learns. That is the mechanism that makes a 30-day simulation mean anything —
and it connects directly to [knowledge tracing](../concepts/knowledge-tracing.md) and
[the KST outer fringe](../systems/aleks.md), which is what would drive such a learner in
thermodynamics.

**They validated the simulation**, which is the part that makes it credible: *"A calibration check
(ECE = 0.049) and a **live-classroom field study** confirm that the simulated learner and its
measurements track reality."*

### Their two findings

**1. ⭐ Tutoring quality is a property of model *and* harness together:**

> *"Tutoring quality belongs to the **base model and the agent harness together rather than either
> alone**."*

**That is the third independent arrival at the same conclusion**, from three unrelated literatures:

| Source | Evidence |
|---|---|
| [Coding agents](../practice/agent-architecture.md) | Same model, changed context handling: fail-to-pass **28% → 49%** |
| [Google's learning arena](../systems/learnlm.md) | **ChatGPT-4o 2nd, GPT-4o 5th** — same model, different product wrapper |
| **EduClaw-Bench** | Tutoring quality attributable to neither alone |

**Stop asking which model. Start asking what we build around it.**

**2. ⚠ Almost nothing survives the full horizon:**

> *"**Almost no combination sustains good tutoring over the full horizon**."*

Ten adapters, three model tiers, thirty days — and essentially nothing holds up. Read alongside
[the geometric law](../practice/agent-architecture.md) and
[scaffolding collapse at 32%](../concepts/guardrails.md), the picture is consistent: **short
demonstrations look fine and sustained relationships do not.** Our own evaluation must run long
enough to see this, or it will measure the wrong thing.

## ⚠ A related warning: scale does not buy Socratic behaviour

*"Beyond Direct Answering: Aligning Educational LLMs as Socratic Guides"* (arXiv:2607.22996)
trains Qwen2.5-7B toward Socratic tutoring with supervised warm-up plus GRPO, on 797 multi-turn
dialogues, measuring **Scaffolding Effectiveness (SE)** and **Conversation Depth**.

> ⚠ **"An unaligned Qwen-72B baseline reaches 0% SE and 96.7% leakage, showing that scale alone
> does not induce Socratic behavior."**

**A model ten times larger, unaligned, leaked the target concept in 96.7% of dialogues and scored
zero on scaffolding.** Their aligned 7B reached **SE 63.3%** with leakage down to **13.3%**.

And a counter-intuitive result worth flagging:

> *"Notably, this best variant **omits the directness penalty** during optimization, suggesting
> that **explicit anti-leakage terms can conflict with gradient-based behavioral alignment**."*

**Penalising directness directly made things worse.** Which is another argument for enforcing
withholding *outside* the model — [in a policy core](../concepts/guardrails.md) — rather than
trying to train or prompt it in.

## ⚠ What a simulated learner cannot tell us

- **It is a model of a student.** EduClaw calibrated theirs (ECE = 0.049) against a live classroom;
  **any simulated learner we build must be validated the same way or its numbers mean nothing.**
- It cannot surface what we most need from real students — **why they avoid chat and hints**, which
  [aiPlato flagged as an open question](../systems/aiplato-uta.md) and which our
  [interview protocol](../../research/student-interviews/protocol-draft.md) exists to answer.
- Both papers lean on **LLM judges**, and
  [four studies say LLM judges fail on educational quality](llm-as-judge.md). EduClaw's three-judge
  cross-family panel is a mitigation, not a solution.
- **Simulated engagement is not engagement.** A scripted persona never gets bored, never stops
  coming back in week ten, and [that is the field's actual failure mode](../concepts/engagement-decay.md).

**Use these to tune the system. Use real students to find out whether anyone wants it.**

## Connects to

- [Guardrails](../concepts/guardrails.md) — the supervisor architecture these tune
- [LLM-as-judge](llm-as-judge.md) — the weak point in both approaches
- [Knowledge tracing](../concepts/knowledge-tracing.md) — what drives the simulated learner
- [Agent architecture](../practice/agent-architecture.md) — the harness finding, third arrival
- [Behavioral evaluation](behavioral-evaluation.md) — what to measure on real students
- [IRB](../../admin/irb.md) — why this matters to our schedule

## Sources

All held in `course-materials/papers/`.

- ["Teaching a Large Language Model Tutor to Withhold the Answer: A Supervisor Architecture," arXiv:2608.12292](https://arxiv.org/pdf/2608.12292) `[read]`
- ["EduClaw-Bench: A Long-Horizon Benchmark for Pedagogical LLM Agents with Simulated Learners," arXiv:2608.03206](https://arxiv.org/pdf/2608.03206) `[read]`
- ["Beyond Direct Answering: Aligning Educational LLMs as Socratic Guides via Heuristic Rewards," arXiv:2607.22996](https://arxiv.org/pdf/2607.22996) `[read]`
