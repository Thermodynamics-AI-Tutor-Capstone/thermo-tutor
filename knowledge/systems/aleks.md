# ALEKS

**Type:** system
**One line:** Assessment and LEarning in Knowledge Spaces — a thirty-year-old adaptive
assessment system based on knowledge space theory, now owned by McGraw Hill.
**Why we care:** It's an actual incumbent in engineering-adjacent courses, it solves the
mastery-estimation problem with a completely different formalism than knowledge tracing,
and it does it in 20–25 questions.

## Origin

Founded **1996** by mathematician **Jean-Claude Falmagne** at **UC Irvine**, building on
theory he'd developed with Belgian mathematician **Jean-Paul Doignon** since the early
1980s. NSF funding supported the prototype math and science courses. **Acquired by McGraw
Hill in 2013.**

## Knowledge space theory — the different idea

Most student modeling asks: *how likely is it this student has mastered skill X?* — a
per-skill probability. ([Knowledge tracing](../concepts/knowledge-tracing.md) works this
way.)

Knowledge space theory asks a structurally different question: **which of the
combinatorially many possible knowledge states is this student actually in?**

A *knowledge state* is the specific set of problems a student can solve. Not all
combinations are possible — prerequisite structure rules most of them out. The set of
feasible states forms a lattice, and assessment is a **search through that lattice**.

The payoff: because states are highly constrained by structure, ALEKS can locate a
student's precise state after only **20–25 questions**, from a space of trillions.

Then it serves problems at the **fringe** of that state — the things the student is
"ready to learn," in the sense of having all prerequisites and not yet having the skill.

## Why this is directly relevant to us

Our [skill graph](../../research/domain/skill-graph-draft.md) is, unknowingly, a first
draft of a knowledge structure — components with prerequisite edges.

The [grain problem](../../docs/03-open-questions.md) we flagged (too coarse and mastery is
meaningless; too fine and there's never enough data per component) is exactly the problem
KST attacks from the other end. **KST gets leverage from the prerequisite structure itself,
so it needs far fewer observations per component than knowledge tracing does.**

Given that a semester may only produce a few hundred graded interactions per student,
this may matter a great deal. Worth understanding properly before committing to BKT.

## Open questions

- [ ] Is ALEKS used in any Penn State engineering course? Ask the instructor sponsor.
- [ ] Is there a usable open-source KST implementation?
- [ ] How does KST compare to BKT/DKT empirically on the same data?
- [ ] Could our skill graph be authored as a knowledge structure from the start rather
      than retrofitted? **Decide before the graph is finalized.**
- [ ] How is ALEKS's underlying structure authored, and how expensive is it?

## Connects to

- [knowledge tracing](../concepts/knowledge-tracing.md) — the competing formalism
- [knowledge components](../concepts/knowledge-components.md) — the shared unit problem
- [our skill graph](../../research/domain/skill-graph-draft.md) — a proto knowledge structure
- [incumbent platforms](../practice/incumbent-platforms.md) — ALEKS is McGraw Hill's, and
  McGraw Hill publishes Cengel & Boles

## Sources

- [The Assessment of Knowledge, in Theory and in Practice — Falmagne](https://www.aleks.com/about_aleks/Science_Behind_ALEKS.pdf) `[found]` — the primary theory paper
- [Research Behind ALEKS — Knowledge Space Theory](https://www.aleks.com/about_aleks/knowledge_space_theory) `[skimmed]`
- [Knowledge spaces and learning spaces (eScholarship)](https://escholarship.org/uc/item/94b9x5sw) `[found]`
- [ALEKS — Wikipedia](https://en.wikipedia.org/wiki/ALEKS) `[skimmed]`
