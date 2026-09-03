# The systematic map of our field (PRISMA, 46 studies)

**Type:** practice
**One line:** The only systematic review of AI-driven intelligent tutoring in **engineering
education**, and its central finding is the gap five of our systems stumbled into independently:
**almost nothing supports instructors.**
**Why we care:** This is the document that tells us what our own search has been missing. It was
invisible to every automated sweep run for this project and took three attempts to obtain by hand.

> **Verification: `[read]` — full text, 22 pp., 2026-09-03.** Held at
> `course-materials/papers/porto-2025-its-engineering-education-slr.pdf`.

Rodrigues et al. (2025). *"A Systematic Literature Review of AI-Driven Intelligent Tutoring Systems
in Engineering Education: Emphasizing Personalization, Feedback, and Student Monitoring."*
**IEEE Access**, [DOI 10.1109/ACCESS.2025.3626473](https://doi.org/10.1109/access.2025.3626473).
Universidade do Porto. **PRISMA methodology, 46 peer-reviewed studies.** CC-BY.

---

## ⭐ Their feature taxonomy is a design checklist

The review codes every system against a fixed feature set. **This is more useful to us than any
individual finding** — it is a checklist of what an engineering ITS can have, derived from 46
systems rather than from our imagination:

**Student-facing:** `RTF` real-time feedback · `SSG` step-by-step guidance · `PSA` problem-solving
assistance · `PLP` personalised learning paths · `ACS` adaptive content selection · `PTPT` pre- and
post-testing · `CA` continuous assessment · `QAS` question-and-answer system · `OSP` overview of
students' progress · `AR` affective recognition

**Instructor-facing:** `TASP` teachers' access to students' progress · `CPT` content preparation
for teachers · `ASLL` aggregates students by learning level

Grouped under macro-categories: **LAA** learning algorithms and adaptation, **DMPS** decision-making
and personalisation, **LMKR** learner modelling and knowledge representation, **PFAI** pedagogical
foundations for AI integration, **LIT** language and interaction.

**How often each appears** (of 46 studies): **ACS 38**, **RTF 34**, **PLP 28** — against
**TASP, CPT and ASLL each in fewer than 10.**

## ⭐⭐ The gap: dual-user support

> *"While many ITS solutions are designed to support student learning, **far fewer provide explicit
> support for instructors**, such as access to analytics or customization tools. Features that
> enable dual-user support, such as **TASP, CPT, and ASLL, were among the least implemented,
> appearing in fewer than 10 studies each**."*

> *"This imbalance indicates a **design gap**: while ITS research increasingly prioritizes
> personalization for [students], instructor support remains limited and underutilized."*

**And the heatmap says these capabilities actively fail to co-occur:**

> *"The heatmap reveals a **negative correlation** between QAS and features like OSP for both
> learners and educators. This implies that **these capabilities are rarely combined** in existing
> systems."*

**A chatbot and a progress view are, empirically, alternatives rather than companions.** Nobody
builds both.

⭐ **This independently confirms what five systems in this repository arrived at separately** —
[Stan](../systems/stan-udel.md) (whose only real contribution is instructor-facing lecture
analytics), [PeteChat](../systems/petechat-purdue.md), [Ethel](../systems/ethel-eth.md),
[aiPlato](../systems/aiplato-uta.md) and [bioTutor](../systems/biotutor-eth.md). **We had five
data points and a hunch; this is the systematic confirmation, from a review that saw 46 systems.**

**Only one reviewed system does both well** — STUART, which *"proactively support[s] both learners
and educators by combining learner profiling with data-driven r[ecommendations] and
instructor-facing dashboards"* — and even that *"is not tailored specifically for engineering
education, leaving a gap in addressing the c[ontext of] domain-specific knowledge."*

## ⚠ Two more gaps that describe our opening precisely

**1. The field is mostly programming.**

> *"Most chatbot-based ITSs focus narrowly on **programming-related support**."*

Which matches what we found from the other direction: nearly every deployed system in
[`systems/`](../systems/) is CS, and the three thermodynamics systems
([Stan](../systems/stan-udel.md), [Ethel](../systems/ethel-eth.md),
[GPThermo](../systems/gpthermo-wpi.md)) are all answer engines.

**2. Real-time feedback is usually generic.**

> *"Many QAS offering RTF **fail to provide personalized guidance. They deliver generic responses
> regardless of user background or past performance**."*

They name examples — ParichartBOT *"does not [use] history for contextual adaptation"*; Q-Module-Bot
*"does not personalize content or recommend resources based on individual student needs"* — and
conclude that **only one** of 46 systems adapts Q&A responses to a learner profile.

**So "personalised" in this literature usually means adaptive content selection, not adaptive
conversation.** A tutor that actually conditions its replies on what this student has already got
wrong is rarer than the word "personalized" in these abstracts suggests.

**And note what that implies about our own student model.** The
[three-way write decision](agent-memory.md) and the
[trusted learner state a policy core would read](../concepts/guardrails.md) are not standard
practice in this field — they are the gap.

## What this changes for us

1. **The dual-user finding is now confirmed, not inferred.** Build the instructor view. It is
   under-implemented across 46 systems, it is what five independent teams converged on, and it
   carries no student-facing risk.
2. ⭐ **Aim at the intersection nobody occupies:** a system that is *both* conversational *and*
   maintains a real learner model *and* surfaces it to an instructor — in a **non-programming**
   engineering domain. The review says each of those is rare and the combinations rarer.
3. **Use their feature codes in our own design doc.** Saying "we implement RTF, SSG, PSA and TASP
   but not ACS or AR" is a more precise scope statement than prose, and it maps directly onto a
   literature.
4. ⚠ **Do not read this as permission to claim novelty.** It reviews **46 studies**; our own
   sweeps found systems it does not cover ([GPThermo](../systems/gpthermo-wpi.md),
   [aiPlato](../systems/aiplato-uta.md), the [ASEE deployments](../systems/rag-tutor-southeast.md)). **A
   systematic review is a systematic sample, not a census** — and this one confirms the shape of
   the field rather than closing the question.

## ⚠ Limits

- **46 studies** with stated exclusion criteria and database coverage — every SLR's findings are
  a function of its search string, and ours found engineering-education work this one does not
  cite.
- Feature coding is **presence/absence**, not quality. A system "has RTF" whether its feedback is
  good or useless.
- **No effect sizes and no learning outcomes** — it maps features, not efficacy. For that, see
  [the proximal/distal collapse](../concepts/vanlehn-2011.md).
- Author's accepted version, not the final published copy.

## Connects to

- [Institutional landscape](institutional-landscape.md) — the systems this review samples from
- [Stan](../systems/stan-udel.md), [PeteChat](../systems/petechat-purdue.md), [Ethel](../systems/ethel-eth.md), [aiPlato](../systems/aiplato-uta.md), [bioTutor](../systems/biotutor-eth.md) — the five independent arrivals at the instructor view
- [Agent memory](agent-memory.md) — what a real learner model would require
- [GPThermo](../systems/gpthermo-wpi.md) — a thermodynamics system this review does not cover

## Sources

- [Rodrigues et al. (2025), "A Systematic Literature Review of AI-Driven Intelligent Tutoring Systems in Engineering Education," *IEEE Access*](https://doi.org/10.1109/access.2025.3626473) `[read — full text, 22 pp., 2026-09-03]` — CC-BY; held locally
