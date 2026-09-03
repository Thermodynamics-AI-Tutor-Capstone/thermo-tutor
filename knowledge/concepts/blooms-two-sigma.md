# Bloom's 2 Sigma Problem

**Type:** concept
**One line:** Benjamin Bloom's 1984 claim that one-to-one tutoring moves the average
student two standard deviations — the foundational myth of AI tutoring, and substantially
overstated.
**Why we care:** It is the implicit promise behind our project brief and behind nearly every
AI tutoring pitch. We should know it doesn't hold before we quote it.

## The claim

Bloom (1984) reported that students taught one-to-one with mastery learning performed
**two standard deviations** better than conventionally-taught students — moving the average
student to roughly the **98th percentile**.

The "problem" was framed as an engineering challenge: one-to-one tutoring works
spectacularly and doesn't scale. Find something that does.

That framing built the intelligent tutoring systems field, and forty years later it is the
opening slide of essentially every AI tutoring deck.

## Why it doesn't hold

[VanLehn's 2011 review](vanlehn-2011.md) of experiments from 1975–2010 found human tutoring
at **d = 0.79**. Large and educationally meaningful — and not 2.0.

## ⭐⭐ It wasn't the tutoring. It was the mastery threshold.

**This node used to list "plausible reasons for the gap." We no longer have to speculate** —
[VanLehn read Bloom's underlying dissertations and reported the mechanism](vanlehn-2011.md),
and we have now read VanLehn in full (2026-09-03).

Of the six studies Bloom summarised — from the dissertations of **Anania (1981)** and
**Burke (1983)** — only Anania's Experiment 3 was actually one-on-one. The other five had each
tutor working with **groups of three**. Anania Exp. 3 gave **d = 1.95**.

Three things Bloom's readers have assumed for forty years, all wrong:

| Assumption | What the original sources say |
|---|---|
| The tutors were expert "super tutors" | **"Undergraduate education majors"** who *"met the experimenter each day for one week before the instruction began"* |
| The comparison was tutoring vs. classroom | There was a **third arm: mastery learning in an ordinary classroom**, which scored **~1.0 SD** over the plain control **with no tutor** |
| The conditions differed only in tutoring | ⭐ **The mastery threshold was 90% for tutees and 80% for the classroom mastery condition** (Anania 1981, pp. 44–45). The plain control had no threshold at all |

> **"That is, the tutors were holding their students to a higher standard of mastery than the
> classroom teachers. This alone could account for the advantage of tutoring (2.0 effect size)
> over mastery learning (1.0 effect size)."** — VanLehn 2011

> **"So the Bloom (1984) article is, as Bloom intended it to be, a demonstration of the power of
> mastery learning rather than a demonstration of the effectiveness of human tutoring."**

**The second 2-sigma study in the literature is a small-sample artefact.** Evens & Michael's
first baroreceptor experiment gave d = 1.95; re-run with more subjects it gave **0.52**. The
tutees scored about the same both times — the **control** moved: N = 9 with a mean gain of
**0.33** the first time, N = 28 with **1.54** the second, and a third comparable control (N = 33)
at **2.0**.

⚠ **After those two, the next highest human-tutoring effect size in VanLehn's whole review is
0.82.** Two outliers, then a cliff.

## ⭐ The finding hiding inside the debunking

**Mastery learning produced ~1.0 SD in an ordinary classroom, with no tutor.** That is larger
than [step-based ITS against no tutoring](vanlehn-2011.md) and it is a *policy*, not a
technology: set a threshold, make students restudy and retest until they clear it, then let them
advance.

**It is also nearly free to implement in software, and it is the one component of the 2-sigma
result that survived scrutiny.** If our tutor adopts one thing from Bloom, it should be the
threshold — not the conversation. → [knowledge tracing](knowledge-tracing.md),
[spaced repetition](spaced-repetition.md)

## Why this matters to us specifically

**It resets the target.** If human tutoring is d ≈ 0.79 and
[step-based ITS from the 1990s already achieved d ≈ 0.76](vanlehn-2011.md), then the
headroom for an LLM tutor over a *well-built classical tutor* is small. The honest pitch is
not "2 sigma at scale." It's "the tutoring effect, available at 2am, in the student's own
course."

**It's a credibility test.** An advisor or reviewer who knows this literature will notice a
2-sigma citation and discount everything after it. Citing d = 0.79 and the step-based
finding signals we've read past the marketing.

**It reframes the actual contribution.** The interesting question isn't "can we approach
human tutoring." It's "can we deliver a meaningful fraction of it to students who currently
get *no* tutoring at 11pm the night before a problem set is due?" That's a coverage
argument, not an efficacy argument, and it's a much more defensible one.

## Open questions

- [x] ~~What did Bloom's actual mastery-learning condition involve? (The mastery component may
      be doing more work than the one-to-one component.)~~ **Answered 2026-09-03 via VanLehn's
      primary: 90% vs 80% vs no threshold. The mastery component is doing most of the work, and
      it is a design finding.**
- [ ] Read Bloom (1984) directly rather than through citations — and Anania (1981) Exp. 3, which
      is where the 1.95 and the threshold detail actually live. Both are still `[found]`.
- [ ] Are there modern well-controlled estimates of human tutoring effects in university
      STEM specifically?
- [ ] **Has anyone tested a mastery threshold inside an LLM tutor?** Nothing in this base does.
      Given the size of the classroom mastery-learning effect, that is a conspicuous gap.

## Connects to

- [VanLehn 2011](vanlehn-2011.md) — the correction
- [Kestin 2025](../evidence/kestin-2025-rct.md) — the modern claim that must be read
  against d = 0.79
- [our open questions](../../docs/03-open-questions.md) — what counts as success (C3)

## Sources

- Bloom, B. S. (1984). "The 2 Sigma Problem: The Search for Methods of Group Instruction as Effective as One-to-One Tutoring." *Educational Researcher*, 13(6), 4–16. `[found]`
- [VanLehn (2011), *Educational Psychologist* 46(4), 197–221](https://doi.org/10.1080/00461520.2011.611369) `[read — full text, 25 pp., 2026-09-03]` — the empirical correction, and the source for the mastery-threshold dissection above. Local: `course-materials/papers/vanlehn-2011-relative-effectiveness.pdf`
- Anania, J. (1981). *The effects of quality of instruction on the cognitive and affective learning of students.* Doctoral dissertation, University of Chicago. `[found]` — Experiment 3 is the only one-on-one study behind the 2-sigma claim; the 90%/80% thresholds are on pp. 44–45
- Burke, A. J. (1983). *Student's potential for learning contrasted under tutorial and group approaches to instruction.* Doctoral dissertation, University of Chicago. `[found]` — the other five Bloom studies, all one-tutor-to-three-students
