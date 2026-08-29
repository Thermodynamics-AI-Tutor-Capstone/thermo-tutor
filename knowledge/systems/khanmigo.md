# Khanmigo

**Type:** system
**One line:** Khan Academy's LLM tutor — the largest real-world deployment, and the source
of the field's two most important practical lessons.
**Why we care:** Khan Academy publishes candidly about what didn't work. Their two lessons
should shape our architecture and our success criteria respectively.

## Lesson 1 — LLMs are unfit for math out of the box

Khan Academy's own account: generative AI "generates a probable next number rather than
executing a correct calculation."

Their response was architectural, not prompt-based. They built a **separate dedicated math
agent** that verifies calculations and checks mathematical expressions in real time before
a response reaches a student, and they track **math error rate as a guardrail metric** —
i.e. a number that must not get worse, monitored continuously in production.

Both of those generalize directly:
- A separate verification component, not a better prompt
- A named guardrail metric with a threshold, tracked over time

→ [grounding and verification](../concepts/grounding-and-verification.md),
[property data tools](../domain/property-data-tools.md)

## Lesson 2 — engagement is the real failure mode

From a two-year school study (2026), the finding that should reset our expectations:

- **96%** of students tried Khanmigo at least once
- The median student messaged it on only **a third of the days they practiced**
- And in only **17% of practice sessions**

Access was nearly universal. Engagement was thin. Students using Khan Academy still made
faster math gains than comparison — but **the tutor itself was largely unused.**

Full detail: [Khanmigo engagement study](../evidence/khanmigo-engagement-2026.md).

This is the largest, best-resourced, most professionally-designed LLM tutor deployment in
existence, backed by a beloved brand, given to students free. **It lost on engagement.**

Any plan of ours that assumes students will use the thing we build is contradicted by the
best available evidence.

## Scale

Khanmigo and Duolingo's Max Tutor collectively serve **50M+ active learners** as of 2026,
in both cases shifting from reactive assistants toward proactive agents — which is itself a
response to the engagement problem.

## Open questions

- [ ] What is the math agent, technically? Symbolic? A second model? A verifier?
- [ ] What does Khan's guardrail metric dashboard actually track?
- [ ] What does the "Khanmigo Tutor Agent" proactive version do differently, and did
      engagement improve?
- [ ] Who *are* the students in the 17%? (If it's the already-high-performing, see
      [equity](../practice/equity.md).)

## Connects to

- [Khanmigo engagement study](../evidence/khanmigo-engagement-2026.md) — the numbers in full
- [engagement decay](../concepts/engagement-decay.md) — the general problem
- [grounding and verification](../concepts/grounding-and-verification.md) — the math agent
- [equity](../practice/equity.md) — who the 17% probably are

## Sources

- [Khan Academy blog, "How Khan Academy Is Building a Better AI Tutor: Our Most Recent Learnings"](https://blog.khanacademy.org/how-khan-academy-is-building-a-better-ai-tutor-our-most-recent-learnings/) `[skimmed]` — unusually candid practitioner writeup
- [AI Tutoring with Khanmigo in a Two-Year School Experiment (EdWorkingPapers, 2026)](https://edworkingpapers.com/sites/default/files/ai26-1551.pdf) `[skimmed]`
- [Chalkbeat coverage of the engagement study](https://www.chalkbeat.org/2026/08/25/ai-tutoring-students-khanmigo-khan-academy-engagement-study/) `[skimmed]`
