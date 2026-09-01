# bioTutor — ETH Zurich

**Type:** system
**One line:** ETH's second course-specific tutor — **open-source**, deployed for **23 weeks to 407
students** with **>10,000 interactions** — and the fourth independent system to arrive at an
**instructor dashboard** as a core feature.
**Why we care:** It is the longest single-course deployment in this knowledge base, it publishes
its framework for other disciplines to adapt, and it is the clearest evidence that the
instructor-facing view is not optional.

> **Verification: `[abstract read in full]` — 2026-09-01. MDPI's PDF is bot-blocked; the
> abstract is complete and detailed, obtained via the DOAJ API. Figures and the edTAM item-level
> results are unread.**

*"A Lecture-Specific AI-Based Tutor for Higher Education: Pedagogical Design and Empirical
Evaluation."* **Educ. Sci.** 16(5), 812 (2026).
[DOI 10.3390/educsci16050812](https://doi.org/10.3390/educsci16050812). Institute for Biomedical
Engineering, **ETH Zurich**. Gold OA.

## What it is

Three components, and the third is the interesting one:

1. **A curated knowledge base** — course-grounded, like every system here.
2. **A didactically structured interaction design** — their framing is **constructivist learning**,
   against systems that *"lack pedagogical grounding, course alignment, and insight into student
   learning."*
3. ⭐ **A learning analytics dashboard for instructors** that *"summarizes anonymized
   student–chatbot conversations."*

## Deployment

| | |
|---|---|
| Course | Introductory biology, **407 enrolled** |
| Duration | **23 weeks** — a full academic year |
| Volume | **>10,000 interactions** across **>1,000 conversations** |
| Licence | **Open source** |

**This is the longest deployment in this base**, against KAIST's 14 weeks and the
[southeastern RAG+SRL tutor's single semester](rag-tutor-southeast.md). Usage patterns show it was
used *"both for learning and exam preparation"* — the two modes
[UIC and USAFA students described](../evidence/student-ai-perceptions-2025.md).

## ⭐ The instructor dashboard, now a four-way convergence

The lecturer dashboard *"provided aggregated insights into students' questions and recurring
difficulties."*

| System | Instructor-facing feature |
|---|---|
| [Stan](stan-udel.md) | Question mining and confusion detection from lecture transcripts — *its only real contribution* |
| [PeteChat](petechat-purdue.md) | Instructor dashboard: content upload, provenance, tone config, alignment metrics |
| [Ethel](ethel-eth.md) | Planned instructor self-serve upload platform |
| [aiPlato](aiplato-uta.md) | Usage logs and analytics at assignment and problem level |
| **bioTutor** | **Aggregated view of student questions and recurring difficulties** |

**Five systems, independently, and a
[systematic review naming dual-user support as the standing gap](../practice/institutional-landscape.md).**
At this point the instructor view is not a nice-to-have we might add — **it is the feature every
team converges on once they have real usage data**, presumably because it is the thing that makes
the deployment survive contact with a department.

**For us it is also the cheapest publishable artefact:** an aggregated view of what a
thermodynamics cohort is getting wrong needs no student-facing risk and directly feeds
[our misconception catalogue](../../research/domain/skill-graph-draft.md).

## ⚠ What it measures — and does not

They built **edTAM**, an education-adapted extension of the **Technology Acceptance Model**,
covering *usefulness, ease of use, learning relevance, output quality, and result
demonstrability*. Results: *"high usability, strong perceived usefulness, and broad interest in
adopting similar tools."*

**Every one of those is a perception.** There is **no learning outcome** — no pre/post, no exam
comparison, no control. After 23 weeks and 10,000 interactions, what we know is that students
liked it.

⚠ **And [TUM just showed why that is not reassuring](../evidence/tum-dissociation-2025.md):
students rated unrestricted ChatGPT as easier and more helpful than the scaffolded tutor that
actually preserved their motivation.** Perceived usefulness selects for answer-giving. A high TAM
score is compatible with a tool that teaches nothing.

**This is the single most common failure in the deployment literature** — Ethel, PeteChat,
bioTutor and GPThermo are all built, all deployed, and none of them measured learning.

## What we should take

1. ⭐ **Look at their code.** Open-source, explicitly *"enables adaptation to other disciplines."*
   **A forkable, deployed, year-long-tested course tutor is worth an afternoon of evaluation
   before we write a line.** → [open questions](#open-questions)
2. **Build the instructor dashboard early.** Five systems converged on it; it is low-risk and it
   is what gets a department to sponsor you.
3. **Do not repeat their evaluation.** TAM instruments are cheap and we should run one — but as a
   secondary measure beside a [distal, unassisted outcome](../evaluation/concept-inventories.md),
   never instead of it.

## Open questions

- [ ] **Where is the source?** The abstract says open-source but the repository is not named in
      the DOAJ record. Worth finding — this is the highest-value follow-up on this node.
- [ ] What does "didactically structured interaction design" concretely mean? Constructivist is a
      stance, not a mechanism. The full text should say.
- [ ] Is this from the same ETH group as [Ethel](ethel-eth.md)? Ethel is Rectorate + AI Center,
      bioTutor is Biomedical Engineering — **possibly two independent ETH efforts**, which would
      itself say something about how institutions actually adopt these.

## Connects to

- [Ethel](ethel-eth.md) — ETH's other tutor
- [Stan](stan-udel.md), [PeteChat](petechat-purdue.md), [aiPlato](aiplato-uta.md) — the dashboard convergence
- [TUM dissociation](../evidence/tum-dissociation-2025.md) — why perceived usefulness is not evidence
- [Engagement decay](../concepts/engagement-decay.md) — 23 weeks is the longest curve available
- [Institutional landscape](../practice/institutional-landscape.md)

## Sources

- ["A Lecture-Specific AI-Based Tutor for Higher Education: Pedagogical Design and Empirical Evaluation," *Educ. Sci.* 16(5), 812 (2026)](https://doi.org/10.3390/educsci16050812) `[abstract only — MDPI PDF bot-blocked, 2026-09-01]` · [DOAJ record](https://doaj.org/article/6d7b154181de4bc1b74983fb1dbb4a85)
