# Bastani et al. 2025 — Generative AI without guardrails can harm learning

**Type:** study (RCT)
**One line:** ~1,000 students, three arms. Unguarded GPT-4 made students **17% worse** on
unassisted exams; a guardrailed tutor eliminated the harm and produced **no benefit**.
**Why we care:** The most important experiment yet run on the question our project asks.
Read in full, it says something more specific and more useful than the headline: the
guardrails that worked were **per-problem, teacher-authored solutions and misconception
hints** — not a Socratic system prompt.

> **Verification: `[read]` — full text, 2026-08-31.** All figures below are from the paper
> itself.

## The study

Hamsa Bastani, Osbert Bastani, Alp Sungu (equal contribution), Haosen Ge, Özge Kabakcı,
Rei Mariman. University of Pennsylvania (Wharton / CIS). PNAS 2025.

- **Setting:** a large high school in **Turkey**, Fall semester 2023–24
- **Sample:** ~**1,000** students across ~50 classes, grades 9–11
- **Design:** four **90-minute** in-class sessions; sessions collectively covered ~**15%**
  of the semester's math curriculum
- **Structure:** each session had two phases — practice with assigned resources, then an
  **exam with no resources at all**
- **IRB:** University of Pennsylvania **#853745**, deemed **exempt under 45 CFR 46.104,
  category 1** ← *directly useful precedent for [our IRB submission](../../admin/irb.md)*

## The three arms

| Arm | What students got |
|---|---|
| **GPT Base** | A ChatGPT-like GPT-4 chat interface. Prompt gives the current problem and says to act as a tutor |
| **GPT Tutor** | Same interface **plus guardrails** (below) |
| **Control** | Course notes and textbook only |

Students never saw the system prompts.

## What "guardrails" actually meant — the part that matters

Not a Socratic instruction. Three concrete things, per problem:

1. **Hint, don't answer.** Instructed to give hints rather than the solution.
2. **The correct solution(s) in the prompt** — included explicitly *"to mitigate
   hallucinations."*
3. **Common student mistakes and the hint to give for each** — an
   expectation/misconception structure authored by teachers.

The authors' own caveat: *"This problem-specific construction is labor-intensive, but
ensures that GPT-4 does not provide incorrect feedback to the student."*

**That is [AutoTutor's expectation–misconception-tailored dialogue](../systems/autotutor.md),
rebuilt inside a prompt, per problem, by hand.** It is also the same mechanism as
[Kestin's expert-authored scaffolds](kestin-2025-rct.md). The two headline studies in this
field independently converged on hand-authored per-problem structure — and one got 2×
gains while the other got zero. See the reconciliation below.

## The results

| Arm | During AI-assisted practice | On the later unassisted exam |
|---|---|---|
| **GPT Base** | **+48%** vs. control | **−17%** vs. control |
| **GPT Tutor** | **+127%** vs. control | **≈ same** as control |
| Control | baseline | baseline |

## Three findings the summaries miss

### 1. GPT-4 was correct only 51% of the time

Querying GPT Base ten times per problem with the students' most common message ("What is
the answer?") across all **57 practice problems**:

- **51%** correct on average
- **42%** logical errors (steps partially or fully wrong)
- **8%** arithmetic errors
- Large problem-to-problem heterogeneity

GPT-4, on high-school math, wrong half the time. Any assumption that model capability has
since made this moot should be checked, not assumed — but note that the deployment was
**Fall 2023**, which the authors flag as a genuine limitation.

### 2. The cleanest evidence that students were copying, not reading

Two inferences, both elegant:

- **Logical errors hurt practice performance but showed no spillover to the exam.** If
  students had been *learning* the wrong method, the error should have followed them.
  It didn't — so they weren't learning anything, right or wrong.
- **Arithmetic and logical errors hurt practice performance about equally.** Students know
  arithmetic; if they were reading the solutions, they'd catch arithmetic slips and be hurt
  less by them. They weren't.

Together: **students were transcribing output without processing it.**
→ [productive failure](../concepts/productive-failure.md)

### 3. The guardrailed tutor got *more* engagement, not less

This is the finding that most changes our design thinking, because it contradicts the
intuitive worry that guardrails drive students away:

- **More messages per problem** with GPT Tutor than GPT Base, and the gap **widened over
  the four sessions**
- Students spent **13% more time** with GPT Tutor
- Superficial first interactions (repeating the question or asking for the answer), first
  session: **56% Base vs. 42% Tutor**. Across all problems in that session: **Base rose to
  67%, Tutor fell to 37%**
- Non-superficial conversations (never asked for the answer) were a small fraction in Base
  and a substantially larger fraction in Tutor, across all sessions

**Students got lazier with the unguarded tool and better with the guarded one, over time.**
Guardrails were not a friction that repelled students; they were a structure students
learned to use. → [engagement decay](../concepts/engagement-decay.md),
[guardrails](../concepts/guardrails.md)

### And: students had no idea they were being harmed

The authors find *"students do not perceive any reduction in their learning or subsequent
performance as a consequence of copying solutions."*

Satisfaction and self-reported learning are therefore **actively misleading** as outcome
measures here. → [concept inventories](../evaluation/concept-inventories.md),
[open question C3](../../docs/03-open-questions.md)

## Reconciling with Kestin

Both studies used hand-authored per-problem scaffolding. Kestin got ~2× gains; Bastani's
best arm got zero. So hand-authoring is not sufficient on its own. What differs:

| | [Kestin](kestin-2025-rct.md) | Bastani |
|---|---|---|
| n | 194 | ~1,000 |
| Population | Harvard undergrads | Turkish high schoolers, grades 9–11 |
| Duration | A semester of alternating weeks | Four 90-min sessions, ~15% of curriculum |
| Comparison | **Active-learning classroom** | Textbook and notes |
| Author-instructor | Physics-education researcher who taught the course | Research team + partner school |
| Result | ~2× | ≈ 0 |

The most defensible reading is that **dose and integration matter as much as design**.
Kestin's tutor was the course's actual learning activity for half the semester; Bastani's
was four sessions bolted onto an existing course. Neither study isolates which factor
carries the effect, and no one has run the experiment that would.

## The authors' own limitations

Worth quoting because they are unusually forthright: single topic (mathematics), single
high school, single country; objective grading available (unlike writing); deployed
**Fall 2023 when generative AI was still very new** — users are now more familiar and
models have improved substantially; **short-term outcomes only** (exam, not retention),
constrained by the partner school.

They also explicitly endorse two alternative directions: **educating students and teachers
on effective use**, and **teacher-facing rather than student-facing tools**, citing
[Tutor CoPilot](../systems/tutor-copilot.md).

## Connects to

- [Kestin 2025](kestin-2025-rct.md) — the contrasting result and the reconciliation
- [guardrails](../concepts/guardrails.md) — what they buy, and what they don't
- [AutoTutor](../systems/autotutor.md) — the EMT structure Bastani's prompt rebuilds
- [productive failure](../concepts/productive-failure.md) — the crutch mechanism
- [engagement decay](../concepts/engagement-decay.md) — guardrails *increased* engagement
- [our IRB](../../admin/irb.md) — Penn's exempt determination is a usable precedent

## Sources

- [Bastani et al., "Generative AI without guardrails can harm learning: Evidence from high school mathematics," PNAS (2025)](https://www.pnas.org/doi/10.1073/pnas.2422633122) `[read]` — full text (author preprint, 68pp incl. appendices)
- [Author preprint PDF](https://hamsabastani.github.io/education_llm.pdf) `[read]`
- [Knowledge@Wharton summary](https://knowledge.wharton.upenn.edu/article/without-guardrails-generative-ai-can-harm-education/) `[read]`
