# Knowledge Components

**Type:** concept
**One line:** The unit of "one thing a student can independently know or not know" — the
atom that mastery tracking, hint selection, and problem sequencing are all built on.
**Why we care:** Choosing the grain of our thermodynamics knowledge model is the single
highest-leverage decision in the project, and it's largely irreversible once data collection
starts.

## What a KC is

From the [CMU Cognitive Tutor](../systems/cognitive-tutor.md) tradition and the KLI
(Knowledge-Learning-Instruction) framework: an acquired unit of cognitive function that can
be inferred from performance on a set of related tasks.

Operationally: **if a student can do task A and not task B, A and B involve different KCs.**

Everything downstream depends on this decomposition:
- [Knowledge tracing](knowledge-tracing.md) estimates mastery *per KC*
- Hint ladders are authored *per KC*
- Problem selection picks the next problem by *KC readiness*
- Misconceptions attach *to KCs* → [AutoTutor's EMT](../systems/autotutor.md)

## The grain problem

Too coarse — `entropy` — and mastery is meaningless. A student can be fluent with ideal-gas
entropy relations and lost on entropy generation in an open system; one number hides that,
and a tutor that only knows "weak on entropy" can't do anything useful with it.

Too fine — `interpolating between two rows of Table A-6` — and you need thousands of
components, authoring becomes impossible, and no component ever accumulates enough
observations to estimate.

There's a genuine optimum, and it's empirical. Notably,
[VanLehn found substep-based tutoring *worse* than step-based](vanlehn-2011.md) (d = 0.40 vs
0.76) — decomposing too finely apparently removes the productive difficulty that makes a
step worth taking. Finer is not safer.

## The constraint people forget: observations per KC

Grain is not only a modeling choice; it's a **statistical budget**.

```
observations per KC per student  ≈  graded interactions per semester ÷ number of KCs
```

With ~300 graded interactions and ~90 KCs, that's ~3. Not enough for
[BKT](knowledge-tracing.md) to say anything.

**Do this arithmetic with real numbers from the actual course before finalizing the
graph.** It may force the grain coarser than the domain analysis wants, and that tension is
worth surfacing to the instructor rather than resolving quietly.
→ [open question C2](../../docs/03-open-questions.md)

## The cross-cutting KC problem, specific to engineering

Standard KC decomposition assumes components map to curriculum topics. Thermodynamics has
skills that cut across every topic and are rarely assessed directly:

- **`assumption-identification`** — what is and isn't licensed by this problem statement
- **`model-selection`** — ideal gas vs. tables vs. incompressible
- **`sanity-checking`** — order of magnitude, sign, second-law plausibility
- **`system-boundary-selection`**

These may predict success better than any chapter-aligned component. `assumption-
identification` in particular is the skill **every LLM tested fails** — see
[LLM capability in thermodynamics](../domain/llm-thermodynamics-capability.md).

That's a striking alignment: the thing models are worst at is plausibly the thing worth
teaching most, and it is nearly absent from standard curricula. If our knowledge model
represents it as a first-class component and our tutor teaches it deliberately, that is a
real and defensible contribution.

## Open questions

- [ ] Is there a published KC model for engineering thermodynamics anywhere? **Search
      DataShop** — CMU's learning-data repository hosts KC models for many domains.
- [ ] How do you *validate* a KC decomposition? (Learning-curve analysis: a correct model
      produces smooth power-law error decline per KC. Requires data we don't have yet.)
- [ ] Can cross-cutting skills be traced with the same machinery, or do they need something
      else?
- [ ] How much authoring effort per KC, realistically? This sets our achievable scope.

## Connects to

- [knowledge tracing](knowledge-tracing.md) — what gets estimated per KC
- [VanLehn 2011](vanlehn-2011.md) — granularity as the key variable
- [ALEKS](../systems/aleks.md) — knowledge states as an alternative decomposition
- [our skill graph draft](../../research/domain/skill-graph-draft.md) — the working model
- [AutoTutor](../systems/autotutor.md) — attaching misconceptions to components

## Sources

- [Koedinger, Corbett & Perfetti — the KLI framework](https://learnlab.org/index.php/background-readings) `[found]`
- [Kenneth Koedinger — Wikipedia](https://en.wikipedia.org/wiki/Kenneth_Koedinger) `[skimmed]`
- [VanLehn 2011](vanlehn-2011.md) `[skimmed]` — the granularity evidence
