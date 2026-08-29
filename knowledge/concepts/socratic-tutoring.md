# Socratic Tutoring (and how students subvert it)

**Type:** concept
**One line:** The dominant design stance in LLM tutoring — ask questions rather than give
answers — and the empirical evidence that students route around it.
**Why we care:** Our project brief specifies Socratic questioning. The best available
evidence says that specification, taken literally, produces a predictable failure. This
node is the argument for what to do instead.

## The stance

Nearly every deployed LLM tutor encodes some version of: *don't give the answer, ask a
guiding question instead.* [CS50 Duck](../systems/cs50-duck.md) ("without spoiling answers
outright"), [Stan](../systems/stan-udel.md) (explicit refusal to solve),
[PeteChat](../systems/petechat-purdue.md) ("Tutor, Not Solver"),
[LearnLM](../systems/learnlm.md) (prompted Socratic in the UK RCT), ChatGPT Study Mode,
Claude Learning Mode, Gemini Guided Learning.

It's the right instinct. [Bastani](../evidence/bastani-2025-harm.md) shows what happens
without it: unguarded AI made students **17% worse** on unassisted exams.

## The evidence that it doesn't work as intended

A 2026 bottom-up taxonomy coded **2,874 student turns across 221 sessions** with a Socratic
AI physics tutor into 357 categories. The top 25 categories account for roughly half of all
turns, clustering into two bands:

**Band 1 — equation handling** (~1/3 of the top categories). Writing energy equations
(8.3%), solving for velocity (2.8%), computing heights (2.3%), algebraic simplification
(1.7%). The authors name this "epistemic games": symbol manipulation with limited
conceptual engagement.

**Band 2 — meta-procedural requests.** Asking the tutor **"what do I do next"** was the
**second-most-common student move overall, at 4.4% of all turns.** Plus requests for the
relevant principle (1.5%) and the problem's assumptions (1.3%).

The top 20 categories contained **virtually no** conceptual reasoning, prediction, or
critical engagement with the tutor's suggestions.

The authors' summary, worth quoting exactly:

> *"a tutor explicitly designed not to direct students nevertheless elicits a discourse in
> which directing is the second-most-requested service."*

## Why it fails

A stance is not a mechanism. "Be Socratic" is an instruction to the model about how to
behave; it has no representation of *why* a given question is the right move now, no memory
of what the student has already tried, and no budget. So:

- The model can be argued out of it — see the
  [defection script](../../research/competitive-teardown/README.md)
- Even when it holds, it converts an answer-seeking student into a **frustrated**
  answer-seeking student, which is not obviously better
- It refuses uniformly, which means it refuses *legitimate* strategic help identically to
  illegitimate answer-seeking

That third point is the important one, and it's a critique of the research framing as much
as of the systems. **"What do I do next" is not necessarily a student failure.** Sometimes a
student genuinely is stuck at the level of strategy, not concept — they understand entropy
fine and don't know which of four relations applies here. Question-asking, in that moment,
is obstruction dressed as pedagogy. See
[open question C1](../../docs/03-open-questions.md).

## What to do instead: graduated scaffolding with a budget

The design that follows from the evidence:

1. **Hint levels, not refusal.** A ladder from elicit → orienting question → strategic hint
   → conceptual hint → worked step → full reveal. The student can always get more; getting
   more costs something and is recorded.
2. **A productive-failure budget.** Time or attempts must be spent before the ladder
   advances. [Productive failure](productive-failure.md) says the struggle is where learning
   happens — but *bounded* struggle, not unbounded.
3. **The policy lives in code.** A deterministic controller with access to attempt history
   picks the move; the LLM renders it in language. The model is the mouth, not the brain.
   → [guardrails](guardrails.md)
4. **Grant the meta-procedural request, at the right grain.** When a student asks "what do
   I do next," answer at the level of *strategy* — "you have an open system with one inlet
   and one outlet; which balance applies?" — rather than refusing or solving.
5. **Track defection as a metric.** How often students escalate, and how far, is signal
   about the problem, the student, and the ladder. Log it.

## Open questions

- [ ] Is "what do I do next" pathology or legitimate need? Distinguishable from the log?
      (Think-alouds → [open questions A4](../../docs/03-open-questions.md))
- [ ] Does a hint ladder with a budget actually beat refusal? **Testable in a
      Wizard-of-Oz prototype with no engineering.**
- [ ] What does the *human* thermo TA do when asked "what do I do next"? Observe office
      hours before designing the ladder.
- [ ] Optimal budget size — how long should a student be left to struggle?

## Connects to

- [productive failure](productive-failure.md) — the theory behind the budget
- [guardrails](guardrails.md) — where policy should live
- [Bastani 2025](../evidence/bastani-2025-harm.md) — why you need *something* here
- [AutoTutor](../systems/autotutor.md) — the disciplined pre-LLM alternative to a stance
- [engagement decay](engagement-decay.md) — frustrated students stop coming back

## Sources

- [A bottom-up taxonomy of student discourse with a Socratic AI physics tutor, arXiv:2608.07373](https://arxiv.org/html/2608.07373v1) `[skimmed]` — **the key source. Needs a full read by someone on the team.**
- [Bastani et al., PNAS 2025](../evidence/bastani-2025-harm.md) `[skimmed]` — the guardrail necessity argument
- Practitioner comparisons of study modes (ChatGPT "trigger-happy", Gemini "patronizing") — see [docs/00-landscape-review.md](../../docs/00-landscape-review.md)
