# LLM-as-judge — four independent findings that it doesn't work for education

**Type:** evaluation
**One line:** Across four unrelated studies, models judge *educational quality* badly — rubric
grading agreement of **κ = 0.128**, pedagogical-preference accuracy **below 0.7**, expert-label
agreement of **κ = 0.44–0.65** — while judging *behavioural uptake* well (**κ = 0.80–1.00**).
**Why we care:** "Have GPT score it" is the default evaluation plan for a capstone. It is the
wrong plan, and the evidence against it is now overwhelming and cheap to cite.

---

## The four findings

| Study | Task | Agreement / accuracy |
|---|---|---|
| **[ASEE 2026 rubric grading](https://peer.asee.org/59260.pdf)** | Grade student papers against a course rubric | ⚠ **Cohen's κ = 0.128** (poor), **Krippendorff's α = 0.17** (slight) |
| **[MathTutorBench](mathtutorbench.md)** | Prefer expert over novice tutor response | **< 0.7 accuracy**; off-the-shelf reward models "barely better than random" |
| **[Niousha et al.](behavioral-evaluation.md)** | Label feedback on pedagogical dimensions | **κ = 0.65 and 0.44** vs 0.76 human–human |
| **[Ethel](../systems/ethel-eth.md)** | Grade a 252-student thermodynamics exam | High precision, **~50% recall** on passing solutions |

**And the contrast that makes it actionable** — the same paper that found κ = 0.44 on pedagogical
labels found **κ = 0.80–1.00** on *"did this feedback change the student's next submission, and
was the change correct?"*

> **Models are unreliable at judging whether tutoring was good, and reliable at judging whether a
> student acted on it.** Design the evaluation around the second question.

## ⚠ The grading study is worth reading closely, because the authors expected the opposite

*"Adoption of Large Language Model for Improving Grading Timing in an Engineering Course"*
(ASEE 2026, read in full 2026-09-01). Two instructors graded student papers independently, then
**normed** their ratings against each other to produce an agreed human standard. A custom GPT was
then primed with **rubric-derived reference responses** — a deliberate effort to raise reliability
— and scored the same papers on a 0–4 rubric with instructions to *"evaluate it strictly using the
rubric below. Do not invent additional criteria."*

**They preregistered an expectation of κ > 0.6. They got 0.128.**

This is not a naive prompt. It is a normed human baseline, a course-specific rubric, seeded
reference answers, and explicit anti-drift instructions — the full set of mitigations a careful
team would apply — and agreement was still poor.

**Two secondary findings:**

- ⚠ **The model grades harsher than faculty.** *"For the most part, the faculty evaluators are more
  likely to rate a student's work higher on the rubric than the AI is."* A systematic bias, not
  just noise — which matters, because a harsh grader is the kind of error students notice and
  resent.
- **It was still useful.** *"Though the expected improvement in reliability was not achieved, the
  LLM's usability for feedback purposes did prove to be advantageous to the instructor,"* and their
  prior work found significant time savings. **Draft feedback, yes. Assign a score, no.**

## What follows for us

1. **Do not evaluate our tutor with an LLM judge on pedagogical quality.** Four studies say the
   number would be meaningless. If a reviewer asks, this node is the citation.
2. **Use human raters on a sample, and report inter-rater reliability.** The
   [ASEE 2026 deployment](../systems/rag-tutor-southeast.md) hand-audited 260 of 27,242
   interactions — under 1% — because evaluator time is the binding constraint. That is the honest
   scale, and it is achievable.
3. **Make behavioural uptake the automated metric.** RelScore and SuccScore are cheap, reliable,
   and retrospective over logs we should be keeping anyway.
   → [behavioral evaluation](behavioral-evaluation.md)
4. **If we use a model for grading at all, use it as triage.** [Ethel's](../systems/ethel-eth.md)
   shape — trust the confident passes, route everything else to a human — is the only defensible
   deployment of an automated grader in this evidence base.
5. ⚠ **Watch for this in others' claims.** Any paper reporting tutoring quality scored by a model
   is reporting a number these four studies say is unreliable. That includes the pedagogical-quality
   half of several systems in [`systems/`](../systems/).

## ⚠ What this does *not* say

Models are fine at judging things with a checkable answer — numerical correctness against a
solver, whether a citation supports a claim, whether an edit was applied. The failure is specific
to **judgements requiring pedagogical expertise**, which is exactly where human raters are
expensive and the temptation to automate is strongest.

## Open questions

- [ ] Does agreement improve with a *reasoning* model rather than a chat model? None of the four
      studies used one, and all predate widespread reasoning-model use for judging.
- [ ] Would a fine-tuned judge work? [MathTutorBench trained a reward model](mathtutorbench.md)
      specifically because prompting failed, and reported it usable. That is the one positive
      signal here and it needs training data we would have to build.
- [ ] Is the harsh-grading bias consistent across rubrics and models? One study, one course.

## Connects to

- [Behavioral evaluation](behavioral-evaluation.md) — what models *can* judge reliably
- [MathTutorBench](mathtutorbench.md) — the reward-model alternative
- [Ethel](../systems/ethel-eth.md) — grading as triage
- [The deployed RAG + SRL tutor](../systems/rag-tutor-southeast.md) — human audit at <1% scale
- [Concept inventories](concept-inventories.md) — what a validated human instrument buys you

## Sources

- ["Adoption of Large Language Model for Improving Grading Timing in an Engineering Course," *ASEE 2026*](https://peer.asee.org/59260.pdf) `[read — full text, 12 pp., 2026-09-01]`
- [Macina et al., MathTutorBench, arXiv:2502.18940](https://arxiv.org/abs/2502.18940) `[read]`
- [Niousha et al., arXiv:2605.05648](https://arxiv.org/pdf/2605.05648) `[read]`
- [Kortemeyer, "Ethel," arXiv:2407.19452](https://arxiv.org/pdf/2407.19452) `[read]`
