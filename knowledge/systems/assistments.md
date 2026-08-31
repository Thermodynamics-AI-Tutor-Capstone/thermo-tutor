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

## ⚠ Evidence — three corrections, and the third would have blindsided us

> **Corrected 2026-08-31 from the primary papers.**

**⚠ 1. "The SRI study" and "the Maine study" are the same study.** Roschelle, Feng & Murphy are
SRI International; Mason is University of Maine; the trial ran in **43 Maine schools**. Citing
them as two independent findings is a factual error a committee member can catch.

**The trial itself is genuinely strong:** school-level matched-pair cluster RCT, **N = 2,850
grade-7 students**, TerraNova outcome scored blind by the publisher, **WWC "meets standards
without reservations," ESSA Tier 1**. Result **g = 0.18** (Roschelle et al. 2016, 2-level HLM);
**g = 0.22 [0.15, 0.30]** in the 3-level reanalysis (Murphy et al. 2020).

**⚠ 2. "Nearly a year of additional gains" overstates it.** The authors' own translations are
**two-thirds of a year** (*"an effect size of 0.22 represents an additional two-thirds of a year
of gain… compared to the 0.30 expected gain due to a full year of 7th grade math instruction"*)
and **0.76 of a year**. No source — including ASSISTments' own marketing — claims a full year.
**Safe formulation: "about two-thirds of a school year of extra math growth, roughly double that
for students entering below the median."**

**⚠ 3. The independent replication failed on its primary outcome.** Feng et al. (AIED 2023) ran
it again in **North Carolina**, chosen as *"a state more demographically representative of the
U.S. than Maine"* — 63 schools, 41 districts, 102 teachers. **Student learning was null:**
*"The model didn't detect a significant difference between treatment and control students."*
(COVID closed schools mid-trial and forced an outcome-measure substitution, which is a real
mitigating factor.) The **g = 0.10 that circulates for North Carolina is a *delayed* effect**
measured a year later on the resumed state test, in a separate paper. **ASSISTments' own
Evidence of Impact page presents the 0.10 and never mentions the immediate null. Cite the
null.**

**⚠ 4. Usage inequity, and it is directly relevant to any adaptive-help design.** Non-IEP
students attempted **32% more problems** than IEP students (876 vs 662); non-FRL **16% more**
than FRL; above-median prior achievement **23% more**; males 10% more — all p < .01. Yet the
*effect* was largest for low prior achievers (**g = .29 vs .12**).

> **The tool that helps low performers most is used least by them.**

That is the cleanest statement of the engagement/equity problem anywhere in this knowledge base.
→ [equity](../practice/equity.md), [engagement decay](../concepts/engagement-decay.md)

Dosage note worth carrying: students completed **967 problems / 14 hours** across the year —
*"We had expected 18 to 24 hr."*

## E-TRIALS — copy the idea, but know its limits

ASSISTments runs **E-TRIALS**, infrastructure letting external researchers run randomized trials
inside the live platform, with **student-level randomization** (not class- or school-level),
*"allowing experiments to be conducted within classrooms."*

The insight generalizes: **if your tutor logs every interaction and can randomize anything,
every deployment is an experiment.**

**⚠ But the platform is a weaker model than its reputation suggests, on exactly the axis we
care about.** Its study schema has fields for study type, conditions (2–8), problem sets,
pre/post tests and surveys, and an OSF project ID — and **no fields for sample size, target N,
power, allocation ratio, stopping rule, eligibility criteria, blocking or stratification,
covariates, or a declared primary outcome.** All of that is pushed out to the OSF
preregistration. The platform enforces *that a prereg exists*, not that it is adequate.
**Build those fields into our own instrumentation.**

**⚠ And the failure rate is sobering:** of **103 experiments deployed in ASSISTments since 2019,
only 50 were usable** — *"many experiments were created incorrectly… or had broken links to
videos, leading students to never be randomized to a condition."* **~50% loss on a mature
platform.** Build a validation gate that proves randomization actually fired before counting a
session.

Their own enumerated threats to validity, worth copying into our design doc: lack of classroom
context; **contamination** (in one study control students texted friends, which *"diluted the
effect size"*); differential attrition; sequencing and carryover across successive experiments;
and **novelty/Hawthorne effects** — *"Novelty effects inflate an observed effect size.
Ultimately we are able to detect novelty effects through replication."*

Dependent measures actually used across 50 E-TRIALS RCTs: **problems-to-mastery 44%, posttest
score 44%**, learning gains 7%, assignment correctness 3%, completion 1%.

**No demographics are collected at all** — *"to preserve their anonymity."* SES is proxied by
IRS **Opportunity Zone** status inferred from the domain of the teacher's school email. That is
a clever, cheap, privacy-preserving pattern worth stealing.

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

- [Roschelle, Feng, Murphy & Mason (2016), "Online Mathematics Homework Increases Student Achievement," *AERA Open* 2(4)](https://doi.org/10.1177/2332858416673968) `[read]` — CC-BY. The Maine trial, g = 0.18
- Murphy, Roschelle, Feng & Mason (2020), *JREE* `[read]` — 3-level reanalysis, **g = 0.22 [0.15, 0.30]**; the usage-inequity finding
- [Feng et al. (2023), "Implementing and Evaluating ASSISTments… over Two Years," AIED 2023](https://files.eric.ed.gov/fulltext/ED631720.pdf) `[read]` — **the North Carolina replication, null on the primary outcome.** Free via ERIC; paywalled at Springer
- Feng, Huang, Collins, Heffernan & Heffernan (2023), LNCS 13917 `[read]` — the **delayed** g = 0.10, N = 5,991
- [E-TRIALS](https://www.assistments.org/e-trials) `[read]` — schema extracted from the live app bundle
