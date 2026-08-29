# Equity

**Type:** practice
**One line:** Roughly 5% of students account for most of the benefit from voluntary digital
learning tools, and that 5% skews already-high-performing and higher-income.
**Why we care:** A voluntary tutor can widen the gap it was built to close, and our current
plan is for a voluntary tutor.

## The concentration problem

Research on voluntary digital learning tools consistently finds that a small, highly
motivated subset uses them as intended and captures most of the benefit — on the order of
**5%** of the student population. That group is disproportionately **already
high-performing** and **from higher-income backgrounds**.

Consistent with [Khanmigo's engagement data](../evidence/khanmigo-engagement-2026.md): 96%
tried it, median use in **17% of practice sessions**. Somebody is using it a lot. It probably
isn't the student who's failing.

**The mechanism is not mysterious.** Using an optional tutor well requires knowing you're
confused, believing help exists, having the time and the metacognitive habits to seek it, and
tolerating a tool that makes you work. Every one of those correlates with prior achievement
and with not having a job.

## The other direction

There is a real counter-case. [Tutor CoPilot](../systems/tutor-copilot.md) — a hybrid
human-AI design — found its **largest effect (+9%) for students of the least-skilled
tutors**. Raising the floor on instruction quality is an equalizing move.

And there is a hint in the literature that **proactive** tutoring narrows the gap between
lower- and higher-performing students. That's plausible for exactly the reason above: it
removes the requirement that the student initiate.

**The pattern across both:** interventions that require student initiative concentrate
benefit at the top. Interventions delivered *to* students, or *through* an instructor,
distribute it more evenly.

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

- [ ] Where does the 5% figure originate? **Trace it to a primary source — currently sourced
      from a consultancy blog and needs verification before use.**
- [ ] Does the concentration pattern hold in university engineering specifically?
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

- [Gray DI, "Why Your AI Tutor Might Be Widening the Achievement Gap"](https://www.graydi.us/blog/gray-insights/why-your-ai-tutor-might-be-widening-the-achievement-gap) `[skimmed]` — the 5% figure. **Consultancy blog. Needs a primary source.**
- [Tutor CoPilot, arXiv:2410.03017](https://arxiv.org/pdf/2410.03017) `[skimmed]` — the +9% for weak tutors
- [Khanmigo two-year study](https://edworkingpapers.com/sites/default/files/ai26-1551.pdf) `[skimmed]`
- [Improving Hybrid Human-AI Tutoring by Differentiating Human Tutor Roles Based on Student Needs, arXiv:2605.11155](https://arxiv.org/pdf/2605.11155) `[found]`
