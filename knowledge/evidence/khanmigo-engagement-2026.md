# Khanmigo engagement study (2026)

**Type:** study (two-year observational)
**One line:** 96% of students tried Khanmigo; the median student used it in **17% of
practice sessions**.
**Why we care:** The best-funded, best-designed AI tutor deployment in the world, given free
to students, was largely ignored. Our project will face the same problem and currently has
no plan for it.

## The numbers

Two-year school experiment (EdWorkingPapers, 2026):

- **96%** of students tried Khanmigo at least once
- The median student messaged it on only **a third of the days they practiced**
- And in only **17% of practice sessions**
- Students using Khan Academy still made **faster math gains** than the comparison group

The researchers' phrasing: *"Access was nearly universal but engagement was thin."*

Note the last bullet carefully. Khan Academy worked. **Khanmigo — the AI tutor layered on
top — was mostly unused.** The gains are attributable to the platform, not the chatbot.

## Why this is the most important number in the knowledge base

Every other finding here is conditional on students using the thing.

- [Kestin's 2× gains](kestin-2025-rct.md) — students were *assigned* to use the tutor
- [Bastani's arms](bastani-2025-harm.md) — structured practice sessions
- [Tutor CoPilot](../systems/tutor-copilot.md) — the user is a tutor at work

Khanmigo measured **voluntary** use at scale and found 17%.

If our tutor achieves Kestin-level quality and Khanmigo-level engagement, the population
effect is roughly 17% of an effect. That arithmetic should be in our project plan.

## What it doesn't tell us

- **Who** the 17% are. If they're already-high-performing students, this is also an
  [equity](../practice/equity.md) finding — and the 5% power-user literature suggests they
  are.
- **Why** students stopped. Friction? Guardrails? It didn't help? Nobody asked, as far as
  this sweep found.
- Whether a **course-specific** tutor differs from a general one. Khanmigo covers all of
  Khan Academy; ours would know the student's actual assignment. Plausibly a real
  difference — and completely untested.

That last point is the most useful thing here: **it's a gap we're positioned to fill.**
Nobody has published voluntary week-by-week return rates for a course-specific university
tutor. If we instrument for it and report it honestly, that's a contribution regardless of
whether our learning effect is detectable.
→ [engagement decay](../concepts/engagement-decay.md)

## Open questions

- [ ] Read the full working paper. Sample, setting, how "session" was defined.
- [ ] Is there a usage *curve* over the two years, or only aggregates?
- [ ] Did engagement correlate with prior achievement?
- [ ] Has Khan Academy's shift to a proactive "Tutor Agent" changed these numbers?

## Connects to

- [engagement decay](../concepts/engagement-decay.md) — the general problem
- [Khanmigo](../systems/khanmigo.md) — the system
- [equity](../practice/equity.md) — who actually uses voluntary tools
- [Tutor CoPilot](../systems/tutor-copilot.md) — a design that sidesteps this entirely

## Sources

- [AI Tutoring with Khanmigo in a Two-Year School Experiment (EdWorkingPapers, 2026)](https://edworkingpapers.com/sites/default/files/ai26-1551.pdf) `[skimmed]` — **priority read**
- [Chalkbeat, "Students rarely engaged with Khan Academy's AI-powered tutor Khanmigo, study finds"](https://www.chalkbeat.org/2026/08/25/ai-tutoring-students-khanmigo-khan-academy-engagement-study/) `[skimmed]`
