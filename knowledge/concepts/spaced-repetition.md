# Spaced Repetition

**Type:** concept
**One line:** Scheduling review at the moment a memory is about to fade — the mechanism
behind "amount of exposures and touches" in our project brief.
**Why we care:** [Knowledge tracing](knowledge-tracing.md) models what a student knows *now*
and classically has no forgetting term. Over a 15-week course, forgetting is not a detail.

## The algorithms

**SM-2** (Wozniak, 1987) — the classic. A fixed formula: every learner gets the same
scheduling curve regardless of how their memory actually behaves.

**FSRS** (Free Spaced Repetition Scheduler, 2022) — fits a statistical model to the
learner's own review history and schedules each item when its predicted **retrievability**
drops to a target (say 90%).

Benchmarked on **500M+ Anki reviews**:

| | FSRS | SM-2 |
|---|---|---|
| Reviews needed for equal retention | **20–30% fewer** | baseline |
| Mean absolute error on recall probability | **~4%** | ~14% |

Anki's default since v23.10 (Nov 2023). v6 (2025) adds a per-user forgetting-decay
parameter. Open source.

## How this combines with knowledge tracing

They answer different questions and should both be in the system:

| | Question answered |
|---|---|
| [Knowledge tracing](knowledge-tracing.md) | *Has this student ever mastered this?* |
| Spaced repetition | *Do they still have it right now?* |

Two students can have identical BKT mastery on the second-law statements and completely
different retrievability if one studied it in week 3 and the other in week 11.

The scheduling policy that follows:

```
surface next  ←  high curricular relevance  (what's due / what's next in the course)
              ×  low retrievability          (about to be forgotten)
              ×  mastery in the productive band (not too easy, not hopeless)
```

## Why this is a real differentiator, and where it gets hard

**The differentiator.** No LLM tutor found in this sweep does this. ChatGPT, Claude, Gemini
Study Mode — all stateless. [CS50 Duck](../systems/cs50-duck.md), [Stan](../systems/stan-udel.md),
[Cogniti](../systems/cogniti-sydney.md) — conversational, not scheduled. The publisher
platforms ([ALEKS](../systems/aleks.md), Connect) do adaptive recall but have no
conversation. **Doing both is genuinely open ground**, and it's the closest thing our brief
has to a defensible novel claim.

It also directly addresses [engagement decay](engagement-decay.md): a scheduler gives the
tutor a *reason to initiate*. A proactive tutor with something specific and well-timed to
say is a different product from one waiting to be asked.

**Where it gets hard — and this is not a minor caveat.** FSRS is validated on flashcards:
atomic items with unambiguous right answers, reviewed thousands of times. Thermodynamics
knowledge components are not flashcards. "Applying the steady-flow energy balance" is not
recalled, it's *performed*, and performance depends on the problem.

Nobody in this literature appears to have validated FSRS-style scheduling over procedural
engineering skills. **That is a real risk to this idea, and it should be stated plainly
before anyone builds on it.** The honest framing is: it's a promising and untested transfer,
not a proven technique in our setting.

A defensible middle path: use spaced scheduling for the parts of thermodynamics that *are*
recall-like — sign conventions, which relation applies when, phase-diagram regions,
definitions — and use mastery-driven problem selection for the procedural parts.

## Open questions

- [ ] Has anyone applied FSRS to procedural/conceptual skills rather than flashcards?
      **Search properly before committing.**
- [ ] What's a "review" for a knowledge component — a whole problem? A step?
- [ ] Does a spaced schedule conflict with the course's own sequence? (The course says study
      Rankine cycles this week; the scheduler says you're forgetting entropy generation.
      Who wins?)
- [ ] Can retrievability be estimated from few observations, given
      [our data-volume problem](knowledge-tracing.md)?

## Connects to

- [knowledge tracing](knowledge-tracing.md) — the other half of the student model
- [knowledge components](knowledge-components.md) — the unit being scheduled
- [engagement decay](engagement-decay.md) — scheduling enables proactivity
- [ALEKS](../systems/aleks.md) — the incumbent doing adaptive recall without conversation

## Sources

- [The FSRS Spaced Repetition Algorithm (RemNote docs)](https://help.remnote.com/en/articles/9124137-the-fsrs-spaced-repetition-algorithm) `[skimmed]`
- [FSRS vs SM-2 comparison](https://www.antiagent.io/blog/fsrs-vs-sm-2) `[skimmed]` — the benchmark figures
- [open-spaced-repetition/fsrs4anki](https://github.com/open-spaced-repetition) `[found]` — reference implementation
