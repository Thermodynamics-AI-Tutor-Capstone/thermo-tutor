# ASSISTments

**Type:** system
**One line:** A free math homework platform from WPI — one of the most rigorously
evaluated educational technologies in existence, and a working model for research
infrastructure.
**Why we care:** Not for its architecture, but for **E-TRIALS**: it turned a deployed
tutor into a randomized-experiment platform. That is what our instrumentation should aspire
to.

## What it is

Built by **Neil Heffernan** and colleagues at **Worcester Polytechnic Institute**.
Web-based, free, used by **1M+ students**, for nightly homework support and in-class
formative assessment.

The name is the design: it **assists** (hints, scaffolding on wrong answers) while it
**assesses** (data on what students know). One interaction, two purposes.

## Evidence

Unusually strong for this field:

- An **SRI Education** study found 7th graders in ASSISTments schools scored higher on
  standardized math tests than peers in non-using schools.
- A prior **Maine** study found nearly **a year of additional gains** for 7th grade math.
- **$7M+** in IES grants for further studies, including a five-year efficacy evaluation
  across ~**15,000** 7th graders in seven diverse US sites.

The reason this is well-evidenced is not that the system is smarter than others — it's
that Heffernan built the platform so experiments could run inside it.

## E-TRIALS — the thing to actually copy

ASSISTments runs **E-TRIALS**, infrastructure that lets external researchers run
randomized controlled trials inside the live platform. Randomization, assignment, and
outcome collection are built in.

The insight generalizes: **if your tutor logs every interaction and can randomize
anything, every deployment is an experiment.**

For us that means designing the interaction log so that, later:
- Any policy choice (hint ladder aggressiveness, proactive vs. reactive, hint wording) can
  be randomized per student or per problem
- Assignment is recorded alongside outcomes
- Analysis doesn't require going back and re-instrumenting

This costs almost nothing at design time and is impossible to retrofit. It's the single
most valuable structural lesson in this node.
→ [our roadmap](../../admin/roadmap.md)

## Open questions

- [ ] What is ASSISTments' hint-ladder design? It's one of the most-tested in existence.
- [ ] Is E-TRIALS documented well enough to imitate the schema?
- [ ] Any post-2023 work adding LLMs? (Heffernan is reportedly leading an AI math tutor
      effort — worth finding.)
- [ ] Is the ASSISTments interaction dataset open? It would be a real resource for
      calibrating [knowledge tracing](../concepts/knowledge-tracing.md).

## Connects to

- [knowledge tracing](../concepts/knowledge-tracing.md) — ASSISTments data is a standard
  KT benchmark corpus
- [Cognitive Tutor](cognitive-tutor.md) — the same research tradition
- [our roadmap](../../admin/roadmap.md) — instrument-for-experiments is a Phase 0 decision

## Sources

- [SRI study coverage — "Rigorous SRI Study Shows Online Mathematics Homework Program... Increases Student Achievement"](https://www.prnewswire.com/news-releases/rigorous-sri-study-shows-online-mathematics-homework-program-developed-at-worcester-polytechnic-institute-increases-student-achievement-300349922.html) `[skimmed]`
- [WPI news on $7M+ in IES research grants](https://www.wpi.edu/news/online-mathematics-homework-program-developed-worcester-polytechnic-institute-be-subject-more-7) `[skimmed]`
- [E-TRIALS](https://www.assistments.org/e-trials) `[found]` — **read this properly**
- [Implementing and Evaluating ASSISTments at Large Scale over Two Years](https://link.springer.com/chapter/10.1007/978-3-031-36272-9_3) `[found]`
