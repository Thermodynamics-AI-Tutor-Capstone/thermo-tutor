# Knowledge Components

**Type:** concept
**One line:** The unit of "one thing a student can independently know or not know" — the
atom that mastery tracking, hint selection, and problem sequencing are all built on.
**Why we care:** Choosing the grain of our thermodynamics knowledge model is the single
highest-leverage decision in the project, and it's largely irreversible once data collection
starts.

> ⭐ **The theory behind this node now has its own home:
> [the KLI framework](kli-framework.md)**, read in full 2026-09-03. It supplies the KC *taxonomy*,
> two operational tests of KC complexity, and the mapping from KC type to appropriate instruction.
> **This node is the grain problem; that one is the vocabulary.**

## What a KC is

From the [CMU Cognitive Tutor](../systems/cognitive-tutor.md) tradition and the
[KLI (Knowledge-Learning-Instruction) framework](kli-framework.md): an acquired unit of cognitive
function that can be inferred from performance on a set of related tasks.

Operationally: **if a student can do task A and not task B, A and B involve different KCs.**

⭐ **Structurally, KLI defines a KC as a `condition → response` pair**, and classifies it on four
axes that turn out to determine what instruction works on it:

| Axis | Question | Why it matters |
|---|---|---|
| Application conditions | constant, or variable? | variable conditions must be **induced**, and mis-induced conditions are misconceptions |
| Response | constant, or variable? | |
| Relationship | can the student **say** it? | ⚠ doing and explaining are different KCs; either can pass while the other fails |
| ⭐ **Rationale** | is there a reason it is true, or is it a **convention**? | **Argumentation and self-explanation only work on KCs with a rationale.** You cannot reason a student into a steam-table value |

**Tagging our ~90 components on those four axes is an afternoon of work and it converts the skill
graph from a list into a decision table.** → [KLI framework](kli-framework.md)

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

There's a genuine optimum, and it's empirical.

⚠ **Correction (2026-09-03, from reading VanLehn in full).** This node previously said VanLehn
found substep-based tutoring *worse* than step-based, at d = 0.40 vs 0.76. **He did not.** Those
are two separate comparisons against different sets of no-tutoring studies. His **direct**
substep-vs-step contrast is **d = 0.16 across 11 comparisons, none of them reliable** — an
equivalence, not a penalty. → [VanLehn 2011](vanlehn-2011.md)

**The real reason not to decompose too finely is the statistical budget below, not a measured
learning penalty.** VanLehn's own conclusion is a plateau: finer than step buys nothing
measurable, but it does not cost anything either. What *does* cost is authoring effort and
observations per component.

### ⭐⭐ Two ways to test a grain empirically, from KLI

Both are runnable and neither needs a learning-curve model.

**1. Description length.** *"The more complex the description of the KC, the more complex is the
KC."* Koedinger et al.'s own counts across three domains: constant-constant KCs took **6–9 words**
to state, variable-constant **10–12**, variable-variable **12–21**. **Write every component in our
graph as a complete `if <conditions> then <response>` sentence and count. A component that will
not fit the pattern is probably two components.**

**2. ⭐ Median correct-execution latency**, which a step-based tutor logs for free:

| KC type | Time to execute correctly |
|---|---|
| constant-constant (a fact) | **3–6 s** |
| variable-constant (a category rule) | **6–10 s** |
| variable-variable (a schema) | **10–14 s** |

**A factor of two to three separates the types.** If components we designed as peers show latency
distributions two tiers apart, the decomposition is wrong — and this is the only method here that
can tell us so **from data**. ⚠ *Their curves are from typed entry in a structured interface; chat
turns are not comparable.* → [KLI framework](kli-framework.md), [VanLehn 2011](vanlehn-2011.md)

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

⭐⭐ **KLI probably has a name for these, and a method for finding them: *integrative knowledge
components*** — components *"not inferable from a single behavioral pattern, but only from
behavioral patterns across task situations varying in complexity."* The canonical case is students
who can do two one-step algebra translations and not the two-step problem that combines them; the
missing piece is the component that lets one expression embed in another.

**The discovery method is a ratio we can compute on paired problems:**

```
P(integrative KC)  =  P(success on the hard task)  ÷  P(success on the easy task)
```

*Can they read h from a table? Can they close an energy balance given h? Can they do a problem
needing both?* **The gap between the third and the product of the first two is a hidden,
nameable, teachable component** — and `assumption-identification` and `model-selection` are
exactly the shape of thing that only shows up in that gap.

⚠ **And integrative KCs need different instruction:** *"non-verbal forms of instruction (e.g.,
example study, repeated practice) may not be optimal… Providing and eliciting explanations may be
critical."* **More practice does not fix an integration failure.**
→ [KLI framework](kli-framework.md)

## Open questions

- [ ] Is there a published KC model for engineering thermodynamics anywhere? **Search
      DataShop** — CMU's learning-data repository hosts KC models for many domains.
- [ ] How do you *validate* a KC decomposition? (Learning-curve analysis: a correct model
      produces smooth power-law error decline per KC. Requires data we don't have yet.)
- [ ] Can cross-cutting skills be traced with the same machinery, or do they need something
      else?
- [ ] How much authoring effort per KC, realistically? This sets our achievable scope.
- [ ] ⭐ **Which of our components have a rationale and which are conventions?** Unasked, and the
      answer decides whether Socratic dialogue is licensed on each one.
      → [KLI framework](kli-framework.md)
- [ ] ⭐ **Are the cross-cutting skills above actually integrative KCs?** Testable with the
      subtraction ratio, on paired problems, from ordinary homework data.

## Connects to

- [KLI framework](kli-framework.md) — the theory this node is the practice of: KC taxonomy, complexity tests, and what instruction each KC type needs
- [knowledge tracing](knowledge-tracing.md) — what gets estimated per KC
- [VanLehn 2011](vanlehn-2011.md) — granularity as the key variable, and the mechanism: a correct self-generated solution generalizes, strengthens, constructs and debugs every KC it touches
- [ALEKS](../systems/aleks.md) — knowledge states as an alternative decomposition
- [our skill graph draft](../../research/domain/skill-graph-draft.md) — the working model
- [AutoTutor](../systems/autotutor.md) — attaching misconceptions to components

## Sources

- [Koedinger, Corbett & Perfetti (2012), "The Knowledge-Learning-Instruction (KLI) Framework," *Cognitive Science* 36(5), 757–798](https://doi.org/10.1111/j.1551-6709.2012.01245.x) `[read — full text, 35 pp., 2026-09-03]` — **now a primary**, with its own node at [kli-framework.md](kli-framework.md). Local: `course-materials/papers/koedinger-2012-kli-framework.pdf`
- [Kenneth Koedinger — Wikipedia](https://en.wikipedia.org/wiki/Kenneth_Koedinger) `[skimmed]`
- [VanLehn (2011), *Educational Psychologist* 46(4)](https://doi.org/10.1080/00461520.2011.611369) `[read — full text, 25 pp., 2026-09-03]` — the granularity evidence, and the completion mechanism that says *what* a knowledge component is for: "when students self-generate a correct solution, they generalize, strengthen, construct, and debug all the knowledge components required by the solution"
