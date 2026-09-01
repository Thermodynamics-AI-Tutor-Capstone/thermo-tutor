# Behavioral evaluation — did the student actually *do* anything with it?

**Status:** `[read in full]` — Niousha et al. 2026, 10,235 submissions, read 2026-08-31.

**One line:** Every rubric in this field scores what the tutor *said*. This paper scores what the
student *did next*, finds the two come apart, and finds that **the behavioral measure is the one
that predicts whether students found the tutor helpful** — while also containing a trap that
would train our tutor to give away answers.

---

## The argument

Current AI-tutor evaluation places systems on a single axis: **pedagogical quality of the feedback
message**. As long as that score is high, tutors look comparable. The authors' point is that this
*"ignores a critical question: what do students actually do with the feedback they receive?"*

They add a second axis grounded in interaction data, and the two axes separate systems that the
pedagogical axis alone cannot tell apart.

**Who:** Niousha, Boatright Smith, Akram, **Brusilovsky**, Hellas, Leinonen, **DeNero**, Norouzi —
UC Berkeley, NC State, Pittsburgh, Aalto. Serious ITS lineage, not a first-time education paper.
**Data:** 10,235 code submissions with paired tutor feedback from a large introductory
undergraduate programming course, comparing two deployed tutors (BaselineTutor vs
MisconceptionTutor) across different semesters.

## ⭐ The method, which we can copy almost directly

The measurement trick is simple and does not need instrumentation beyond what we would log anyway:
**diff consecutive student submissions and attribute the change to specific tutor sentences.**

For each pair of consecutive submissions `c_t → c_t+1` and each **sentence** of the feedback
message in between, an LLM judge (GPT-4.1, temperature 0) assigns two binary labels:

| Label | Question | Aggregated as |
|---|---|---|
| `rel` | Did this sentence influence the student's edit? | **RelScore** — fraction of sentences acted on |
| `succ` | Given it was acted on, was the change applied **correctly**? | **SuccScore** — evaluated only where `rel = 1` |

The judge also emits a rationale grounded in the actual diff. Pedagogical quality is scored
separately as **DAMR** (Desired Annotation Match Rate) — the fraction of feedback messages whose
label on a given rubric dimension matches the desired label.

**Reliability, which is better than most LLM-judge work and honestly reported:**

| Measure | LLM–human κ | Human–human κ |
|---|---|---|
| `rel` | 0.67–0.76 | 0.89 |
| `succ` | **0.80–1.00** | 0.80 |
| Pedagogical labels (DAMR) | ⚠ **0.65 and 0.44** | 0.76 |

Note the asymmetry: **the behavioral judgments are more reliable than the pedagogical ones.**
Judging "did this edit follow from this sentence" is an easier and better-posed task than judging
"was this good tutoring," which is a point in favour of the whole approach.

**Adapting it to thermodynamics is direct.** Consecutive problem attempts replace consecutive code
submissions; the diff is over stated assumptions, chosen equations, state points and numeric
answers rather than over source lines. Everything else transfers.

## ⚠⚠ The trap: the behavioral metric rewards exactly what pedagogy penalises

This is the finding to carry forward, and it is uncomfortable.

Pedagogically *desired* feedback reliably earned **higher RelScore** on every dimension — students
engage more with better tutoring. But SuccScore distributions for desired and undesired feedback
**largely overlap**, which the authors read as pedagogical quality influencing *which* feedback
students act on rather than *whether* the action is correct.

**One dimension reverses, in both semesters, and it is `revealing_answer`:**

| Tutor | SuccScore, answer **revealed** (undesired) | SuccScore, answer **withheld** (desired) |
|---|---|---|
| BaselineTutor | **67.8%** | 50.9% |
| MisconceptionTutor | **79.4%** | 53.0% |

Their interpretation: *"these successes are driven by students copying the revealed answer rather
than understanding and solving the problem themselves… high SuccScore alone does not necessarily
reflect effective learning, given that success can also be achieved through answer revelation."*

**If we optimise a tutor against immediate success rate, we will train it to give away answers,
and the metric will congratulate us the whole way.** This is
[Bastani's +48% assisted / −17% unassisted](../evidence/bastani-2025-harm.md) at the granularity
of a single edit, and it is the same shape as
[CS50's instruction dilution](../systems/cs50-duck.md). Three independent measurements, three
scales, one pattern.
→ [assessment integrity](../practice/assessment-integrity.md)

**Design rule: never use success rate as a standalone objective. Always report it stratified by
whether the answer was revealed.**

## What predicts students finding the tutor helpful

Three binary logistic models — pedagogy-only, engagement-only, combined. **Engagement metrics were
the most robust predictors** of a "highly helpful" rating:

- **RelScore β = 0.420, p < 0.001**
- **SuccScore β = 0.187, p < 0.001**
- Coefficients held nearly identical in the combined model, so engagement is not a proxy for
  pedagogical quality — it adds independent signal.

**Whether students act on feedback predicts satisfaction better than how good the feedback was.**

## ⚠ What it does not show

The authors are explicit: *"Our engagement-based metrics measure immediate feedback uptake but do
not assess longer-term learning outcomes; future work should relate these metrics to"* learning.
**RelScore and SuccScore are process measures, not outcome measures.** Given the `revealing_answer`
reversal, they are not even reliably *aligned* with outcome measures. They belong alongside a
proctored unassisted post-test, never instead of one.

Also: one institution, one introductory CS course, LLM-judged labels throughout, and the
comparison between the two tutors is **across semesters**, so cohort and course changes are
confounded with tutor version.

## What we should take

1. **Log consecutive attempts from day one.** The entire method is retrospective over data we
   would otherwise discard. Not logging attempt-to-attempt diffs is the one decision that would
   foreclose this analysis later.
2. **Report on both axes.** Pedagogical quality alone cannot distinguish two tutors; this is the
   cheapest way to show ours does something.
3. **Stratify every success number by answer revelation.** Non-negotiable.
4. **Expect uptake to be low.** [PeteChat logged 0% hint utilisation](../systems/petechat-purdue.md)
   and [CycleTalk saw help requests on 14% of actions](../systems/cyclepad-cycletalk.md). RelScore
   is the metric that would have caught both, early.

## Connects to

- [MathTutorBench](mathtutorbench.md) — the pedagogical axis this complements
- [Concept inventories](concept-inventories.md) — the outcome measure it cannot replace
- [Bastani et al. 2025](../evidence/bastani-2025-harm.md) — the same trap at semester scale
- [Assessment integrity](../practice/assessment-integrity.md)
- [Engagement decay](../concepts/engagement-decay.md) — RelScore is its early-warning instrument
- [PeteChat](../systems/petechat-purdue.md), [CycleTalk](../systems/cyclepad-cycletalk.md) — the
  two deployments whose uptake problem this would have surfaced

## Sources

- [Niousha, Boatright Smith, Akram, Brusilovsky, Hellas, Leinonen, DeNero & Norouzi (2026), "The Missing Evaluation Axis: What 10,000 Student Submissions Reveal About AI Tutor Effectiveness," arXiv:2605.05648](https://arxiv.org/pdf/2605.05648) `[read — full text, 15 pp., 2026-08-31]`
