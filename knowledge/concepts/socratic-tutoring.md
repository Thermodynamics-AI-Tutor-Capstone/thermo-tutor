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

## The evidence that it doesn't work as intended — and its real weight

> **Verification: `[read]` — full text, 2026-08-31. This node previously overstated the
> paper.** Corrections are marked ⚠ below. The headline finding survives; the sweeping
> claims around it do not.

Hashmi & Rebello (Purdue, arXiv:2608.07373) built a bottom-up taxonomy of student discourse
with a Socratic AI physics tutor.

**The setting, precisely:** an introductory calculus-based mechanics course for engineers at
a large US midwestern public research university, Fall 2025, 1,508 enrolled. The tutor
(Django + Postgres + RAG over course materials, system-prompted to use Socratic prompting
and *"scaffold conceptual setup before symbolic execution"*) ran in **5 of 34 recitation
sections**, during **Week 8 of a 16-week semester**, on essentially **one multi-step
problem** (a ramp-into-loop problem requiring the critical condition at the top of the loop
plus energy conservation). Students used it **for extra credit** — so this is compelled, not
voluntary, use.

**Corpus:** 5,513 messages from **240 students** across **221 sessions**, of which **2,874
are student turns**.

**Method** (reusable — see below): GPT-5.4-mini assigned each turn an emergent free-text
label with four turns of prior context; 833 raw labels were consolidated by embedding
(`text-embedding-3-small`) + agglomerative clustering into **357 categories**; validated
against a human expert on a stratified 10% sample at **Cohen's κ = 0.78** (84% raw
agreement).

**The distribution.** Top 20 categories = **47.2%** of turns; top 25 ≈ 52%; categories with
≥5 messages cover 86%.

| Category | n | % of student turns |
|---|---|---|
| Writing Energy Equation | 239 | **8.3%** |
| **Next Step Guidance** | 127 | **4.4%** |
| Presenting Problem Statement | 107 | 3.7% |
| Velocity Solving | 80 | 2.8% |
| Solving for Height | 68 | 2.4% |
| Computing Heights | 65 | 2.3% |
| Tutor Interaction Checks | 63 | 2.2% |
| Restating Problem | 61 | 2.1% |
| Centripetal Relation Setup | 50 | 1.7% |
| Substitution & Simplification | 49 | 1.7% |
| Requesting Solution Help | 47 | 1.6% |
| Asking for Principles | 42 | 1.5% |
| Assumptions About Problem | 37 | 1.3% |

**Band 1 — equation handling and symbolic execution.** Roughly a third of top-20 turns:
writing relationships, manipulating them, substituting, reporting numbers. Consistent with
Sherin's symbolic forms and Tuminaro & Redish's *epistemic games*.

**Band 2 — meta-procedural requests**, where the student asks the tutor what to do rather
than advancing the problem: Next Step Guidance (4.4%) + Requesting Solution Help (1.6%) +
Asking for Principles (1.5%) + Assumptions About Problem (1.3%) ≈ **8.8% of all turns**.

The authors' summary, worth quoting exactly:

> *"a tutor explicitly designed not to direct students nevertheless elicits a discourse in
> which directing is the second-most-requested service."*

## ⚠ How much weight this can actually bear

Three corrections to how this knowledge base previously used the paper:

**⚠ 1. "Second-most-common" means 4.4%, not a majority.** What makes it notable is its
*rank* in a tutor built never to direct — not its share. The finding is real and pointed;
it is not evidence that most students most of the time are trying to extract direction.

**⚠ 2. The claim that conceptual reasoning was "virtually absent" is the authors' own
hedge, not their finding.** Their words: the absence at the top *"is suggestive but should
be interpreted with care: it may reflect what students actually do, or it may reflect that
conceptual moves are spread thinly across many low-count categories in the long tail rather
than absent."* 357 categories with a long tail is exactly the shape in which thinly-spread
conceptual moves would hide. **Do not assert that students weren't reasoning conceptually.**

**⚠ 3. It cannot support causal claims about Socratic design.** Stated plainly by the
authors: *"The analysis is observational; nothing here licenses causal claims about what the
tutor's design contributes to the patterns we observe."* There is no comparison condition. A
non-Socratic tutor might elicit *more* meta-procedural requests, not fewer — nobody has
checked.

**Scope limits, also theirs:** single site, single course, single tutor, one week, and
dominated by one problem. Category names like *Centripetal Relation Setup* obviously do not
transfer. Step 2's coherence audit had a single rater.

**What survives, and it is enough to design around:** in a real deployment of a genuinely
Socratic tutor, asking the tutor what to do next was the single most common thing students
did other than write equations. That is a phenomenon worth designing for, whatever its
cause.

## A methodological gift, separate from the finding

The pipeline — **LLM open-coding with rolling context → embedding-based consolidation →
κ-validated against a human-coded stratified sample** — is directly reusable for our own
[student interview](../../research/student-interviews/protocol-draft.md) and think-aloud
transcripts, and for tutor session logs later. It converts qualitative coding from a
multi-week team effort into something a capstone can actually complete, *with a defensible
reliability statistic attached*. Their parameters (4-turn context window, distance threshold
0.40 chosen by sweep with manual coherence inspection, κ = 0.78) are a working starting
point.

**Adopt this method.** It is arguably more valuable to us than the finding.

## Why the stance fails

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

1. **Hint levels, not refusal — and the ladder must *terminate*.** A ladder from elicit →
   orienting question → strategic hint → conceptual hint → worked step → **explicit
   contrast between what the student tried and the canonical solution.**

   That last rung is not a failure state.
   [Productive failure](productive-failure.md) ranks *"instruction building on student
   solutions"* as the **#1 of seven** fidelity criteria (g = 0.56 vs 0.20, p = .02), and effect
   size scales with fidelity. **A tutor that only ever asks questions delivers the failure and
   skips the instruction — which is productive failure done at low fidelity.**

   ⚠ **And the hints in between must be principle-based or metacognitive, never step-level.**
   Scaffolded problem-solving-before-instruction has failed on average in meta-analysis
   (**g = −0.08, 60 comparisons**), with hint-sequence systems named explicitly. A working
   university script: *"what information do you have in the problem?"* → *"what other kind of
   information would you need to continue?"* → *"where might you find this?"* — prompts that
   focus attention **without providing additional information**.
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
- [ ] **Does a non-Socratic tutor elicit fewer meta-procedural requests, or more?** Nobody
      has run the comparison. It is a clean, cheap experiment and it would convert this
      paper's observation into an actual finding about Socratic design.
- [ ] Does the pattern hold outside a single heavily-scaffolded recitation problem?
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

- [Hashmi & Rebello, "A bottom-up taxonomy of student discourse with a Socratic AI physics tutor," arXiv:2608.07373](https://arxiv.org/abs/2608.07373) `[read]` — full text. NSF grants 2111138, 2300645.
- [Bastani et al., PNAS 2025](../evidence/bastani-2025-harm.md) `[skimmed]` — the guardrail necessity argument
- Practitioner comparisons of study modes (ChatGPT "trigger-happy", Gemini "patronizing") — see [docs/00-landscape-review.md](../../docs/00-landscape-review.md)
