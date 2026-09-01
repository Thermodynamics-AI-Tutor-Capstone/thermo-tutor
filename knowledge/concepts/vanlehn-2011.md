# VanLehn 2011 — the effect sizes that anchor the field

**Type:** concept / meta-analysis
**One line:** The review that corrected Bloom's 2 sigma claim and showed step-based
intelligent tutoring nearly matches human tutoring.
**Why we care:** It sets the bar our project has to clear, and it identifies *interaction
granularity* — not feedback intelligence — as the variable that predicts learning.

## The paper

Kurt VanLehn, *"The Relative Effectiveness of Human Tutoring, Intelligent Tutoring Systems,
and Other Tutoring Systems,"* **Educational Psychologist, 2011**. Reviews experiments
published 1975–2010; 10 comparisons drawn from 28 evaluation studies. 1,400+ citations.

## The two headline numbers

**Human tutoring: d = 0.79**, not Bloom's 2.0. → [Bloom's 2 sigma](blooms-two-sigma.md)

**Step-based ITS: d = 0.76** against no tutoring — nearly identical.

Head to head, human tutoring beat step-based ITS by only **d = 0.21**, and beat
substep-based systems by **d = 0.12**.

## The taxonomy that actually matters

VanLehn classified systems by **interaction granularity** — what the student is required to
enter:

| Granularity | Student enters | vs. no tutoring |
|---|---|---|
| Answer-based | Final answer only | ~0.3 |
| **Step-based** | **Each step of the derivation** | **0.76** |
| Substep-based | Sub-steps within steps | 0.40 |

Two counterintuitive readings:

**Granularity beats intelligence.** The strongest predictor of learning was not how clever
the tutor's feedback was, but **how much of their reasoning the student had to externalize.**

**⭐ The "interaction plateau" — and the ambiguity is now resolved.**

This node previously flagged an unresolved question: does substep-based tutoring genuinely
*underperform* step-based (d = 0.40 vs 0.76), or are those numbers not comparable? **Resolved:
they are not comparable, and substep is not worse.**

Three independent lines converge:

1. **VanLehn's own head-to-head comparisons run the other way.** Against *human tutoring*,
   **substep-based scored d = −0.12** (i.e. substep slightly *beat* the human tutors) while
   step-based scored d = +0.21 (human tutors slightly ahead).
2. **Kulik & Fletcher independently found step 0.60 ≈ substep 0.63.**
3. The plateau hypothesis asserts equivalence: **human ≈ substep ≈ step > answer-based.**

The 0.76 / 0.40 pair are **separate small-k comparisons against no tutoring**, not a
granularity contrast. Reading them as one was the error.

**Design implication, now clean:** a **step-level inner loop is non-negotiable**; finer-than-step
is **open, not disfavoured**; and **answer-only (~0.31) is the tier to avoid.** That last point
is the one that matters for a chat interface.
→ [Andes](../systems/andes.md), [productive failure](productive-failure.md)

## ⚠⚠ The number everyone quotes, and the one they don't

We still cannot get VanLehn 2011 or Kulik & Fletcher 2016 as primaries (see
[PAPER §IX](../PAPER.md) for why). But **Alkhatlan & Kalita's 2018 survey** (arXiv:1812.09628,
read in full 2026-09-01) reports all four major ITS meta-analyses side by side, and one detail
changes how the headline should be read.

**Ma et al. 2014** — 107 effect sizes from 73 studies, the largest of the four:

| ITS compared against | d |
|---|---|
| Non-ITS computer-based instruction | **0.57** |
| Teacher-led / large-group instruction | **0.42** |
| Textbooks or workbooks | **0.35** |
| Small-group human instruction | **0.05** |
| ⭐ **Individualized human tutoring** | **−0.11** |

**ITSs beat every form of mass instruction and tie with a human tutor.** That is the strongest
version of the case for building one, and it is consistent with VanLehn's 0.76 vs 0.79.

**Kulik & Fletcher 2016** — 50 studies. 92% favoured the ITS; **median effect 0.66** across 39 of
them. That 0.66 is the number quoted everywhere as the high-water mark for ITS effectiveness.

⚠ **But in the same analysis, the effect on *standardized tests* was 0.13.**

**0.66 on the researchers' own measures; 0.13 on an external one.** That is not a footnote — it
is a fivefold collapse, and it means the field's most optimistic headline rests on locally
constructed outcomes.

**This is the fifth independent instance of the same pattern in this knowledge base**, and at
this point it should be treated as a law rather than a curiosity:

| Study | Proximal measure | Distal measure |
|---|---|---|
| Kulik & Fletcher 2016 | **0.66** own measures | **0.13** standardized tests |
| [Tutor CoPilot](../systems/tutor-copilot.md) | **+4 p.p.** exit tickets | **null** end-of-year MAP |
| [CycleTalk](../systems/cyclepad-cycletalk.md) | **+0.35 SD** concept test | **null** both design exercises |
| [Andes](../systems/andes.md) | **+1.21** drawings, +0.69 variables | **−0.08** answers |
| [Bastani](../evidence/bastani-2025-harm.md) | **+48%** while assisted | **−17%** unassisted exam |

**Whatever we measure close to the tutor will look good.** Our own evaluation has to lead with a
distal, unassisted, ideally externally-validated outcome, and we should expect it to be roughly a
fifth the size of whatever the in-app numbers say.
→ [concept inventories](../evaluation/concept-inventories.md),
[behavioral evaluation](../evaluation/behavioral-evaluation.md)

**One more thing the survey pins down:** VanLehn's famous numbers rest on **10 comparisons drawn
from 28 evaluation studies**, 1975–2010. The most-cited effect sizes in this field come from a
very small evidence base.

**Steenbergen-Hu & Cooper 2013** (K-12 maths, 26 reports) adds two moderators worth knowing:
**no significant effect for short-duration use**, with effects appearing only at a **full school
year or longer** — and effects **larger for general students than for low achievers**, which cuts
against the intuition that a tutor helps the struggling most.

## Why this is uncomfortable for our project

**A chat interface is not obviously step-based.**

A student who types "I'm stuck on 4b," reads three paragraphs, and types "oh ok thanks" has
externalized almost nothing. That's answer-based tutoring — the d ≈ 0.3 tier — with better
prose.

[Andes](../systems/andes.md) got its results by making students enter vectors, coordinate
systems, variable definitions, and equations, with feedback after each. That is a
*structured problem-solving surface*, not a chat window.

**The design implication is uncomfortable and should be argued about explicitly by the
team:** the most-evidenced design in the history of this field is not a chatbot. If we build
a chat interface because it's what LLMs make easy, we are choosing the weaker interaction
granularity for implementation convenience.

A defensible synthesis: a **structured solving surface** where the student enters steps,
with conversational help alongside — the LLM providing what Andes couldn't (natural
language understanding of a confused question), while the interface provides what chat
can't (mandatory externalization).

## Open questions

- [ ] **Still not read in full.** Two independent attempts failed: the paper is closed at the
      publisher with no repository copy, the ASU faculty copy moved behind Cloudflare Access,
      and the Internet Archive was down during both attempts. **A confirmed-good Wayback URL
      exists** — retry `https://web.archive.org/web/20240802132649id_/https://www.public.asu.edu/~kvanlehn/Stringent/PDF/EffectivenessOfTutoring_Vanlehn.pdf`
      when IA recovers, or use the **PSU library proxy**, which is the fast path.
- [ ] Still genuinely unknown and **not to be filled from secondary sources**: VanLehn's
      per-condition study counts and confidence intervals.
- [ ] Has anyone re-run this analysis including LLM-era systems?
- [ ] What exactly counts as a "step" in a thermodynamics problem?
      → [knowledge components](knowledge-components.md),
      [our skill graph](../../research/domain/skill-graph-draft.md)
- [ ] Why do substep systems underperform? The answer probably constrains our hint ladder
      depth. → [Socratic tutoring](socratic-tutoring.md)

## Connects to

- [Bloom's 2 sigma](blooms-two-sigma.md) — the claim this corrects
- [Andes](../systems/andes.md) — the exemplar step-based physics system
- [knowledge components](knowledge-components.md) — what a step is made of
- [Kestin 2025](../evidence/kestin-2025-rct.md) — the modern result that has to be read
  against these baselines

## Sources

- [Alkhatlan & Kalita (2018), "Intelligent Tutoring Systems: A Comprehensive Historical Survey with Recent Developments," arXiv:1812.09628](https://arxiv.org/pdf/1812.09628) `[read — full text, 31 pp., 2026-09-01]` — **the source for the Ma et al., Kulik & Fletcher and Steenbergen-Hu figures above.** ⚠ Secondhand: these are the survey's report of those meta-analyses, not our read of the primaries, which remain blocked.

- [VanLehn (2011), Educational Psychologist — ERIC record](https://eric.ed.gov/?id=EJ946764) `[skimmed]`
- [Semantic Scholar entry with PDF](https://www.semanticscholar.org/paper/The-Relative-Effectiveness-of-Human-Tutoring,-and-VanLehn/3b924661db089b3511465ae48e6400e20a1dd232) `[found]`
- [Intelligent Tutoring Systems: A Comprehensive Historical Survey, arXiv:1812.09628](https://arxiv.org/pdf/1812.09628) `[found]` — useful context
