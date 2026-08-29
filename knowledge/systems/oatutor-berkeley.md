# OATutor — UC Berkeley

**Type:** system
**One line:** The field's first open-source intelligent tutoring system with a Creative
Commons content library — BKT-based, React/Firebase, deployed in California community
colleges.
**Why we care:** If we want a working step-based ITS with knowledge tracing already in it,
this is the one we can actually read, run, and fork.

## What it is

From **Zachary Pardos**'s group (Berkeley School of Education / EECS). Published at
**CHI 2023**.

- **Open source** — [github.com/CAHLR/OATutor](https://github.com/CAHLR/OATutor)
- **ReactJS + Firebase**
- **Bayesian Knowledge Tracing** built in
- **Creative Commons content library** — the content is reusable too, which is rarer and
  arguably more valuable than the code
- Authoring via a **Google Spreadsheets pipeline**, deliberately crowdsourceable

Three years of development, seven classroom deployments, 25 student content creators, 3
developers, 4 researchers, 2 educators. Active deployments across California community
college and state university campuses.

## Why it matters to us

Two concrete uses:

**1. As a reference implementation.** Our design calls for
[knowledge tracing](../concepts/knowledge-tracing.md), hint ladders, and mastery-driven
problem selection. OATutor has all three, working, in readable code, with real deployment
behind it. Reading it will answer questions about grain, hint structure, and BKT parameter
fitting faster than any paper.

**2. As a possible foundation.** A serious option worth naming: **build the thermodynamics
content and the LLM layer on top of OATutor rather than building the ITS from scratch.**
That would put the well-understood parts (mastery estimation, hint sequencing, problem
selection) on proven code and concentrate our effort on what's actually novel — thermo
domain modeling, property-data tools, and LLM dialogue.

The authoring pipeline is the other half of the appeal. The
[bottleneck in this whole field is course-specific hand-work](../evidence/kestin-2025-rct.md),
and OATutor was explicitly designed to make that work distributable across a team of
non-engineers. That is a capstone-team-shaped affordance.

**Caveat, per our own standards:** everything above is from the CHI paper abstract and the
repo description. Before anyone commits to this, someone must actually clone it, run it,
and check whether it's maintained, whether the BKT implementation is sound, and how hard
new content authoring really is. Do not put OATutor in a plan on the strength of this node.

## Open questions

- [ ] Is it actively maintained? Last meaningful commit?
- [ ] How hard is authoring a new domain in practice, honestly?
- [ ] Does the BKT implementation fit parameters from data, or use fixed priors?
- [ ] Could an LLM be layered in for dialogue while OATutor owns state?
- [ ] Any published effect sizes from the seven classroom deployments?
- [ ] Does the content library include anything engineering or thermodynamics adjacent?

## Connects to

- [knowledge tracing](../concepts/knowledge-tracing.md) — OATutor's BKT engine
- [Cognitive Tutor](cognitive-tutor.md) — the tradition it implements
- [ALEKS](aleks.md) — the competing formalism
- [our roadmap](../../admin/roadmap.md) — a build-vs-fork decision to make in Phase 2

## Sources

- [Pardos et al., "OATutor: An Open-source Adaptive Tutoring System and Curated Content Library for Learning Sciences Research," CHI 2023](https://dl.acm.org/doi/10.1145/3544548.3581574) `[skimmed]`
- [GitHub — CAHLR/OATutor](https://github.com/CAHLR/OATutor) `[found]` — **clone and evaluate**
- [Berkeley School of Education — Leveraging AI to improve adaptive tutoring systems](https://bse.berkeley.edu/leveraging-ai-improve-adaptive-tutoring-systems) `[found]`
