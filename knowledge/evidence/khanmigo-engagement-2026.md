# Oreopoulos & Low 2026 — "One Click Away": Khanmigo in a two-year school experiment

**Type:** study (**two-year cluster randomized trial**)
**One line:** 18 Tennessee middle schools, two years. Khan Academy raised math achievement —
but **the AI tutor added nothing detectable**, because students barely used it.
**Why we care:** This is the largest and longest RCT of an AI tutor in this knowledge base,
and its conclusion is a sentence we should put on the wall.

> **Verification: `[read]` — full text, 2026-08-31. Two corrections:** this node previously
> described the study as *observational* (it is a **cluster RCT**) and misstated the 17%
> figure (it is 17% of sessions **in which the student made a mistake**, which is worse).

## The study

**Philip Oreopoulos** (University of Toronto) and **Nina Low** (Charles River Associates).
EdWorkingPaper No. 26-1551, Annenberg Institute at Brown, August 2026.

- **Two-year cluster randomized trial**, **18 Tennessee middle schools**
- Randomly assigned students used Khan Academy with **Khanmigo, configured to coach rather
  than give answers**, during existing **daily remedial mathematics sessions**
- Described by the authors as *"some of the first large-scale experimental evidence"*

## The results

| Measure | Effect |
|---|---|
| Math achievement | **+1.3 national percentile ranks per term** |
| Over a school year | **0.06 – 0.08 SD** |
| Implied, for a full year of *active participation* | **0.14 SD** |

**And the finding that matters:**

> *"These gains resemble those from Khan Academy practice **without** AI assistance."*

The platform worked. **The AI tutor layered on top produced no detectable additional
learning.** Not harm — [that's Bastani](bastani-2025-harm.md) — simply nothing.

## Why: the engagement numbers, precisely

- **96%** of students tried Khanmigo at least once
- The median student messaged it on **a third of the days they practiced**
- And in only **17% of the exercise sessions *in which they made a mistake***

That last one is the damning version. **Even when a student got a problem wrong — the exact
moment a tutor exists for — they engaged the tutor five times out of six... not at all.**

And the engagement that did occur was shallow: *"Messages that students did send were mostly
bare answers or clicks on suggested prompts."* Not dialogue. Not questions. Clicks.

The authors' conclusion, which is the single most quotable line in this knowledge base:

> **"The binding constraint appears to be engagement: realizing the promise of AI tutoring
> will require getting students to use it, not just giving them access."**

## Why this is the most important study in the knowledge base

Every other finding here is conditional on students using the thing.

- [Kestin's 2× gains](kestin-2025-rct.md) — students were *assigned* to use the tutor
- [Bastani's arms](bastani-2025-harm.md) — structured practice sessions, 90 minutes each
- [Tutor CoPilot](../systems/tutor-copilot.md) — the user is a paid tutor already at work

**This is the one study that gave a well-built, guardrailed tutor to real students in a real
daily routine for two years and just watched.** The answer was: they didn't use it, and it
didn't matter.

If our tutor achieves Kestin-level quality and Khanmigo-level engagement, the population
effect is roughly 17% of an effect. **That arithmetic belongs in our project plan, and in
whatever we tell our advisor to expect.**

Note the design contrast that makes this actionable rather than merely discouraging:
[CS50](../systems/cs50-duck.md) got to **3% never-users** by coupling the tool to course
policy, embedding it where the work happens, throttling it, and making it charming.
Khanmigo did none of those. **Engagement is a design variable, not a fact of nature** — but
it has to be designed for deliberately, and nobody in this literature did.

## What it doesn't tell us

- **Who** the 17% are. Note that [KAIST](kaist-vta-2025.md) found the least-prepared students
  engaged *most* at university level. → [equity](../practice/equity.md)
- **Why** students didn't engage. The "bare answers or clicks on suggested prompts" finding
  hints at a UI story — suggested-prompt chips may substitute for thinking rather than
  scaffold it, which is a caution about
  [PeteChat's "Try asking…" cards](../systems/petechat-purdue.md) too.
- Whether a **course-specific** tutor differs from a general one. Khanmigo covers all of
  Khan Academy; ours would know the student's actual assignment. Plausibly a real
  difference — and completely untested.

That last point is the most useful thing here: **it's a gap we're positioned to fill.**
Nobody has published voluntary week-by-week return rates for a course-specific university
tutor. If we instrument for it and report it honestly, that's a contribution regardless of
whether our learning effect is detectable.
→ [engagement decay](../concepts/engagement-decay.md)

## Open questions

- [x] ~~Read the full working paper~~ — done 2026-08-31.
- [ ] Is there a usage *curve* over the two years, or only aggregates? (Full paper is 17k
      words; the results section beyond the abstract has not been mined.)
- [ ] Did engagement correlate with prior achievement? Directly tests the
      [equity](../practice/equity.md) question against KAIST's finding.
- [ ] What exactly did the "coach rather than give answers" configuration look like?
- [ ] Has Khan Academy's proactive "Tutor Agent" changed these numbers?

## Connects to

- [engagement decay](../concepts/engagement-decay.md) — the general problem
- [Khanmigo](../systems/khanmigo.md) — the system
- [equity](../practice/equity.md) — who actually uses voluntary tools
- [Tutor CoPilot](../systems/tutor-copilot.md) — a design that sidesteps this entirely

## Sources

- [Oreopoulos, P. & Low, N. (2026). "One Click Away: AI Tutoring with Khanmigo in a Two-Year School Experiment." EdWorkingPaper 26-1551, Annenberg Institute at Brown](https://doi.org/10.26300/kner-hv33) `[read]` — abstract and framing read in full; results section not yet mined
- [Chalkbeat, "Students rarely engaged with Khan Academy's AI-powered tutor Khanmigo, study finds"](https://www.chalkbeat.org/2026/08/25/ai-tutoring-students-khanmigo-khan-academy-engagement-study/) `[skimmed]`
