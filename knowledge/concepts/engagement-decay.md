# Engagement Decay

**Type:** concept
**One line:** The field's actual failure mode — students try an AI tutor, then stop using
it, and the ones who keep using it are the ones who needed it least.
**Why we care:** This is where the best-funded, best-designed deployment in the world lost.
Our project will hit it, and almost nothing in our brief currently addresses it.

## The numbers

**[Khanmigo](../evidence/khanmigo-engagement-2026.md)**, two-year school study:
- **96%** of students tried it at least once
- The median student messaged it on only **a third of the days they practiced**
- And in only **17% of practice sessions**

**[The power-user concentration](../practice/equity.md):** roughly **5%** of students account
for most of the benefit from voluntary digital learning tools — and that 5% is
disproportionately already-high-performing and higher-income.

Put together: near-universal access, thin engagement, and the engagement that exists is
concentrated in students who were going to be fine anyway.

## Why this deserves more attention than it gets

Almost every published evaluation of an AI tutor studies **mandatory or incentivized use**.
[Kestin's RCT](../evidence/kestin-2025-rct.md) assigned students to the tutor as coursework.
[Bastani's](../evidence/bastani-2025-harm.md) practice sessions were structured.
[Tutor CoPilot](../systems/tutor-copilot.md) sits inside a paid tutor's workflow.

So the literature is largely silent on the question that determines whether a voluntary tool
matters: **does anyone come back in week ten?**

The one large deployment that measured voluntary use found 17%.

## Why students stop

Hypotheses, mostly untested — and worth testing, since this is where the project actually
lives or dies:

1. **Friction.** Another login, another tab, another context switch, at 11pm. ChatGPT is one
   tab away and already open. → [competitive teardown](../../research/competitive-teardown/README.md)
2. **The guardrails.** A tutor that won't give answers is *less useful in the moment* than
   one that will. Students optimize for finishing the assignment.
   → [guardrails](guardrails.md)
3. **Frustration.** Socratic questioning of a student who wanted direction reads as
   obstruction. → [Socratic tutoring](socratic-tutoring.md)
4. **No felt progress.** Nothing accumulates; every session starts cold. This one is
   *fixable by our design* — a visible mastery model is exactly a progress signal.
5. **It didn't help the first time.** The single most likely cause and the least
   discussed.

## The tension with productive failure

[Productive failure](productive-failure.md) argues for withholding help. Engagement data says
students who don't get help leave.

**These are in direct conflict and the resolution is empirical.** The hint-ladder budget is
exactly the knob where they trade off, and nobody in this literature has published the right
setting. That makes it one of the few genuinely open questions our pilot could answer.

## What follows for our project

**Voluntary week-10 return rate should be a primary metric, not a footnote.**

Concretely, instrument from day one:
- Sessions per student per week, over the full term
- Time from a student's *first* session to their *last*
- The distribution — are we serving 5% heavily or 60% lightly?
- Correlation between usage and incoming performance (are we widening the gap?)
- Defection events: how often students escalate for answers, and whether escalation predicts
  churn

**And consider designs that don't have this problem.**
[Tutor CoPilot](../systems/tutor-copilot.md) has no engagement problem because its user is a
tutor already at work. Proactivity — a tutor that speaks first — is the other lead, and
almost entirely unexplored; the one hint in the literature is that proactive tutoring
narrows the gap between low- and high-performers.

## Open questions

- [ ] What *is* a good voluntary return rate? We have one data point (17%) and no baseline.
- [ ] Does a visible mastery model increase return? Directly testable.
- [ ] Does proactive outreach help, or is it just annoying?
- [ ] Who are the 17%, and are they the students who needed it?
- [ ] What would make a PSU thermo student come back in week ten? **Ask them**
      → [interview protocol](../../research/student-interviews/protocol-draft.md), Q17

## Connects to

- [Khanmigo engagement study](../evidence/khanmigo-engagement-2026.md) — the source numbers
- [equity](../practice/equity.md) — who the power users are
- [productive failure](productive-failure.md) — the design tension
- [Tutor CoPilot](../systems/tutor-copilot.md) — a design without this problem
- [guardrails](guardrails.md) — a plausible cause of churn

## Sources

- [AI Tutoring with Khanmigo in a Two-Year School Experiment (2026)](https://edworkingpapers.com/sites/default/files/ai26-1551.pdf) `[skimmed]`
- [Chalkbeat, "Students rarely engaged with Khan Academy's AI-powered tutor"](https://www.chalkbeat.org/2026/08/25/ai-tutoring-students-khanmigo-khan-academy-engagement-study/) `[skimmed]`
- [Gray DI, "Why Your AI Tutor Might Be Widening the Achievement Gap"](https://www.graydi.us/blog/gray-insights/why-your-ai-tutor-might-be-widening-the-achievement-gap) `[skimmed]` — the 5% figure
