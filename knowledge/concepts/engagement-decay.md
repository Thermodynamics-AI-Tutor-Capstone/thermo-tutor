# Engagement Decay

**Type:** concept
**One line:** The field's actual failure mode — students try an AI tutor, then stop using
it, and the ones who keep using it are the ones who needed it least.
**Why we care:** This is where the best-funded, best-designed deployment in the world lost.
Our project will hit it, and almost nothing in our brief currently addresses it.

> **Substantially revised 2026-08-31** after full reads of the KAIST, CS50, and Bastani
> papers. Two of this node's original hypotheses turn out to be wrong.

## The numbers, from three real deployments

**[Khanmigo](../evidence/khanmigo-engagement-2026.md)** (K-12, two-year study):
- **96%** tried it at least once
- Median student used it on a third of practice days, and in only **17% of practice sessions**

**[KAIST](../evidence/kaist-vta-2025.md)** (477 graduate students, 14 weeks, voluntary):
- **237 of 472 (50%) never used it once**
- **6 students (1.3%) produced 30%** of all interactions; 12.5% produced **78%**

**[CS50](../systems/cs50-duck.md)** (~500 on-campus students, end-of-term survey):
- **28% "constantly," 50% "frequently," 19% "infrequently", only 3% never**

**CS50's engagement profile is dramatically better than the other two, and that difference is
the most useful thing in this node.**

## Why CS50 succeeded where the others didn't

Five differences, all of them design or policy choices rather than luck:

1. **Course policy pushed students to it.** CS50 *encouraged* its own tools and **limited use
   of ChatGPT, Copilot, and Bing**. The tool wasn't competing with a better free alternative.
2. **It lived where the work happened** — inside VS Code via an extension, not on a separate
   site requiring a separate login. → [LMS integration](../practice/lms-integration.md)
3. **Deliberate scarcity.** Usage throttling via "hearts": 10 to start, one regained every
   three minutes, one spent per interaction. Framed as pedagogy, not just cost control —
   *"promotes thoughtful interaction... foster independent problem-solving skills and the
   ability to formulate precise questions."* Students asked for it to be relaxed; the team
   declined.
4. **Anthropomorphism.** A lovable duck. *"Love love loved the duck. We're friends now."*
   KAIST found the same effect independently: the 13% of conversations containing social
   cues came from students averaging **27.8** interactions versus **11.4** for everyone else.
5. **A large, self-selected, highly motivated population** — the honest caveat. CS50's online
   cohort is not a required course's cohort.

## Two hypotheses this node had wrong

**Wrong #1: "Guardrails cause churn."** [Bastani](../evidence/bastani-2025-harm.md) measured
the opposite. The guardrailed tutor got **more** messages per problem than the unguarded one,
the gap **widened** over four sessions, and students spent **13% more time** with it.
Superficial "just give me the answer" openers fell from 42% to **37%** with the guardrailed
tool while *rising* from 56% to **67%** with the unguarded one.

Students got lazier with the tool that gave answers and more skilled with the tool that
didn't. **Guardrails are not a friction that repels; they are a structure students learn.**

**Wrong #2: "The power users are the already-advantaged."** At KAIST, students with **no
prior coding experience averaged 62.2 interactions** against **4.5** for advanced students.
See [equity](../practice/equity.md).

## The real churn mechanism: disappointed low-frequency users

KAIST's survey data separates two opposite trends that the aggregate hides:

| Group | Helpfulness, pre → post |
|---|---|
| High-frequency users (A/B/C) | **improved significantly** (p = 0.043) |
| **Group D (<5 uses)** | **3.72 → 3.26** |

Group D also rated *human* TAs highest (4.06). They arrived with high expectations, tried it
about twice, weren't impressed, and left.

**The critical window is the first two or three interactions.** Students who get past it
grow *more* positive with use. Students who don't, don't come back. That is a much more
actionable target than "engagement" in the abstract — it makes onboarding and first-session
quality the highest-leverage surface in the product.

## The substitution effect nobody discusses

CS50's forum traffic **collapsed** after the Duck was fully deployed:

| Term | Questions per student on Ed (the human forum) |
|---|---|
| Fall 2022 | 0.89 |
| Summer 2023 | 1.1 |
| **Fall 2023** | **0.28** |

A ~75% drop. The team's reading is substitution — students moved to synchronous Duck
interaction and escalated only hard questions to humans.

**This is not obviously good.** Fewer questions reaching human staff means less instructor
visibility into where students are stuck, and the AI becomes the only witness to student
confusion. That argues strongly for **logging and surfacing aggregate confusion to the
instructor** — which is precisely what [Stan's question mining](../systems/stan-udel.md) does
and what [KAIST found](../evidence/kaist-vta-2025.md) students will use an AI for four times
more than a human (35% vs 8.3% conceptual questions).

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

1. **It didn't help the first two times.** Now the best-evidenced cause (KAIST Group D).
2. **Friction.** Another login, another tab, another context switch, at 11pm. ChatGPT is one
   tab away and already open. CS50 beat this by living inside VS Code.
   → [competitive teardown](../../research/competitive-teardown/README.md)
3. **A better free alternative exists.** Unless course policy or genuine course-specific
   capability closes the gap. → [PSU AI landscape](../practice/psu-ai-landscape.md)
4. **No felt progress.** Nothing accumulates; every session starts cold. *Fixable by our
   design* — a visible mastery model is exactly a progress signal.
5. ~~The guardrails~~ — **disproven**, see above.

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

- [ ] What *is* a good voluntary return rate? We now have a range: **50% never-users
      (KAIST) to 3% never-users (CS50)**. The spread is design and policy, not luck.
- [ ] Can we reproduce CS50's throttling result? A hint budget that *increases* perceived
      value is a striking claim and directly testable.
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

- [Kweon et al., KAIST VTA deployment, arXiv:2506.17363](https://arxiv.org/abs/2506.17363) `[read]` — the usage distribution and Group D finding
- [Liu et al., "Teaching CS50 with AI" (SIGCSE 2024)](https://cs.harvard.edu/malan/publications/V1fp0567-liu.pdf) `[read]` — hearts, engagement survey, Ed substitution
- [Bastani et al., PNAS 2025](https://www.pnas.org/doi/10.1073/pnas.2422633122) `[read]` — guardrails increased engagement
- [AI Tutoring with Khanmigo in a Two-Year School Experiment (2026)](https://edworkingpapers.com/sites/default/files/ai26-1551.pdf) `[skimmed]`
- [Chalkbeat, "Students rarely engaged with Khan Academy's AI-powered tutor"](https://www.chalkbeat.org/2026/08/25/ai-tutoring-students-khanmigo-khan-academy-engagement-study/) `[skimmed]`
- [Gray DI, "Why Your AI Tutor Might Be Widening the Achievement Gap"](https://www.graydi.us/blog/gray-insights/why-your-ai-tutor-might-be-widening-the-achievement-gap) `[skimmed]` — the 5% figure
