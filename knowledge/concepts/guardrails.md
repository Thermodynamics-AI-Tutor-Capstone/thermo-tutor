# Guardrails

**Type:** concept
**One line:** The constraints that stop a tutor becoming an answer machine — and the
evidence that they prevent harm without producing learning.
**Why we care:** Guardrails are the field's consensus solution. Understanding exactly what
they do and don't buy keeps us from mistaking damage control for a contribution.

## What the evidence says guardrails do

From [Bastani et al. (PNAS 2025)](../evidence/bastani-2025-harm.md), ~1,000 students:

| Arm | During practice | Later, unassisted exam |
|---|---|---|
| **GPT Base** (unguarded) | +48% | **−17%** |
| **GPT Tutor** (guardrailed) | +127% | **≈ same as control** |
| Control | baseline | baseline |

**Guardrails turned a −17% learning penalty into zero.** That's the whole measured effect.

Two conclusions, and both matter:

1. **Guardrails are necessary.** Deploying an unguarded LLM into a course actively harms
   learning. That's the strongest empirical claim in this entire knowledge base.
2. **Guardrails are not sufficient.** The best-designed arm produced **no learning benefit**
   over students with a textbook and their notes.

Anyone claiming their guardrailed tutor helps students learn is claiming something the
largest RCT in the field did not find. → [the paper, §IV](../PAPER.md)

## Where guardrails can live, weakest to strongest

**1. System prompt.** "Don't give the answer; ask a guiding question." What ChatGPT Study
Mode, Claude Learning Mode, Gemini Guided Learning, and most course tutors do.

**We now have a hard number on how badly this fails at scale.** CS50 analysed **10 million
messages** from the Duck — the reference implementation of "won't spoil the answer," backed
by course academic-integrity policy — and found responses containing code blocks in:

| | Leakage |
|---|---|
| All responses | **22%** |
| **Conversations** | **48%** |

And upgrading GPT-4 → GPT-4o made it **worse**: conversation-level leakage rose from 44% to
**56%**. Their name for the cause: **"instruction dilution"** — the model losing guidelines
buried in a long system prompt.

**Two conclusions:**
- **A system prompt is not a guardrail.** The best-resourced deployment in the field leaks in
  roughly half of conversations.
- **Compliance is not stable across model versions.** A silent 12-point regression from an
  upgrade nobody would think to re-validate. **Pedagogical compliance must be a regression
  test**, re-measured on every model change. → [CS50 Duck](../systems/cs50-duck.md)

They also found few-shot prompting counterproductive as a fix — examples inflate every
request and *worsen* dilution — and got their improvement instead from **fine-tuning on 50
curated conversations**.

**2. Fine-tuning / preference alignment.** Put the behavior in the weights.
[LearnLM](../systems/learnlm.md) and [PeteChat](../systems/petechat-purdue.md) do this.
Stronger and more expensive; LearnLM's own numbers suggest bounded returns.

**3. Output verification.** Check the response before the student sees it.
[Jill Watson](../systems/jill-watson.md) uses textual entailment;
[Khan Academy](../systems/khanmigo.md) runs a separate math agent verifying every
calculation. → [grounding and verification](grounding-and-verification.md)

**4. Deterministic policy outside the model.** The model doesn't decide whether to help — a
controller with access to attempt history and a
[productive-failure budget](productive-failure.md) does, and the model renders the chosen
move in language.

**Almost nobody has built layer 4, and it is the layer the evidence most supports.**
→ [Socratic tutoring](socratic-tutoring.md)

## The CS50 lesson: couple the guardrail to the policy

[CS50's Duck](../systems/cs50-duck.md) is "mindful of CS50's policy on academic honesty."
The tool and the course's integrity rules were designed **together**.

This is doing more work than it appears. Most course tutors have to *guess* where the line
is between help and cheating, because the course never wrote it down precisely enough to
implement. CS50 wrote it down, then built to it.

**Actionable for us:** ask the instructor sponsor to state, concretely, what help is
legitimate on a thermodynamics problem set and what isn't. Not a philosophy —
implementable rules. If they can't, that's a finding worth reporting, and the tutor's
behavior will be arbitrary until it's resolved. → [C5](../../docs/03-open-questions.md)

## Open questions

- [ ] Which layer actually stops defection? **Testable directly with the teardown script.**
- [ ] Does a deterministic policy layer beat a prompt? Nobody appears to have measured this.
      **This is a plausible capstone contribution.**
- [ ] Is there a guardrail design that produces *positive* learning, not just zero harm?
      The open problem in the field.
- [ ] How much do guardrails cost in student satisfaction, and does that feed
      [engagement decay](engagement-decay.md)?

## Connects to

- [Bastani 2025](../evidence/bastani-2025-harm.md) — the evidence base
- [Socratic tutoring](socratic-tutoring.md) — the stance guardrails try to enforce
- [productive failure](productive-failure.md) — why withholding help is defensible
- [grounding and verification](grounding-and-verification.md) — the technical layer
- [CS50 Duck](../systems/cs50-duck.md) — policy and tool designed together

## Sources

- [Bastani et al., "Generative AI without guardrails can harm learning," PNAS 2025](https://www.pnas.org/doi/10.1073/pnas.2422633122) `[skimmed]`
- [Tutor, Not Solver: PeteChat, arXiv:2606.09845](https://arxiv.org/pdf/2606.09845) `[skimmed]`
- [CS50.ai docs](https://cs50.readthedocs.io/cs50.ai/) `[skimmed]`
