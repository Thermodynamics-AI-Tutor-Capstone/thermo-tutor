# Bastani et al. 2025 — Generative AI without guardrails can harm learning

**Type:** study (RCT)
**One line:** ~1,000 students, three arms. Unguarded GPT-4 made students **17% worse** on
unassisted exams; a guardrailed tutor eliminated the harm and produced **no benefit**.
**Why we care:** The most important experiment yet run on the question our project asks. It
is the reason guardrails are non-negotiable, and the reason "our tutor helps students learn"
is a much harder claim than it sounds.

## The study

Hamsa Bastani, Osbert Bastani, Alp Sungu, Haosen Ge, Özge Kabakcı, Rei Mariman.
Published in **PNAS (2025)**; earlier as an SSRN working paper titled *"Generative AI Can
Harm Learning."*

Nearly **1,000 high school mathematics students in Turkey**, randomized into three arms:

| Arm | What students got |
|---|---|
| **GPT Base** | A ChatGPT-4-like chat interface, unrestricted |
| **GPT Tutor** | Similar interface **with safeguards** — built with teacher input, designed to guide with hints rather than give answers |
| **Control** | No technology. Textbook and notes |

Students used their assigned condition during **practice sessions**. They were later tested
on an **exam without any AI assistance.**

## The result

| Arm | During AI-assisted practice | On the later unassisted exam |
|---|---|---|
| **GPT Base** | **+48%** vs. control | **−17%** vs. control |
| **GPT Tutor** | **+127%** vs. control | **≈ same** as control |
| Control | baseline | baseline |

## What it means

**1. Unguarded generative AI actively harms learning.** Not "fails to help" — *harms*. A 17
point relative deficit against students with nothing but a textbook. The authors'
explanation: students use the model as a **crutch** during practice, and never build the
skill the practice was for. → [productive failure](../concepts/productive-failure.md)

**2. Practice performance and learning move in opposite directions.** The GPT Tutor arm
performed **127% better while using it** — the best practice performance of any arm — and
learned **nothing extra**. Any metric that measures assisted performance is measuring the
wrong thing, and it will flatter us in exactly the direction we want to be flattered.
→ [open question C3](../../docs/03-open-questions.md)

**3. Guardrails prevent harm and do not create learning.** This is the sentence to hold
onto. The best-designed arm — teacher-informed, hint-based, explicitly non-answering —
achieved **parity with a textbook**.

Every deployed tutor's "don't give the answer" system prompt is doing damage control. That
is genuinely worth doing. It is not a contribution.
→ [guardrails](../concepts/guardrails.md)

## How to read it against Kestin

[Kestin et al.](kestin-2025-rct.md) found ~2× learning gains from an AI tutor. Bastani found
zero for the guardrailed arm. Both are well-run RCTs. The reconciliation matters:

| | Kestin | Bastani |
|---|---|---|
| n | 194 | ~1,000 |
| Population | Harvard undergrads | Turkish high schoolers |
| Tutor | Expert-authored scaffolds, per-problem, built by a physics-education researcher | A guardrailed general chat interface |
| Comparison | Active-learning classroom | Textbook and notes |
| Result | ~2× gains | ≈ 0 |

The most plausible reading: **the hand-crafted, problem-specific scaffolding is where the
effect lives** — not in the model, and not in the guardrails. Kestin built a tutor for
*those* problems. Bastani deployed a well-guarded general tutor.

That is a claim about *our* project, and it's the central one: the differentiator is the
domain work, not the architecture.

## Caveats to check on a full read

- [ ] High school, not university. Does the crutch effect hold for undergraduate engineers?
- [ ] Single-topic, short duration? Longer exposure might differ in either direction.
- [ ] What exactly were the GPT Tutor guardrails? The design details are the most useful
      part of the paper for us and are not in the summaries.
- [ ] Was the exam immediate or delayed? Retention interval matters a lot.

> **Verification: `[skimmed]`.** Numbers here come from the Knowledge@Wharton article and
> search summaries. The PDF didn't text-extract. **Someone must read the PNAS version
> before any of these figures appear in a graded deliverable.**

## Connects to

- [Kestin 2025](kestin-2025-rct.md) — the contrasting positive result
- [guardrails](../concepts/guardrails.md) — what they buy and don't
- [productive failure](../concepts/productive-failure.md) — the mechanism
- [Socratic tutoring](../concepts/socratic-tutoring.md) — why a stance isn't enough
- [the paper, §IV](../PAPER.md) — how this fits the overall evidence picture

## Sources

- [Bastani et al., "Generative AI without guardrails can harm learning: Evidence from high school mathematics," PNAS (2025)](https://www.pnas.org/doi/10.1073/pnas.2422633122) `[found]` — **the version to read**
- [Knowledge@Wharton, "Without Guardrails, Generative AI Can Harm Education"](https://knowledge.wharton.upenn.edu/article/without-guardrails-generative-ai-can-harm-education/) `[read]` — source of the exact percentages above
- [Author preprint PDF](https://hamsabastani.github.io/education_llm.pdf) `[found]`
- [SSRN working paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4895486) `[found]`
