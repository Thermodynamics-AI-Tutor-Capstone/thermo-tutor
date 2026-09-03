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

## ⭐⭐ The architecture that actually enforces withholding

*"Teaching a Large Language Model Tutor to Withhold the Answer: A Supervisor Architecture"*
(arXiv:2608.12292, read 2026-09-03). **A deployed system**, and the first thing in this repository
that answers the question [CS50's 22% leakage](../systems/cs50-duck.md) poses.

Their premise is our finding, stated by someone else:

> *"An effective LLM tutor must often **decline to give an answer it could easily produce**…
> Reliable answer-withholding is therefore central to a tutor's value, yet **a capable model
> pressed by a frustrated student does not withhold reliably on a prompt alone**."*

**Their answer is to make withholding a machine-checkable contract, not a disposition.** Four
layers, and note how little of it is the model:

| Layer | What it is |
|---|---|
| ⭐ **Policy core** | **Non-LLM.** Reads *"only trusted learner state"* and sets a **per-turn ceiling on an eight-rung help ladder** |
| **Deterministic detector** | Mechanically **strips solution code** from the reply |
| **Separate LLM judge** | Checks each *risky* reply against the contract |
| The tutor itself | Generates within the ceiling the policy core set |

**The policy core is not a language model and reads only trusted state.** That is the structural
move: the decision about *how much help is allowed this turn* is taken away from the thing that can
be argued with. A frustrated student can pressure the tutor; they cannot pressure a rung ceiling
computed from learner state.

**This maps directly onto our design.** The
[sub-question verifier loop](grounding-and-verification.md) already produces trusted learner state
— which sub-steps are verified correct, how many attempts, where the error class was. **That state
is exactly what a policy core would read to set the ceiling.** Two pieces we found separately turn
out to be halves of one architecture.

### ⭐ Their evaluation method needs no students, which matters enormously to us

> *"We tune the behavior with an automated evaluation that **uses no human subjects**: **scripted
> student personas are driven through the live pipeline and re-scored by a stronger model**, and
> **we record each rejection's stated reason so failures are fixed by cause**."*

**We can build and tune the entire guardrail layer before IRB approval exists.** Given that
[IRB is a standing blocker](../../admin/irb.md), an evaluation loop that requires no students is
worth more to this project than most findings in this repository.

And it produced a genuinely interesting artefact — an **"over-help ladder"** of failure severity:

> *"from **blatant solution leaks**, to **naming the exact bug**, to **over-citing general facts**,
> with **each fix exposing the next**."*

**Over-helping is not one behaviour; it is a stack**, and fixing the obvious layer reveals a
subtler one underneath. Anyone who declares their guardrails working after removing solution leaks
has fixed rung one of at least three.

Their framing generalises past education, and is worth quoting to anyone who thinks this is a
prompt problem: *"the **measure, diagnose, and fix** loop as a reusable recipe for **any LLM agent
that must refuse a capability it has**."*

## ⚠ Scaffolding collapse — the failure has a name and a shape

*"Mitigating Scaffolding Collapse in Socratic Tutors via Representation Alignment"*
(arXiv:2607.19371, read 2026-09-03):

> *"**Scaffolding collapse**: under sustained student pressure, a tutor **gradually abandons guided
> inquiry and reveals solutions directly**."*

The important observation is *where* prior work looks:

> *"Prior defenses primarily constrain **observable responses** through prompting, preference
> optimization, or filtering, leaving the **internal representation drift that precedes
> trajectory-level collapse** largely unaddressed."*

**Collapse is gradual and begins before it is visible in the output.** By the time the tutor is
handing over answers, the drift happened several turns earlier — which is why turn-level filtering
catches it late.

They train against it (SFT warm-up, trajectory-weighted DPO, and a margin-preserving representation
loss anchored to frozen reference states), evaluated across **five STEM disciplines and five
red-teaming attack strategies**.

⚠ **Read the results as a floor, not a fix.** On Qwen3-8B their method *"lowers Collapse Rate to
**32%**, delays average collapse onset **beyond nine turns**, and keeps over-refusal low."*

**A third of dialogues still collapse, and the rest are delayed rather than prevented.** That is
the state of the art in a paper whose entire purpose is preventing it. **Assume our tutor will
collapse under pressure and design the surrounding system accordingly** — which is the argument for
the non-LLM policy core above.

**And our students are the red team.**
[22% of PeteChat's homework-context messages were boundary probes](../systems/petechat-purdue.md),
and [Jill Watson's stock-assistant baseline dropped from 68% to 5% refusal](../systems/jill-watson.md)
when hostile prompts were rewritten to be course-relevant. Sustained pressure is not a hypothetical
attack model; it is Wednesday night before a problem set is due.

## Connects to

- [Bastani 2025](../evidence/bastani-2025-harm.md) — the evidence base
- [Socratic tutoring](socratic-tutoring.md) — the stance guardrails try to enforce
- [productive failure](productive-failure.md) — why withholding help is defensible
- [grounding and verification](grounding-and-verification.md) — the technical layer
- [CS50 Duck](../systems/cs50-duck.md) — policy and tool designed together

## Sources

- ["Teaching a Large Language Model Tutor to Withhold the Answer: A Supervisor Architecture," arXiv:2608.12292](https://arxiv.org/pdf/2608.12292) `[read — full text, 2026-09-03]` — the policy core / detector / judge architecture and the no-human-subjects tuning loop
- ["Mitigating Scaffolding Collapse in Socratic Tutors via Representation Alignment," arXiv:2607.19371](https://arxiv.org/pdf/2607.19371) `[read — full text, 2026-09-03]` — collapse rate 32% after mitigation

- [Bastani et al., "Generative AI without guardrails can harm learning," PNAS 2025](https://www.pnas.org/doi/10.1073/pnas.2422633122) `[read]`
- [Tutor, Not Solver: PeteChat, arXiv:2606.09845](https://arxiv.org/pdf/2606.09845) `[read]`
- [CS50.ai docs](https://cs50.readthedocs.io/cs50.ai/) `[skimmed]`
