# Kestin et al. 2025 — AI tutoring outperforms in-class active learning

**Type:** study (RCT, within-subject crossover)
**One line:** Harvard PS2, 194 students. An AI tutor produced **0.73–1.3 SD** greater
learning than an excellent active-learning classroom, in **less time**, with higher
engagement.
**Why we care:** The field's best result, the template for our study design — and, read in
full, it carries a limitation that lands directly on thermodynamics.

> **Verification: `[read]` — full text, 2026-08-31.** It is **gold open access**; an earlier
> fetch failure was a cookie-consent redirect, not a paywall.
> [Direct PDF](https://www.nature.com/articles/s41598-025-97652-6.pdf).

## The study

Greg Kestin, Kelly Miller (equal contribution), Anna Klales, Timothy Milbourne, Gregorio
Ponti — Harvard Physics and SEAS. *Scientific Reports* **15:17458**, 3 June 2025.

- **Physical Sciences 2 (PS2)**, Harvard's largest physics class — introductory physics for
  the life sciences. **233 enrolled; 194 eligible** (consent + participation in both
  conditions + all pre/post tests). ~316 student-lesson observations.
- **Fall 2023**, weeks 9 and 10 of the course. Sessions are 75 minutes.
- **Within-subject crossover**: students randomly assigned to two groups. Group 1 got the
  AI lesson in week 1 and the in-class lesson in week 2; group 2 the reverse. Topics:
  **surface tension** (week 1) and **fluid flow** (week 2). Pre-test before each lesson,
  post-test after.
- Randomization **respected existing peer-instruction working groups**, keeping regular
  collaborators together so the in-class condition wasn't degraded. A thoughtful detail.
- **The two lessons were taught by different instructors**, deliberately, to show the effect
  wasn't instructor-specific.

## The results

| Measure | Result |
|---|---|
| Median learning gain, AI vs. in-class | **more than double** |
| Rank-sum test | z = −5.6, **p < 10⁻⁸** |
| Effect size, linear regression | **0.63** — the authors call this an underestimate |
| Effect size, **quantile regression** (avoids ceiling effects) | **0.73 – 1.3** |
| Median time on task, AI group | **49 minutes** vs. 60 assumed in class; 70% finished under an hour |
| Engagement (5-pt) | AI **4.1** (SD 0.98) vs. in-class 3.6 (SD 0.92), t(311) = −4.5, p < 0.0001 |
| Motivation | AI **3.4** (SD 1.0) vs. in-class 3.1 (SD 0.86), t(311) = −3.4, p < 0.001 |

Two other statements about perceived learning showed **no** significant difference — worth
noting, since "students loved it" is often over-claimed from this paper.

**There was no correlation between time on task and post-test score**, across a wide range of
times. The authors attribute the benefit to *self-pacing* rather than to more time.

## ⚠ The generalizability case is stronger than I previously credited

My earlier note dismissed this as "Harvard undergrads, not a general population." The authors
anticipated that and ran the subgroup analysis:

- Students with **FCI pre-test below 40%** and **above 40%** *both* showed significantly
  better post-test performance with AI tutoring (**p < 0.001** for each).
- The same held below and above the 65% benchmark on the **CLASS** scientific-attitudes
  survey.
- Typical pre-instruction FCI scores nationally run ~30–50%; this sample spans that range,
  and PS2's FCI scores are comparable to students at other universities.

Controls in the regression: pre-test score, prior physics knowledge (FCI), prior ChatGPT
experience, and other factors.

**And the comparison condition is genuinely hard.** PS2's active learning is a documented,
optimized implementation; the authors note that the literature establishing its
effectiveness overlaps with the present author list, and both instructors scored above
departmental averages on evaluations. This is not "AI beats a bad lecture."

## ⚠ The limitation that lands on us

The authors are unusually forthright, and one caveat is directly relevant:

> *"we do not presume that structured AI tutoring will always outperform in-class active
> learning in all contexts, for example, **those requiring complex synthesis of multiple
> concepts and higher-order critical thinking**."*

Their lessons targeted the **understanding, applying, and analyzing** levels of Bloom's
taxonomy — a stage *"characterized by a meaningful degree of information delivery"* that they
describe as *"particularly well suited for current generative AI tutors."*

**Engineering thermodynamics is largely the opposite kind of subject.** The
[RPTU exam](../domain/superstudent-thermodynamics.md) is explicitly designed so that
*"problems… cannot be solved by relying on pattern learning but only by knowledgeably and
creatively applying the principles"* — i.e. synthesis and higher-order reasoning, the case
Kestin explicitly declines to claim.

**This should temper our expectations directly.** The field's best result comes from
information-delivery-heavy content, and our subject is the category its authors carved out.
Not a reason to abandon the design — a reason not to promise 2×.

## What the tutor actually was, and the design lesson

Seven pedagogical best practices were targeted: active learning, managing cognitive load,
promoting a growth mindset, **scaffolding content**, ensuring accuracy, timely feedback, and
self-pacing.

**Two implementation findings that confirm this knowledge base's central architectural claim
— stated by the authors of the field's best result:**

1. **The system prompt wasn't enough.** They found *"that a system prompt could not reliably
   provide enough structure to scaffold problems with multiple parts,"* so the **platform**
   was built to guide students sequentially through each part of each problem. Structure
   moved out of the prompt and into code.
   → [guardrails](../concepts/guardrails.md), [the paper §V](../PAPER.md)
2. **They didn't trust GPT-4 to generate the answers.** *"we avoided relying solely on GPT-4
   to generate… we enriched our prompts with comprehensive, step-by-step answers."*
   Pre-authored correct solutions in the prompt — **exactly what
   [Bastani's guardrailed arm did](bastani-2025-harm.md)**, independently. **83%** of students
   reported the tutor's explanations were accurate.

The authors also list what the result *depended on*: a heterogeneous student population,
**high-quality instructional videos**, an LLM able to follow complex prompts (GPT-4),
**expert-crafted, question-specific prompts written by instructors experienced with the
content**, a carefully structured scaffolding framework, and content suited to the format.

That video dependency is worth flagging: Kestin is a professional science-video producer.
**Some of this effect may rest on production resources a capstone team does not have.**

## What to copy

- **The crossover design.** Every student gets both conditions; each is their own control;
  statistically efficient at small n; and — per [Corvinus](corvinus-2025-overreliance.md) —
  the design least likely to provoke a student revolt over withheld AI access.
- **Randomize while preserving collaboration groups.**
- **Two lessons, two instructors**, to show instructor-independence.
- **Quantile regression** if post-test scores hit a ceiling.
- **Report the FCI/CLASS-stratified subgroup analysis** — it is what makes their
  generalizability claim credible, and the [TTCI-T](../evaluation/concept-inventories.md)
  could play the FCI's role for us.

## Open questions

- [ ] Read the Supplementary Material — the system prompt guidelines are in there, and that
      is the single most reusable artifact in the paper.
- [ ] Is the tutor platform itself available?
- [ ] How much authoring effort per problem? Still unstated, and it sets our scope.
- [ ] Their suggested future directions are a menu of adjacent projects: **homework,
      recitation, exam studying, pre-class assignments, laboratory**, plus systematic
      integration of **spacing** and the effect on **collaboration skills**.
      → [spaced repetition](../concepts/spaced-repetition.md)

## Connects to

- [Bastani 2025](bastani-2025-harm.md) — the contrasting null, and the shared mechanism
- [Corvinus 2025](corvinus-2025-overreliance.md) — why the crossover design also protects us
- [Superstudent](../domain/superstudent-thermodynamics.md) — why our subject is the harder case
- [guardrails](../concepts/guardrails.md) — they found the system prompt insufficient too
- [concept inventories](../evaluation/concept-inventories.md) — the FCI-stratified approach

## Sources

- [Kestin, Miller, Klales, Milbourne & Ponti, "AI tutoring outperforms in-class active learning: an RCT introducing a novel research-based design in an authentic educational setting," *Scientific Reports* 15:17458 (2025)](https://doi.org/10.1038/s41598-025-97652-6) `[read]` — **gold open access**, [direct PDF](https://www.nature.com/articles/s41598-025-97652-6.pdf)
