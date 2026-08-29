# Tutor CoPilot

**Type:** system
**One line:** A Stanford system that coaches the *human tutor* in real time instead of
tutoring the student — and got its largest effect for the weakest tutors.
**Why we care:** It is the best-evidenced positive result in this knowledge base per dollar
of engineering, and it suggests a smaller, more tractable version of our project that
nobody has built for engineering.

## The inversion

Every other system in [`systems/`](.) puts the AI between the student and the material.
Tutor CoPilot puts the AI **behind the human tutor**, suggesting how to respond to a
student's mistake while a live session is happening.

Built by Stanford's **EduNLP Lab**. Suggestions are **educator-curated**, not free
generation. Open source, embeddable in any tutoring platform. Piloted with **FEV Tutor**.

## Results

RCT: ~**900 tutors**, ~**1,800** elementary and secondary students in a large southern US
school district.

- Students of tutors using Tutor CoPilot were **4 percentage points** more likely to
  master topics
- **+9%** for students of the **least-skilled** tutors
- Tutors using it **asked more guiding questions** and **gave away fewer answers**

## Why this is the most interesting result for a capstone team

Three reasons:

**1. It raises the floor, which is where the room is.** The effect concentrated among weak
tutors. Excellent tutors didn't need it. Most tutoring at a large university is delivered
by undergraduate and graduate TAs with variable training — that is exactly the population
where this works.

**2. It sidesteps the field's fatal problem.** Every student-facing tutor in this knowledge
base hits the [engagement wall](../concepts/engagement-decay.md) — 17% session usage, 5%
power users. **Tutor CoPilot has no engagement problem, because the user is a tutor who is
already at work.** Adoption is a staffing decision, not a motivation problem.

**3. It changes the pedagogy problem into a tractable one.** The system doesn't have to
hold a Socratic line against a student demanding answers — a human does that, better, with
the AI feeding them better moves. The
[Socratic subversion problem](../concepts/socratic-tutoring.md) largely evaporates.

## The version nobody has built

**A Tutor CoPilot for engineering office hours and recitations.** Suggestions to a
thermodynamics TA, grounded in the course's actual problems and misconception catalogue,
at the moment a student is stuck.

Compared to a standalone tutor it is: smaller in scope, better evidenced in prior work,
free of the engagement problem, easier to get instructor buy-in for, and — as far as this
sweep found — **undone in engineering**.

It is not what our brief asked for, and it should be on the table as an explicit
alternative or as a second arm. See
[open questions C4](../../docs/03-open-questions.md).

## Open questions

- [ ] Does the effect hold for university-level content, or is it K-12-bound?
- [ ] What do the educator-curated suggestions look like? Is the library public?
- [ ] What's the tutor-side UX? Latency requirements in a live session?
- [ ] Would PSU thermo TAs accept real-time AI suggestions? (Ask them.)

## Connects to

- [engagement decay](../concepts/engagement-decay.md) — the problem this design avoids
- [Socratic tutoring](../concepts/socratic-tutoring.md) — the problem a human solves better
- [faculty adoption](../practice/faculty-adoption.md) — TA acceptance is the adoption path
- [our open questions](../../docs/03-open-questions.md) — informs the comparison-condition
  decision

## Sources

- [Tutor CoPilot: A Human-AI Approach for Scaling Real-Time Expertise, arXiv:2410.03017](https://arxiv.org/pdf/2410.03017) `[skimmed]` — the paper
- [Stanford EduNLP Lab project page](https://edunlp.stanford.edu/projects/tutor-copilot) `[found]`
- [Stanford NSSA, "Tutor CoPilot Transforms Real-Time Tutoring"](https://nssa.stanford.edu/news/stanford-us-tutor-copilot-transforms-real-time-tutoring-ai-driven-expert-guidance) `[skimmed]`
- [K-12 Dive, "How AI can improve tutor effectiveness"](https://www.k12dive.com/news/ai-tutor-effectiveness-stanford-university/728980/) `[skimmed]`
