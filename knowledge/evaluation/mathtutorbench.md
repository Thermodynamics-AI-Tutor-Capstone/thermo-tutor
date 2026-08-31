# MathTutorBench and the pedagogy benchmarks

**Type:** benchmark
**One line:** A benchmark for *teaching ability* rather than subject knowledge — and the
finding that the two trade off against each other.
**Why we care:** It's the methodological template for the thermodynamics **pedagogy**
benchmark that doesn't exist, which is now our clearest novel contribution.

> **Verification: `[read]` — full text, 2026-08-31.**

## MathTutorBench

Jakub Macina, Nico Daheim, Ido Hakimi, **Manu Kapur**, Iryna Gurevych, Mrinmaya Sachan —
ETH Zurich (CS + ETH AI Center + Professorship for Learning Sciences), with TU Darmstadt's
UKP Lab. **EMNLP 2025 (oral).** [Code](https://github.com/eth-lre/mathtutorbench).

*(Note: **Manu Kapur**, the [productive failure](../concepts/productive-failure.md)
researcher, is a co-author. That's a direct route into the literature that is our biggest
remaining gap.)*

**Seven tasks across three axes:**

| Axis | Tasks | Dataset | Instances |
|---|---|---|---|
| **Math expertise** | Problem solving; Socratic questioning | GSM8k | 1,319 each |
| **Student understanding** | Solution correctness; mistake location; mistake correction | StepVerify | 2,004 / 2,004 / 1,002 |
| **Teacher response generation** | Scaffolding generation + pedagogical instruction following, standard and `[hard]` | MathDial + Bridge | 1,150 / 327 |

The `[hard]` variant simply uses a **longer conversation history** (avg. 5.78 turns vs.
3.08) — and that alone separates models, see below.

Their stated pedagogical principles, drawn from effective-teaching research: **(a)
correctness** — guide to the right answer without stating incorrect facts; **(b) scaffolding
instead of giving away the answer**; **(c)** encouraging cognitive engagement.

Scoring the open-ended axis is the clever part: they train a **reward model to discriminate
expert from novice teacher responses**, and use it as judge.

**Critically — generic LLM-as-judge does not work here.** They tried prompting
Llama-3.1-70B-Instruct and GPT-4o-mini with detailed pedagogical guidelines and got
**accuracy below 0.7**; off-the-shelf RewardBench reward models were barely better on
pedagogical preferences. **If we build a thermodynamics pedagogy benchmark, "just ask GPT to
judge it" is not a viable methodology.** That's an expensive lesson to learn late.

## The headline finding

> **Subject expertise does not translate into good teaching.** Pedagogy and subject expertise
> form a trade-off, navigated by how tutoring-specialized the model is.

Their sharper phrasing: *"high problem-solving accuracy often means that the LLM lacks
pedagogy."*

**Two further findings that matter more for design than the headline:**

**1. General models degrade pedagogically as the conversation goes on.** *"More specialized
tutoring models tend to retain their teaching abilities even further into a dialog with a
student, while general models quickly become worse."* This is why the `[hard]` split exists,
and it is a direct warning about our architecture: a frontier model with a good system prompt
may tutor well for three turns and poorly by turn eight. **Multi-turn degradation should be
something we actively test, not assume away.**

**2. Specialization costs subject ability.** SocraticLM (Qwen2.5-Math base) gained strongly
on scaffolding for its size — and **degraded on all Student Understanding tasks**. You cannot
currently have both. Given [TutorGym's](tutorgym.md) finding that no model reliably spots an
incorrect step, trading *away* student-understanding ability is a bad trade for us.

This is the empirical backbone of the argument running through this whole knowledge base:

- [o3 aces a thermodynamics exam](../domain/superstudent-thermodynamics.md) and that tells us
  nothing about whether it can teach thermodynamics
- A better base model is not automatically a better tutor, and may be worse
- **Model capability is not our lever.** Architecture and domain work are.
  → [grounding and verification](../concepts/grounding-and-verification.md)

## MRBench and the BEA shared task

**MRBench** — from *"Unifying AI Tutor Evaluation: An Evaluation Taxonomy for Pedagogical
Ability Assessment of LLM-Powered AI Tutors"* (arXiv:2412.09416). Built from **MathDial** and
**Bridge**. Each instance is a partial tutor-student conversation **cut at the moment the
student errs or shows confusion** — then you evaluate what the tutor says next.

That construction is the key idea and it's directly portable: **the interesting moment in
tutoring is the turn right after a mistake.** Everything before it is chat.

**BEA 2025 Shared Task** — pedagogical ability assessment of AI tutors, at the 20th Workshop
on Innovative Use of NLP for Building Educational Applications. A community-scale effort with
published systems, e.g. retrieval-augmented prompting for mistake identification
(arXiv:2506.10627).

Also in this space: **AITutor-EvalKit** (arXiv:2512.03688), **TutorGym** (arXiv:2505.01563 —
a testbed for LLM agents as both tutors and simulated students), and
*"The Missing Evaluation Axis: What 10,000 Student Submissions Reveal About AI Tutor
Effectiveness"* (arXiv:2605.05648).

## Why this is our opening

Correctness in thermodynamics is now well covered — [ThermoQA](../domain/thermoqa.md) and
[UTQA](../domain/utqa.md) between them.

**Nothing measures thermodynamics tutoring *quality*.** The MathTutorBench axes don't exist
for our domain.

Constructing one is well-suited to a capstone:

1. **Collect real student errors.** From the course's actual submissions, or from our own
   think-aloud sessions. → [interview protocol](../../research/student-interviews/protocol-draft.md)
2. **Cut conversations at the error**, MRBench-style.
3. **Have thermodynamics instructors and experienced TAs write the expert next turn.**
4. **Score candidate tutor responses** by expert preference — the
   [CS50 TF pairwise-comparison method](../systems/cs50-duck.md) — and/or a trained reward
   model as MathTutorBench does.

Note what this needs: instructors and TAs, not students. **The expert-judgment portion has a
much lighter IRB path than student-facing work**, so it can run while the student protocol is
still in review. → [roadmap](../../admin/roadmap.md)

## Open questions

- [ ] Is the MathTutorBench reward model reusable across domains, or maths-specific?
- [ ] How many expert-authored turns are needed for a usable benchmark? (Cost driver.)
- [ ] Can we get MathDial/Bridge and study the annotation scheme directly?
- [ ] Would the ETH group advise us? They've solved the methodology once already.
- [ ] Does TutorGym provide infrastructure we could reuse rather than rebuild?

## Connects to

- [ThermoQA](../domain/thermoqa.md) — covers correctness; leaves pedagogy open
- [Superstudent](../domain/superstudent-thermodynamics.md) — expertise ≠ pedagogy, dramatized
- [LearnLM](../systems/learnlm.md) — the other pedagogy-measurement tradition
- [CS50 Duck](../systems/cs50-duck.md) — the practical expert-comparison method
- [concept inventories](concept-inventories.md) — measuring the *student*, not the tutor

## Sources

- [MathTutorBench, arXiv:2502.18940](https://arxiv.org/abs/2502.18940) `[skimmed]` · [code](https://github.com/eth-lre/mathtutorbench) `[found]`
- [Unifying AI Tutor Evaluation (MRBench), arXiv:2412.09416](https://arxiv.org/html/2412.09416v1) `[skimmed]`
- [NeuralNexus at BEA 2025 Shared Task, arXiv:2506.10627](https://arxiv.org/pdf/2506.10627) `[found]`
- [AITutor-EvalKit, arXiv:2512.03688](https://arxiv.org/pdf/2512.03688) `[found]`
- [TutorGym, arXiv:2505.01563](https://arxiv.org/pdf/2505.01563) `[found]`
- [The Missing Evaluation Axis, arXiv:2605.05648](https://arxiv.org/pdf/2605.05648) `[found]`
