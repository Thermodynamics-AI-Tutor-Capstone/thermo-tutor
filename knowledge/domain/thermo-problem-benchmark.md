# Hoffmann et al. — Using LLMs for Solving Thermodynamic Problems

**Type:** study / benchmark
**One line:** A 22-problem thermodynamics benchmark whose most useful result is a single
failure: on an adiabatic process with reversibility unstated, **every model assumed
reversible, in every repetition.**
**Why we care:** That one finding names the deepest failure mode in our domain, and it maps
onto the most valuable thing a thermodynamics tutor could teach.

## The study

arXiv:2502.05195. **22 thermodynamic problems**, simple and advanced. Five models:
GPT-3.5, GPT-4, GPT-4o, Llama 3.1, and Mistral's le Chat. **Three repetitions each.**

## Results

- **Simple problems:** handled well. Large improvement GPT-3.5 → GPT-4; no significant
  difference GPT-4 → GPT-4o.
- **Advanced problems:** GPT-3.5 consistently failed to produce meaningful responses.
- **Problem 12 — the important one.** An adiabatic process where the text does *not* state
  whether the process is reversible. Assuming reversibility is incorrect. **Every studied
  model made that assumption, in all three repetitions.**

Other reported weak spots: property-table lookup, entropy calculations, symbolic handling of
van der Waals.

## Why Problem 12 is the most important result in our domain

**It is not hallucination.** The model didn't invent a fact. It made a **plausible,
standard, widely-taught engineering assumption that the problem did not license** — and
stated it with full confidence and no flag.

Three consequences:

**1. It's the same error our students make.** Conflating adiabatic with isentropic is a
classic undergraduate misconception and is already in
[our misconception list](../../research/domain/skill-graph-draft.md). A tutor that makes it
doesn't merely give a wrong answer — **it validates the student's misconception with
apparent authority.** That is worse than no tutor.

**2. It's invisible to verification.** [Grounding and verification](../concepts/grounding-and-verification.md)
catches wrong numbers. It does not catch a *correctly executed calculation on an unlicensed
assumption*. Every step is right. The premise is wrong. Tool calls don't help either — the
tool will happily compute an isentropic process.

This is the hardest problem in our architecture and there is no off-the-shelf fix.

**3. It names the highest-value teaching target.** "Which assumptions does this problem
statement actually license?" is:
- the skill models measurably lack
- a cross-cutting skill in [our knowledge model](../../research/domain/skill-graph-draft.md)
  that standard curricula rarely assess directly
- plausibly the thing that separates students who can do thermodynamics from students who
  can pattern-match it

**A tutor built specifically to teach assumption identification would be doing something no
existing system does, in the exact place base models fail.** Flagging this as the strongest
candidate for our project's distinctive pedagogical contribution.

## Design implications

- **Assumption extraction as an explicit step**, before any calculation. Make the student
  state what's given and what's assumed, and check that against a ground-truth annotation of
  the problem.
- **Annotate our problem set with licensed vs. unlicensed assumptions.** This is domain
  authoring work, it's tractable for a capstone team, and it's the substrate for both the
  tutoring feature and an evaluation.
- **Test for it.** This is exactly Problem 3 in
  [our teardown script](../../research/competitive-teardown/README.md) — the adiabatic trap.
  Every tool we evaluate should be probed with it.

## Open questions

- [ ] **Read the full paper.** All 22 problems, and per-model per-problem results.
- [ ] Is the problem set public? 22 problems with known traps is directly reusable.
- [ ] Do reasoning models (o3, extended thinking) fix Problem 12, or just fail more
      elaborately? **Testable today, cheaply, and worth doing early.**
- [ ] Does explicit assumption-extraction prompting help? (UTQA says prompt phrasing
      correlates weakly with performance — but that's phrasing, not scaffolding structure.)
- [ ] How many other "trap" problems exist in a standard thermo course?

## Connects to

- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis
- [UTQA](utqa.md) — independently finds the gap concentrated in irreversible scenarios
- [knowledge components](../concepts/knowledge-components.md) — assumption-identification as
  a first-class KC
- [our skill graph](../../research/domain/skill-graph-draft.md) — U5 and the cross-cutting skills
- [teardown methodology](../../research/competitive-teardown/README.md) — the adiabatic trap test

## Sources

- [Using Large Language Models for Solving Thermodynamic Problems, arXiv:2502.05195](https://arxiv.org/abs/2502.05195) `[skimmed]` — **priority read; it's short**
