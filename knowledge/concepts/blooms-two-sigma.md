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

Plausible reasons for the gap, in rough order of importance:
- Bloom's original studies were small, and conducted under conditions (mastery learning,
  hand-picked tutors, tightly-scoped content) that don't reflect ordinary tutoring
- The comparison condition was conventional instruction of the era, a lower bar than
  modern active learning
- Publication and selection effects across a small literature

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

- [ ] Read Bloom (1984) directly rather than through citations
- [ ] What did Bloom's actual mastery-learning condition involve? (The mastery component may
      be doing more work than the one-to-one component — which would be a design finding,
      not just a historical note.)
- [ ] Are there modern well-controlled estimates of human tutoring effects in university
      STEM specifically?

## Connects to

- [VanLehn 2011](vanlehn-2011.md) — the correction
- [Kestin 2025](../evidence/kestin-2025-rct.md) — the modern claim that must be read
  against d = 0.79
- [our open questions](../../docs/03-open-questions.md) — what counts as success (C3)

## Sources

- Bloom, B. S. (1984). "The 2 Sigma Problem: The Search for Methods of Group Instruction as Effective as One-to-One Tutoring." *Educational Researcher*, 13(6), 4–16. `[found]`
- [VanLehn (2011)](https://eric.ed.gov/?id=EJ946764) `[skimmed]` — the empirical correction
