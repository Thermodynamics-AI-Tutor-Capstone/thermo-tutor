# CyclePad and CycleTalk

**Type:** system
**One line:** An "articulate virtual laboratory for engineering thermodynamics" from
Northwestern, deployed in the US Naval Academy's thermodynamics curriculum since **1996**, plus
its CMU dialogue-agent successor.
**Why we care:** **This is the actual closest historical precedent for our project, and this
knowledge base missed it entirely for two weeks.** It is a thermodynamics tutoring system, in a
real engineering curriculum, from the same ONR programme that produced
[Andes](andes.md) — and nobody in the modern LLM-tutoring literature cites it.

> **Created 2026-08-31.** We found it only because the *Andes: Lessons Learned* paper mentions
> it in passing. **This node is a stub built from that mention plus provenance checks — nobody
> has read the CyclePad papers yet.** It is currently the highest-value unread item in the
> knowledge base.

## How we found it

From *Andes: Lessons Learned*, describing the ONR initiative that funded both projects:

> *"Two projects resulted, an extensive implementation of Ken Forbus' existing **CyclePad**
> software in the **thermodynamics curriculum at the Academy**, and a more ambitious project to
> build a new physics tutor…"*

So Andes and CyclePad are **siblings** — same funder, same institution, same era. Andes is the
one the AI-in-education field remembers. **CyclePad is the one in our domain.**

## What it is, as far as we currently know

**CyclePad** — Kenneth Forbus and the Qualitative Reasoning Group, Northwestern University.
Described as an *"articulate virtual laboratory for engineering thermodynamics."* Students
**construct and analyse thermodynamic cycles**, and a **hypertext explanation facility exposes
the chain of reasoning behind every derived value**.

The **US Naval Academy Mechanical Engineering department has been evaluating and incorporating
it since 1996.**

**CycleTalk** — Carnegie Mellon HCII. A **dialogue agent guiding design work with an articulate
simulator**, including a study on **goal orientation × tutoring style** in a CMU thermodynamics
course.

## Why this matters more than its obscurity suggests

**1. "Articulate" is the architecture we independently arrived at.** A simulator that computes
correct thermodynamic state and can *explain the derivation chain* for every value is
structurally what our [property-tools layer](../domain/property-data-tools.md) plus
[render-don't-read](../domain/diagram-reading.md) proposal describes. Forbus built it in the
1990s with qualitative reasoning instead of an LLM. **The reasoning layer is the part we would
not have to invent.**

**2. Cycle design is exactly our Tier 3.** [ThermoQA's](../domain/thermoqa.md) hardest tier is
Rankine, Brayton, vapour-compression and combined-cycle analysis — and that is CyclePad's entire
subject. Frontier models score as low as **52.7%** there.

**3. CycleTalk already ran the experiment we keep proposing.** A dialogue agent on top of an
articulate thermodynamics simulator, with a study on **goal orientation × tutoring style** — and
goal orientation is precisely the at-risk screen the
[productive failure literature](../concepts/productive-failure.md) points us to
(performance-oriented students, not low-ability ones, are the ones who withdraw effort under
struggle). **Someone has plausibly already measured the interaction we care most about.**

**4. It is a live counterexample to our own framing.** We have been writing that
[Stan](stan-udel.md) is the only thermodynamics tutoring system. That was wrong by thirty years.

## What we need to find out — all of it

- [ ] **Read the CyclePad papers.** Forbus, Whalley, Everett, Ureel, Brokowski, Baher & Kuehne,
      *"CyclePad: An articulate virtual laboratory for engineering thermodynamics"* (Artificial
      Intelligence, 1999) is the canonical citation to chase. Northwestern QRG hosts a
      publications page.
- [ ] **What are the USNA evaluation results?** Nearly thirty years of use in a real mechanical
      engineering curriculum should have produced outcome data. **If it exists, it is the only
      long-run evidence for thermodynamics tutoring anywhere.**
- [ ] **Is CyclePad still available?** Given
      [what happened to Andes' problem library](andes.md), assume the software may be
      unobtainable and check early.
- [ ] **Read the CycleTalk papers**, especially the goal-orientation × tutoring-style study.
      CMU HCII / PSLC should have them.
- [ ] **What does its qualitative-reasoning engine actually do**, and could an LLM sit on top of
      it the way CycleTalk's dialogue agent did?
- [ ] Does its explanation facility generate the **pairwise contrast material**
      [productive failure](../concepts/productive-failure.md) says consolidation needs?

## Why nobody cites it

Worth noting as a finding in its own right: the 2023–2026 LLM-tutoring literature does not
reference CyclePad, and neither does [Stan](stan-udel.md), the one contemporary thermodynamics
assistant. **A thirty-year-old, domain-exact, curriculum-embedded precedent is invisible to the
current field.** If our capstone does nothing else, connecting that line of work to the present
one is a real contribution — and it protects us from re-deriving what Forbus's group already
built.

## Connects to

- [Andes](andes.md) — the sibling project, and where we found this
- [property data tools](../domain/property-data-tools.md) — "articulate simulator" is our tool layer
- [diagram reading](../domain/diagram-reading.md) — render-don't-read, arrived at independently
- [ThermoQA](../domain/thermoqa.md) — cycle analysis is the hardest tier
- [productive failure](../concepts/productive-failure.md) — goal orientation as the at-risk screen
- [Stan](stan-udel.md) — the contemporary thermodynamics system that doesn't cite this one

## Sources

- Forbus et al., "CyclePad: An articulate virtual laboratory for engineering thermodynamics," *Artificial Intelligence* (1999) `[found]` — **priority read**
- Northwestern Qualitative Reasoning Group publications `[found]`
- CycleTalk (CMU HCII) — dialogue agent + articulate simulator; goal orientation × tutoring style study `[found]`
- [VanLehn et al., "Andes: Lessons Learned"](https://oli.cmu.edu/wp-content/uploads/2012/05/VanLehn_2005_Andes_Physics_Tutoring_System.pdf) `[read]` — the passage that surfaced this
