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

- [VanLehn (2011), Educational Psychologist — ERIC record](https://eric.ed.gov/?id=EJ946764) `[skimmed]`
- [Semantic Scholar entry with PDF](https://www.semanticscholar.org/paper/The-Relative-Effectiveness-of-Human-Tutoring,-and-VanLehn/3b924661db089b3511465ae48e6400e20a1dd232) `[found]`
- [Intelligent Tutoring Systems: A Comprehensive Historical Survey, arXiv:1812.09628](https://arxiv.org/pdf/1812.09628) `[found]` — useful context
