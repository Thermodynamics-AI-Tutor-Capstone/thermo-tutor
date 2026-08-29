# Knowledge Tracing

**Type:** concept
**One line:** Estimating what a student knows, per skill, from their history of correct and
incorrect responses.
**Why we care:** This is the machinery behind "track learning over time" in our brief, and
the evidence is unambiguous that it should **not** be done by an LLM.

## The family

**BKT — Bayesian Knowledge Tracing.** From the [Cognitive Tutor](../systems/cognitive-tutor.md)
lineage (Corbett & Anderson). A per-skill hidden Markov model with four parameters:

| Parameter | Meaning |
|---|---|
| **P(L₀)** | prior — probability the student already knew it |
| **P(T)** | learn — probability of acquiring it at each opportunity |
| **P(G)** | guess — probability of answering right without knowing |
| **P(S)** | slip — probability of answering wrong while knowing |

Four numbers, all interpretable, forty years of use. Its limits are real: it models skills
independently, handles non-linear progression poorly, and classic BKT has **no forgetting**
— which for a semester-long course is a significant omission.
→ [spaced repetition](spaced-repetition.md)

**DKT — Deep Knowledge Tracing.** Piech et al. (2015). An LSTM over the response sequence.
Captures cross-skill dependencies BKT can't. Better fit, much worse interpretability.

**SAKT and attention-based KT.** Transformer self-attention over response sequences; state
of the art on standard KT benchmarks. Also GNN-based variants that use a skill graph
directly — potentially interesting given
[ours](../../research/domain/skill-graph-draft.md).

## The settled question: don't use an LLM for this

*Faster, Cheaper, More Accurate: Specialised Knowledge Tracing Models Outperform LLMs*
(arXiv:2603.02830) tested specialized KT models against GPT-3.5/4 on standard benchmarks.
Specialized models won on **accuracy and AUC**, at **millisecond latency**, at **orders of
magnitude lower cost per prediction**.

Which settles a design question cleanly: **the LLM converses; a statistical model owns
mastery state.** Asking the model "how well does this student understand entropy?" is
worse, slower, more expensive, and — because it's non-deterministic — unpublishable.

## The recommendation for us

**Start with BKT.** Not because it's best, but because for a capstone:

- Four interpretable parameters you can defend in a presentation
- Works with small data — and we will have small data
- Every result is explainable to an instructor, which matters for adoption
- A working reference implementation exists in
  [OATutor](../systems/oatutor-berkeley.md)

Add DKT as a comparison arm if time allows. That comparison is itself a legitimate
capstone result.

## The problem nobody has solved for us: data volume

BKT needs multiple observations per knowledge component per student to estimate anything.

Our [draft skill graph](../../research/domain/skill-graph-draft.md) has ~90 components. If a
semester produces roughly 300 graded interactions per student, that's ~3 observations per
component. **BKT cannot say anything useful from 3 observations.**

Three ways out, none free:
1. **Coarsen the grain.** ~25 components instead of ~90. Loses diagnostic precision.
2. **Pool across students.** Fit parameters on the cohort, track state per student. Standard
   practice, and it's what makes BKT work at all with limited data.
3. **Use the prerequisite structure.** [Knowledge space theory](../systems/aleks.md) gets
   leverage from the graph itself, needing far fewer observations per component. This may be
   the right answer and it is worth investigating before committing to BKT.

**Run the arithmetic before finalizing the skill graph.**
→ [open question C2](../../docs/03-open-questions.md)

## Open questions

- [ ] How many graded interactions does a PSU thermo student actually produce in a semester?
- [ ] Does KST beat BKT at our data volume? Empirical question, answerable.
- [ ] Can conversation turns count as evidence, or only graded attempts? (If dialogue can
      update the student model, the data problem eases substantially — and the validity
      problem gets much harder.)
- [ ] How to handle forgetting over a 15-week course? BKT has no mechanism.
      → [spaced repetition](spaced-repetition.md)

## Connects to

- [knowledge components](knowledge-components.md) — the unit being traced
- [ALEKS](../systems/aleks.md) — the competing formalism
- [OATutor](../systems/oatutor-berkeley.md) — working open-source BKT
- [spaced repetition](spaced-repetition.md) — the forgetting half of the problem
- [Cognitive Tutor](../systems/cognitive-tutor.md) — where BKT came from

## Sources

- [Faster, Cheaper, More Accurate: Specialised KT Models Outperform LLMs, arXiv:2603.02830](https://arxiv.org/pdf/2603.02830) `[skimmed]`
- [Bayesian Knowledge Tracing overview](https://www.emergentmind.com/topics/bayesian-knowledge-tracing) `[skimmed]`
- [Deep Learning vs. Bayesian Knowledge Tracing: Student Models for Interventions, JEDM 2018](https://eric.ed.gov/?id=EJ1195512) `[found]`
- [BKT-LSTM, arXiv:2012.12218](https://arxiv.org/pdf/2012.12218) `[found]`
- Piech et al., Deep Knowledge Tracing (NeurIPS 2015) `[found]`
