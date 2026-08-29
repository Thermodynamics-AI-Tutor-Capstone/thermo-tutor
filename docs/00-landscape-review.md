# Landscape Review — AI Tutoring, as of August 2026

Status: **first pass.** Assembled from literature search, not yet from hands-on use.
Every claim about a product below needs to be re-verified by our own teardown
(`research/competitive-teardown/`) before it goes in a report.

---

## Tier 1 — General chatbots with a "study mode"

All three major labs shipped a pedagogical mode in 2025.

| Product | Mode | Observed behavior |
|---|---|---|
| ChatGPT | Study Mode | Self-corrects mid-solution ("let me re-check that step"), which reviewers rate as genuinely useful for learning. But it is *trigger-happy* — reviewers report it explains everything upfront without waiting for the student to attempt anything or asking what the student is trying to learn. |
| Gemini | Guided Learning | The only one reviewers found approached an uploaded document from a step-by-step teaching angle; good at contextualizing and generating scaffolding exercises. Loses focus over longer sessions, and its "teacher" stance can read as patronizing. |
| Claude | Learning Mode | Rated most "teacher-like" — explains *why* something is weak and offers alternatives. Reported to shorten revision time. |

**The structural point.** All three are a system prompt, not an architecture. They share
the same four gaps for our use case:

- No model of the specific course — syllabus, notation, which chapter you're in, what
  your instructor actually assigned.
- No persistent model of what this student knows. Every session starts cold.
- No ground truth for property data. The model recalls steam-table values from weights.
- **No defense against the student defecting.** "Just give me the answer" ends the
  pedagogy, because the pedagogy is only a request.

That last one is the single most important observation in this document. See
`01-key-findings.md` §1.

---

## Tier 2 — Homework answer engines

Chegg, Numerade, Symbolab, Wolfram Alpha, Photomath, Gauth, Course Hero.

Answer machines by design and by business model. Relevant to us in three ways:

1. They are the **actual competition** for a student's attention at 11pm the night
   before a problem set is due. Any honest evaluation has to compare against them on
   convenience, not just on pedagogy.
2. They're the baseline for "what happens with no learning support at all."
3. Understanding *why* students choose them tells us more about tutor design than any
   amount of pedagogical theory. This is a core interview question.

## Tier 2.5 — The incumbents nobody lists

Underrated and specific to our domain. A Penn State thermo student is far more likely to
be using one of these than Khanmigo:

- **Pearson Mastering Engineering** — hint-based homework with graded steps.
- **McGraw Hill Connect / SmartBook** — publisher of Cengel & Boles, the most common
  US undergrad thermo text. Has adaptive-recall features that predate LLMs.
- **WileyPLUS** — publisher of Moran & Shapiro.
- **EES (Engineering Equation Solver)** — not a tutor, but the tool many thermo courses
  actually require. Worth understanding what it does and doesn't teach.

These have a decade of adaptive-learning telemetry behind them. If we're claiming to
improve on the status quo, the status quo is *this*, not ChatGPT.

---

## Tier 3 — Purpose-built course tutors

This is the real comparison class — the systems doing what we've been asked to do.

### Harvard PS2 Tutor (Kestin, Miller, Klales, Milbourne, Ponti)
*Scientific Reports*, June 2025. Physical Sciences 2, Fall 2023.

The strongest existing evidence that this can work:

- 194 students, RCT, within-subject alternating design (students switched weekly between
  an active-learning classroom and the AI tutor at home).
- **Roughly 2× the learning gains** of the active-learning classroom condition.
- Students spent *less* time on the content.
- Higher self-reported engagement, motivation, and satisfaction.

Design notes worth stealing: expert-authored scaffolds (not generic prompts),
enforced step-by-step reasoning, explicit anti-hallucination guardrails.

Note carefully: they beat active learning, which is itself the well-evidenced gold
standard. This is a high bar and a fair one. It also means the comparison condition
matters enormously — beating a lecture is not the same claim.

### Stan — University of Delaware, ChemE thermodynamics
The closest direct competitor to our brief. Deployed Fall 2025.

- Local open-weight models via Ollama (offline-capable — a deliberate privacy choice).
- RAG over course materials, specifically Sandler's *Chemical Engineering
  Thermodynamics*.
- Socratic prompting with explicit refusal to solve problems outright.
- Voice interface: Faster-Whisper for STT, Silero VAD.
- Delivered through a Sphinx/Jupyter interface.

Reported limitations: failure modes on complex problem types, and constrained model
reasoning on multi-step thermodynamic calculations.

**Action item:** this is the paper to read in full and, if possible, the team to email.
Same subject, same year, same idea. We should know exactly how our approach differs
before we claim novelty.

### Khanmigo — Khan Academy
The largest real-world deployment. Two lessons, both painful and both useful.

**Lesson 1 — LLMs are unfit for math out of the box.** Khan's own writeup: generative AI
"generates a probable next number rather than executing a correct calculation." They
built a separate dedicated math agent that verifies calculations and checks expressions
in real time, and they track math error rate as a guardrail metric.

**Lesson 2 — engagement is the real failure mode, not quality.** From a two-year school
study (2026): access was nearly universal, engagement was thin. **96% of students tried
Khanmigo at least once. The median student messaged it on only a third of the days they
practiced, and in only 17% of practice sessions.** Students using Khan Academy still made
faster math gains than comparison — but the tutor itself was largely unused.

We should treat "will students voluntarily use this more than twice" as a primary
research question, not an afterthought. It is the question Khanmigo lost on.

---

## What nobody appears to have built

Gaps that would make our project a contribution rather than a re-implementation:

1. **A thermodynamics-specific tutoring benchmark.** MathTutorBench exists for math
   (EMNLP 2025). Nothing equivalent for engineering thermo.
2. **A tutor whose pedagogical policy lives outside the prompt.** Every system reviewed
   here encodes "be Socratic" as an instruction to the model. The discourse research
   (§1 of key findings) suggests that's exactly why it fails.
3. **Longitudinal per-concept mastery tracking tied to a real course's assignment
   stream.** Publisher platforms do adaptive recall; LLM tutors do conversation. Nobody
   found doing both against a live Canvas course.
4. **Honest reporting on voluntary usage decay.** Almost all published tutor evaluations
   are of mandatory or incentivized use.

Whether we build any of it is a later decision. Knowing the gaps is this phase's job.

---

## Sources

See `docs/02-bibliography.md` for the annotated list with links.
