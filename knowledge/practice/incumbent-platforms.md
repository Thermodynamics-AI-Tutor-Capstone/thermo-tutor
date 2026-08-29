# Incumbent Platforms

**Type:** practice
**One line:** Mastering Engineering, McGraw Hill Connect, WileyPLUS, and EES — what a
thermodynamics student is *actually* using, and the competitor nobody in the AI tutoring
literature benchmarks against.
**Why we care:** If we claim to improve on the status quo, the status quo is these, not
ChatGPT. They have a decade of adaptive-learning telemetry and they are already in the course.

## Who they are

**Pearson Mastering Engineering** — hint-based homework with graded steps and answer-specific
feedback. Note what that is: **step-based tutoring**, the design
[VanLehn found most effective](../concepts/vanlehn-2011.md) (d = 0.76). The incumbent already
has the interaction granularity that a chat tutor lacks.

**McGraw Hill Connect / SmartBook** — publisher of **Cengel & Boles**, the most common US
undergraduate thermodynamics text. Adaptive recall features that predate LLMs. McGraw Hill
also owns [ALEKS](../systems/aleks.md), meaning thirty years of knowledge space theory sits in
the same company.

**WileyPLUS** — publisher of **Moran & Shapiro**, the other standard text.

**EES (Engineering Equation Solver)** — not a tutor, but the tool many thermodynamics courses
actually require. It has built-in property data, which makes it the existing answer to the
problem our [property tools layer](../domain/property-data-tools.md) addresses. Worth
understanding precisely what EES does and doesn't teach: it removes the property-lookup
burden entirely, which is either good scaffolding or a skill bypass depending on who you ask.

## Why the AI tutoring literature ignores them

Nearly every published AI tutor evaluation compares against "no help," a control group, or
another chatbot. Almost none compare against the publisher platform the students are already
required to use.

That's a real gap in the field's evidence base, and it's convenient for the field.

## What this means for us

**1. The honest comparison condition is harder than it looks.** Our tutor is not entering an
empty room. A PSU thermodynamics student plausibly has: the publisher platform (required),
[PSU AI Studio](psu-ai-landscape.md) with Claude/ChatGPT/Gemini (free), Chegg (paid, at 11pm),
office hours, and a study group.

**Beating "nothing" is not a result.** → [open question C4](../../docs/03-open-questions.md)

**2. Their hint ladders are the most-tested in existence.** Mastering Engineering has served
hint sequences to millions of engineering students and iterated on them commercially for
years. We should look hard at that structure before designing ours from scratch.
→ [Socratic tutoring](../concepts/socratic-tutoring.md)

**3. They have the data we don't.** Per-problem difficulty, common wrong answers, time on
task, at enormous scale. We can't get it, but we should know it exists and be humble about
claims that we've discovered something about how students fail.

**4. What they can't do is our opening.** They have no conversation, no natural-language
understanding of a confused question, no course-specific context beyond their own problem
bank, and no ability to help with the instructor's own materials. That's the seam.

## Access — ask the sponsor

Evaluator access to these platforms is the single most useful thing an instructor sponsor can
provide for the [competitive teardown](../../research/competitive-teardown/README.md), and it
costs them nothing. Ask early.

## Open questions

- [ ] Which platform does the PSU course actually use, and which textbook?
      **Blocking for [property tools](../domain/property-data-tools.md) reference states too.**
- [ ] Can we get evaluator access?
- [ ] What does Mastering Engineering's hint ladder actually look like, level by level?
- [ ] Is there published efficacy research on these platforms, or only vendor claims?
- [ ] Are these platforms adding LLM features? (If Pearson ships an AI tutor into the course
      next semester, our competitive position changes overnight. **Check.**)
- [ ] Does the course require EES, and what does that imply about what students are expected
      to do by hand?

## Connects to

- [VanLehn 2011](../concepts/vanlehn-2011.md) — the publisher platforms are step-based
- [ALEKS](../systems/aleks.md) — same corporate parent as Connect
- [competitive teardown](../../research/competitive-teardown/README.md) — tier 2 tools
- [property data tools](../domain/property-data-tools.md) — EES as prior art
- [open questions C4](../../docs/03-open-questions.md) — the comparison condition

## Sources

- Vendor documentation for Mastering Engineering, McGraw Hill Connect, WileyPLUS `[found]`
- [ALEKS research page](https://www.aleks.com/about_aleks/research_behind) `[found]`
- **Gap: no independent efficacy literature located for these platforms. Worth searching
  properly — it's a notable absence given their market position.**
