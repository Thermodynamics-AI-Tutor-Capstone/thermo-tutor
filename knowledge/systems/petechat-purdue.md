# PeteChat — Purdue

**Type:** system
**One line:** A course-specific, guardrailed AI tutor built by fine-tuning open-source
LLMs on course data, deployed in Purdue's ECE 20875 in Spring 2025.
**Why we care:** The closest **methodological** sibling to our project — a student-facing,
single-course tutor with published design rationale and an explicit "tutor, not solver"
stance.

## What it is

Purdue built PeteChat by collecting course-specific data and fine-tuning open-source LLMs,
deploying via Gradio/Hugging Face to undergraduates in **ECE 20875** (a Python programming
course). Spring 2025 was the first large-scale test. By **Spring 2026** a
"stable, preference-aligned version" extended into additional large undergraduate Python
courses — the paper frames this as the transition "from course-specific innovation to
broader, campus-level integration."

## The framing worth stealing

The paper's title is the thesis: **"Tutor, Not Solver."** That phrase does more work than
most system prompts. It names a design constraint that can be tested, argued about, and
violated — as opposed to "be Socratic," which is a vibe.

Reported design principles (from the abstract-level reading):
- Prevent direct answer provision
- Encourage metacognitive engagement
- Limit solution shortcuts
- Promote self-directed learning

## Why the trajectory matters to us

PeteChat is the only system found that documents the path **one course → several courses →
campus platform**. That's the arc a successful capstone would follow, and the paper
presumably discusses what broke along the way. Worth reading specifically for that.

Also note: **fine-tuning + preference alignment**, not just prompting. That's a heavier
approach than most course tutors take and a distinctly different bet from
[Stan's](stan-udel.md) local-RAG design or [Cogniti's](cogniti-sydney.md)
instructor-configured agents.

## Open questions

- [ ] Which base models, and what did fine-tuning actually buy over prompting?
- [ ] What is "preference-aligned" here — DPO? RLHF on TA judgments? On what data?
- [ ] Usage numbers and retention from Spring 2025
- [ ] Did the guardrails hold under pressure? Any measured defection?
- [ ] What broke when scaling from one course to several?

> The PDF did not text-extract cleanly. Everything above is from the abstract and search
> summaries. **Needs a proper read.**

## Connects to

- [CS50 Duck](cs50-duck.md) — same "won't spoil the answer" commitment, much larger scale
- [Stan](stan-udel.md) — same course-tutor pattern, our domain
- [guardrails](../concepts/guardrails.md) — PeteChat is a guardrail design case study
- [Cogniti](cogniti-sydney.md) — the alternative: don't build a tutor, build a tutor factory

## Sources

- ["Tutor, Not Solver: Designing a Guardrailed AI Assistant for Learning in Higher Education: A Design Case of PeteChat," arXiv:2606.09845](https://arxiv.org/pdf/2606.09845) `[skimmed]` — PDF cached locally
