# The dissociation: performance rose, learning did not (TUM, N = 275)

**Type:** evidence
**One line:** A three-arm RCT that separates a **scaffolded** AI tutor from **unrestricted**
ChatGPT and from no AI at all — and finds that **both AI conditions raised task scores while
neither raised learning.**
**Why we care:** This is [Bastani](bastani-2025-harm.md) refined, in a university course, with the
guardrailed arm tested properly. It is the cleanest statement of the trap our project has to
avoid, and its title says it: *performance and learning dissociate.*

> **Verification: `[abstract read in full]` — 2026-09-01. Elsevier's full text is
> bot-blocked (403); the abstract is complete and detailed, obtained via the DOAJ API.**

Bassner, P., Lenk-Ostendorf, B., Beinstingel, R., Wasner, T. & Krusche, S. (2025). *"Less stress,
better scores, same learning: The dissociation of performance and learning."*
**Computers and Education: Artificial Intelligence**, [DOI 10.1016/j.caeai.2025.100537](https://doi.org/10.1016/j.caeai.2025.100537).
Technical University of Munich.

## Design

**N = 275**, introductory programming (CS1) at TUM. A **90-minute exercise** on concurrency —
implementing a parallel sum with threading. Three randomised arms:

| Arm | What students got |
|---|---|
| **Iris** | A **scaffolded tutor** providing *"calibrated hints while withholding full solutions"* |
| **ChatGPT** | **Unrestricted** assistance, free to hand over complete solutions |
| **Control** | No AI; traditional web resources |

Measured: **performance** (auto-graded test coverage), **learning** (pre/post knowledge test plus a
separate code-comprehension task), and validated scales for **intrinsic, germane and extraneous
cognitive load**, **frustration**, and **intrinsic motivation**.

**Note what makes this better than most:** performance and learning are measured by *different
instruments*, so the dissociation can actually be observed rather than assumed.

## ⚠⚠ The result

> **"Both AI groups achieved substantially higher exercise scores than the control group…
> Despite these performance gains, neither AI condition produced greater pre–post knowledge gains
> or code-comprehension advantages."**

**Neither.** Not just the unguardrailed arm — **the scaffolded, hint-withholding tutor also failed
to produce a learning gain.** That is the same shape as
[Bastani's guardrailed arm scoring the same as controls](bastani-2025-harm.md), now replicated at
a university with a properly built tutor.

**The score distributions are the detail worth keeping:**

- **ChatGPT users clustered at high scores**
- **Control participants clustered at low scores**
- **Iris users spread across the full range**

The scaffolded tutor did not compress everyone to the top. It let students land where their
understanding put them — which is what an assessment is supposed to do, and exactly what
[the deployed RAG+SRL tutor's "variance compression"](../systems/rag-tutor-southeast.md) did *not*
do.

## ⭐ The mechanism: germane load went *down*

Both AI groups reported **lower frustration** and **reduced extraneous *and* germane cognitive
load**; intrinsic load did not differ.

**Reducing germane load is the finding.** Extraneous load is wasted effort and cutting it is good.
**Germane load is the effortful schema-building that *constitutes* learning** — so a tool that
reduces it has removed the work that produces understanding. That is a mechanism, not just a
correlation, for why scores rose and learning did not.

→ [productive failure](../concepts/productive-failure.md), whose entire premise is that the
struggle is the point.

## ⭐ "The comfort trap"

> **"Scaffolded, hint-first design preserved motivational benefits, whereas AI providing
> unrestricted solutions encouraged a 'comfort trap' where students' preferences misaligned with
> pedagogical effectiveness."**

- **Only Iris increased intrinsic motivation.**
- **Students rated ChatGPT as easier to use and more helpful.**

**Students preferred the tool that taught them less.** That single sentence should govern how we
read every satisfaction metric in this knowledge base — including
[LearnLM being called "patronizing"](../systems/learnlm.md) and
[UIC students preferring more succinct answers](student-ai-perceptions-2025.md). Preference and
pedagogy point in opposite directions, and it is measured here rather than asserted.

⚠ **So do not use student satisfaction as a proxy for tutor quality.** It selects for
answer-giving.

## What we take from this

1. **Scaffolding is worth building anyway** — it kept motivation up and produced an honest score
   distribution — **but do not promise it produces learning gains.** The best available evidence
   says it does not, at least in a single 90-minute session.
2. **Measure performance and learning with different instruments.** This study can see the
   dissociation only because it did. Ours must too.
   → [behavioral evaluation](../evaluation/behavioral-evaluation.md)
3. ⭐ **Measure germane cognitive load.** It is a validated scale, cheap to administer, and it is
   the mechanism. Nobody else in this base measured it, and a result on it would be a real
   contribution.
4. **Their own closing recommendation is our assessment-integrity argument:** we need *"assessment
   designs resilient to environments where performance no longer reliably tracks understanding."*
   → [assessment integrity](../practice/assessment-integrity.md)

## ⚠ Limits

One 90-minute session, one topic, one CS1 course. A single exercise is a very short dose, and
[Steenbergen-Hu & Cooper found ITS effects appear only over a full school year](../concepts/vanlehn-2011.md) —
so "no learning gain in 90 minutes" is not "no learning gain ever." **The dissociation is the
robust part; the null is dose-limited.**

We have the abstract, not the full text — Elsevier returns 403 to scripted access. **Figures,
effect sizes and the exact scales are unread.** Worth retrieving by hand.

## Connects to

- [Bastani et al. 2025](bastani-2025-harm.md) — the same dissociation, K-12, with a harm result
- [Productive failure](../concepts/productive-failure.md) — germane load is the struggle
- [Assessment integrity](../practice/assessment-integrity.md) — their closing recommendation
- [The deployed RAG + SRL tutor](../systems/rag-tutor-southeast.md) — variance compression, read differently
- [LearnLM](../systems/learnlm.md) — preference and pedagogy diverging, again
- [VanLehn 2011 and the meta-analyses](../concepts/vanlehn-2011.md) — the proximal/distal table

## Sources

- [Bassner, Lenk-Ostendorf, Beinstingel, Wasner & Krusche (2025), "Less stress, better scores, same learning," *Computers and Education: Artificial Intelligence*](https://doi.org/10.1016/j.caeai.2025.100537) `[abstract only — full text 403-blocked at Elsevier, 2026-09-01]` · gold OA, [DOAJ record](https://doaj.org/article/e332fcb5ad36419195f6e275704ba83f)
