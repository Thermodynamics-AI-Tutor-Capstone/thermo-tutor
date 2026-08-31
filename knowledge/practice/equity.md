# Equity

**Type:** practice
**One line:** Usage of voluntary AI tutors concentrates in a small minority — but the best
university-level evidence says that minority is the **least-prepared** students, not the
most-advantaged.
**Why we care:** We had this backwards. The equity case for our project is stronger than we
thought, and the mechanism is not the one we assumed.

> **Substantially corrected 2026-08-31** after reading the
> [KAIST deployment study](../evidence/kaist-vta-2025.md) in full. This node previously
> asserted that voluntary-tool power users "skew already-high-performing and higher-income,"
> sourced from a consultancy blog. The best available university data says the opposite.

## What is solid: usage concentrates

The concentration is real and large. From KAIST — 477 graduate students, 14 weeks, voluntary:

| Group | Usage | Students | Share of all interactions |
|---|---|---|---|
| A | ≥100 times | 6 (**1.3%**) | **30%** |
| A+B | ≥18 times | 59 (**12.5%**) | **78%** |
| E | **never used it** | **237 (50%)** | 0% |

Half the class never engaged at all. An eighth of the class produced nearly four-fifths of
the traffic. Consistent with
[Khanmigo](../evidence/khanmigo-engagement-2026.md) (96% tried it; median use in 17% of
practice sessions).

## What was wrong: *who* those users are

At KAIST, average interactions by **prior coding experience**:

| Prior experience | Avg. interactions |
|---|---|
| **None** | **62.2** |
| Beginner | 11.2 |
| Intermediate | 5.5 |
| Advanced | 4.5 |

**A 14× gap, running the opposite way from our earlier assumption.** The same pattern held
for prior ML knowledge.

And the plausible mechanism, measured in the same study: **58% of students had previously
refrained from asking a human instructor** a question out of discomfort, fear of burdening
them, or fear of seeming silly. Those students used the VTA **13.2** times on average versus
**7.8** for students who had never hesitated — and their comfort scores rose over the term.

**The AI tutor's distinctive advantage is that it costs nothing socially to ask.** That
advantage accrues precisely to students who are struggling, intimidated, or on the outside of
the informal networks that carry help.

Supporting signal: the same students asked the VTA **four times as many conceptual questions**
(35% vs 8.3%) as students had asked human TAs the prior year. Confusion that was going
unvoiced got voiced.

**Caveat, held honestly.** These are graduate students in Korea, self-selecting into a
programming course. Different populations may behave differently, and the K-12-flavored
"5% already-advantaged power users" pattern may well hold there. But for *our* setting —
university engineering — KAIST is the better evidence, and it is encouraging.

## The converging counter-case

[Tutor CoPilot](../systems/tutor-copilot.md) found its **largest effect (+9%) for students of
the least-skilled tutors**. Raising the floor is an equalizing move.

And there is a hint in the literature that **proactive** tutoring narrows the gap between
lower- and higher-performing students — plausible because it removes the initiation
requirement entirely.

**Three independent findings now point the same way:** the AI's equity contribution comes
from *lowering the cost of asking* — socially (KAIST), in tutor quality (Tutor CoPilot), and
in initiative required (proactivity). The residual risk is not who benefits from asking; it
is **the 50% who never ask at all.** That is the population our design has to reach, and
nothing in this literature has reached it.

## What follows for our design

**1. Measure it, don't assume it.** Correlate usage with incoming performance from the first
week. If our users are the top quartile, we're widening the gap and should say so — that is a
publishable finding and an honest one.

**2. Proactivity is an equity feature, not just an engagement feature.** A tutor that
initiates — "you've got a problem set due Thursday and your entropy-generation work has been
shaky" — removes the initiation requirement that filters out the students who need it most.
→ [engagement decay](../concepts/engagement-decay.md), [spaced repetition](../concepts/spaced-repetition.md)

**3. The hybrid frame is the equity-strongest option on the table.** A
[Tutor CoPilot for thermodynamics office hours](../systems/tutor-copilot.md) reaches students
who show up to office hours — a broader and different population than students who adopt an
optional app.

**4. Watch the friction.** Every login, token paste, and setup step filters. It filters
hardest on students with the least time and the least tech confidence.
→ [Canvas access](../../admin/canvas-access.md) — the "generate your own API token" fallback
is an equity problem as well as a UX one.

**5. The guardrails have a distributional cost.** A tutor that makes you work is a harder sell
to a student working 20 hours a week than to one who isn't. The
[productive-failure budget](../concepts/productive-failure.md) may not be the same for every
student, and "adaptive to individual needs" — which our brief asks for — might legitimately
mean adaptive here too.

## Open questions

- [ ] Where does the "already-advantaged 5%" claim originate, and in what population? It is
      contradicted by KAIST at university level. **Trace it before citing either way.**
- [ ] Does the least-prepared-use-it-most pattern hold in *undergraduate* engineering, or is
      it specific to graduate students who know they are behind?
- [ ] **Who are the 50% who never engage, and why?** KAIST did not investigate. This is now
      the sharpest open equity question in the field, and one a small interview study could
      actually answer. → [interview protocol](../../research/student-interviews/protocol-draft.md)
- [ ] Does a course-specific tutor distribute more evenly than a general one? Untested and
      directly answerable by us.
- [ ] Would a proactive tutor be experienced as helpful or as nagging? **Ask students**
      → [interview protocol](../../research/student-interviews/protocol-draft.md)
- [ ] Should the hint budget adapt to student circumstances, and is that fair or patronizing?

## Connects to

- [engagement decay](../concepts/engagement-decay.md) — the same phenomenon, different lens
- [Khanmigo engagement](../evidence/khanmigo-engagement-2026.md) — the numbers
- [Tutor CoPilot](../systems/tutor-copilot.md) — the design that raises the floor
- [productive failure](../concepts/productive-failure.md) — guardrails have a distributional cost

## Sources

- [Kweon et al., KAIST VTA deployment, arXiv:2506.17363](https://arxiv.org/abs/2506.17363) `[read]` — **the primary correction**; see [our node](../evidence/kaist-vta-2025.md)
- [Gray DI, "Why Your AI Tutor Might Be Widening the Achievement Gap"](https://www.graydi.us/blog/gray-insights/why-your-ai-tutor-might-be-widening-the-achievement-gap) `[skimmed]` — source of the "already-advantaged 5%" claim. **Consultancy blog, contradicted by KAIST at university level. Do not cite without a primary source.**
- [Tutor CoPilot, arXiv:2410.03017](https://arxiv.org/pdf/2410.03017) `[skimmed]` — the +9% for weak tutors
- [Khanmigo two-year study](https://edworkingpapers.com/sites/default/files/ai26-1551.pdf) `[skimmed]`
- [Improving Hybrid Human-AI Tutoring by Differentiating Human Tutor Roles Based on Student Needs, arXiv:2605.11155](https://arxiv.org/pdf/2605.11155) `[found]`
