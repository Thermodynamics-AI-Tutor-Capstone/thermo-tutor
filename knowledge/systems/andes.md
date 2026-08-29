# Andes

**Type:** system
**One line:** A step-based intelligent tutoring system for university physics, developed
at Pittsburgh and the US Naval Academy — the closest historical analogue to what we're
building.
**Why we care:** Andes is the proof that a well-designed pre-LLM tutor produces real
learning gains in exactly our kind of subject. If we can't beat Andes, we haven't advanced.

## What it was

Developed at the **University of Pittsburgh** and the **United States Naval Academy**, with
the Cognitive Science Program at the **Office of Naval Research**. Kurt VanLehn and
colleagues.

The design philosophy, stated by its authors, is unusually disciplined:

> Andes replaces only the students' pencil and paper as they do problem-solving homework.
> Students do the same problems as before, study the same textbook, and attend the same
> lectures, labs and recitations.

That restraint is the opposite of most modern AI tutoring pitches, which propose to
replace or restructure instruction. Andes changed one surface and left everything else
alone — which is also why its effects are attributable.

## The step-based commitment

Where most tutoring systems have students enter only a final answer, **Andes has students
enter the whole derivation**: drawing vectors, drawing coordinate systems, defining
variables, writing equations. It gives feedback after **each step**.

This is the mechanism behind [VanLehn's step-based finding](../concepts/vanlehn-2011.md)
(d = 0.76 vs. no tutoring, against d = 0.79 for human tutors). It's also the single
biggest design gap between classical ITS and a chatbot: a student typing "I'm stuck on 4b"
and reading a paragraph is doing **answer-based** tutoring with more words.

**Andes made externalizing your reasoning mandatory. A chat box makes it optional.**

Internally, Andes used **Bayesian networks** for decision-making — inferring which solution
path a student was pursuing and what they knew.
→ [knowledge tracing](../concepts/knowledge-tracing.md)

## Evidence

Five years of experimental evaluation at the US Naval Academy indicate Andes
**significantly improves student learning**. Hundreds of students.

## What this means for a thermodynamics tutor

Thermodynamics problem solving has the same structure Andes targeted: choose a system,
identify assumptions, select relations, write balances, solve. Every one of those is a
*step* that can be entered and checked — and most of them are exactly where students go
wrong. See [our skill graph](../../research/domain/skill-graph-draft.md), particularly the
cross-cutting skills.

**Design implication:** if our tutor is a chat window, we've chosen the weaker interaction
granularity for no reason. A structured problem-solving surface with conversational help
alongside it is closer to what the evidence supports.

## Open questions

- [ ] What were the actual effect sizes at Annapolis, year by year?
- [ ] How much authoring effort per problem? (This is the hidden cost of step-based ITS
      and the reason chatbots won on convenience.)
- [ ] Is Andes still available? Any modern successor or open-source reimplementation?
- [ ] Has anyone combined an Andes-style step interface with an LLM for the hints?
      **This may be an open and tractable research direction.**

## Connects to

- [VanLehn 2011](../concepts/vanlehn-2011.md) — the meta-analysis that Andes helped produce
- [knowledge components](../concepts/knowledge-components.md) — what a "step" is
- [Cognitive Tutor](cognitive-tutor.md) — the other great step-based lineage
- [our skill graph](../../research/domain/skill-graph-draft.md) — thermo steps to target

## Sources

- [VanLehn et al., "The Andes Physics Tutoring System: Lessons Learned," IJAIED (2005)](https://dl.acm.org/doi/10.5555/1434930.1434932) `[skimmed]`
- [Andes: An Intelligent Tutor for Classical Physics](https://doi.org/10.3998/3336451.0006.110) `[found]`
- ["The Andes Physics Tutoring System: Five Years of Evaluations"](https://www.researchgate.net/publication/221297239_The_Andes_Physics_Tutoring_System_Five_Years_of_Evaluations) `[found]`
