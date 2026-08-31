# TutorGym

**Type:** benchmark
**One line:** A testbed that drops AI agents into real intelligent tutoring systems and asks
them to act as tutor *or* as student — and finds that **no LLM beats chance at recognizing
an incorrect student step.**
**Why we care:** That single result is the sharpest statement in this knowledge base of what
LLMs cannot yet do pedagogically. Recognizing a wrong step is the atomic act of tutoring.

> **Verification: `[read]` — full text, 2026-08-31.**

## What it is

Daniel Weitekamp, Momin N. Siddiqui, Christopher J. MacLellan — **Georgia Institute of
Technology**. arXiv:2505.01563.
Site: [tutorgym.ai](https://tutorgym.ai) · Code: [Teachable-AI-Lab/tutor_gym](https://github.com/Teachable-AI-Lab/tutor_gym)

A standard interface for testing AI agents **inside existing, classroom-validated
intelligent tutoring systems** — [Cognitive Tutors (CTAT)](../systems/cognitive-tutor.md),
Apprentice Tutors, and [OATutor](../systems/oatutor-berkeley.md). **223 tutor domains.**

The design idea is what makes it more than a problem-solution benchmark: at **each step** of
problem solving, the agent is asked what it would do — **as a tutor** (generate a worked
example, a hint, or step-level correctness feedback) or **as a learner** (attempt the step,
then learn from the tutor's response). Tutor behavior is scored against the adaptive
step-by-step support the real ITS provides. Learner behavior is compared against **real
student data**.

## The headline result: LLMs cannot spot a wrong step

Models evaluated: `claude-3-5-sonnet-20241022`, `claude-3-5-haiku-20241022`,
`gpt-4o-2024-08-06`, `deepseek-v2.5:236b`.

GPT-4o, labeling student actions as correct/incorrect and generating next-step
demonstrations:

| Tutor suite | Correct-action accuracy | **Incorrect-action accuracy** | Demo accuracy |
|---|---|---|---|
| CTAT (10 domains) | 28.11% | 42.63% | 38.89% |
| Apprentice (30 domains) | 74.61% | 49.80% | 70.75% |
| OATutor (183 domains) | 71.20% | 38.69% | 51.07% |

The authors' finding, stated plainly:

> *"The models with the highest accuracy at identifying correct actions were the worst at
> identifying incorrect actions, and **no model exceeded chance (i.e. 50%) at identifying
> incorrect actions**."*

Next-step demonstrations ("bottom-out hints") were correct only **~52–70%** of the time.

## Why this is the most important pedagogical limitation we've found

There is a **yes-bias trade-off**: models that are good at confirming correct work are bad at
catching wrong work, and vice versa. Nothing tested does both.

Tutoring is not mostly explanation. It is mostly **diagnosis** — noticing that step 3 is
wrong, working out *why*, and responding to that specific error. If a model cannot reliably
tell a wrong step from a right one, everything downstream is unreliable:

- It will validate incorrect student work
- Its hints will target the wrong misconception
- Any "check my work" feature is untrustworthy
- Automated feedback on a student's derivation cannot be shipped without verification

**This is the pedagogical twin of the
[unstated-assumption failure](../domain/thermo-problem-benchmark.md) in our domain**, and it
points at the same architectural answer: the *correctness* judgment must come from something
other than the model's opinion — a solver, a checker, a comparison against a known solution.
→ [grounding and verification](../concepts/grounding-and-verification.md)

Note that this is exactly the gap **Bastani's guardrails filled by brute force**: their GPT
Tutor prompt included the correct solution *and* the common mistakes with matched hints,
precisely so the model wouldn't have to judge correctness itself.
→ [Bastani 2025](../evidence/bastani-2025-harm.md)

## The other result: LLMs make convincing simulated students

Running Haiku-3.5 and GPT-4o as *learners* — in-context learning from ~20–30 prior state /
action / correctness examples, prompts capped at 50k characters — produced **"remarkably
human-like learning curves."**

That is a direct enabler for two things we care about:

1. **Testing a tutor without students.** A simulated learner lets us exercise hint ladders
   and policies before any IRB-gated human contact. Enormous for a capstone timeline.
2. **[Learning by teaching](../systems/bettys-brain.md).** A teachable agent needs an agent
   that can plausibly hold, and act on, a *wrong* model. This says LLMs can.

## What we could actually do with it

- Run our tutor design against TutorGym's 223 domains to get comparative numbers with zero
  student data and no IRB gate
- Reuse the **correct/incorrect-action labeling task** as a template for a thermodynamics
  version — this is arguably a cleaner, more tractable pedagogy benchmark than the
  open-ended [MathTutorBench](mathtutorbench.md) approach, because it has ground truth
- Use simulated learners to pilot a hint ladder before Phase 3

## Open questions

- [ ] Is the harness usable outside its three ITS suites — could we add a thermodynamics domain?
- [ ] Do reasoning models (o3, extended thinking) beat chance on incorrect-action labeling?
      **The paper predates them. This is a cheap, high-value replication.**
- [ ] How close are the simulated learning curves, quantitatively?
- [ ] Chase reference 29: **Pardos & Bhandari, "ChatGPT-generated help produces learning
      gains"** — a positive result from the [OATutor](../systems/oatutor-berkeley.md) group
      that we have not yet read.

## Connects to

- [grounding and verification](../concepts/grounding-and-verification.md) — why diagnosis must be external
- [Bastani 2025](../evidence/bastani-2025-harm.md) — guardrails as a workaround for this gap
- [MathTutorBench](mathtutorbench.md) — the other pedagogy-measurement approach
- [Betty's Brain](../systems/bettys-brain.md) — simulated students enable teachable agents
- [OATutor](../systems/oatutor-berkeley.md) / [Cognitive Tutor](../systems/cognitive-tutor.md) — the wrapped systems

## Sources

- [Weitekamp, Siddiqui & MacLellan, "TutorGym: A Testbed for Evaluating AI Agents as Tutors and Students," arXiv:2505.01563](https://arxiv.org/abs/2505.01563) `[read]` — full text
- [tutorgym.ai](https://tutorgym.ai) `[found]` · [GitHub](https://github.com/Teachable-AI-Lab/tutor_gym) `[found]`
