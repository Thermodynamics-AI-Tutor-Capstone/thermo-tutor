# Knowledge Tracing

**Type:** concept
**One line:** Estimating what a student knows, per skill, from their history of correct and
incorrect responses.
**Why we care:** This is the machinery behind "track learning over time" in our brief.

> **Substantially rewritten 2026-08-31 after reading the primary literature.** This node
> previously claimed our data volume made BKT unworkable and that BKT has an
> "identifiability problem." **Both were wrong**, and the corrections change our design in a
> good direction. Marked ⚠ below.

## The family

**BKT — Bayesian Knowledge Tracing.** Corbett & Anderson, *User Modeling and User-Adapted
Interaction* 4:253–278, **1995**. A per-skill two-state HMM. Their exact definitions:

| Parameter | Corbett & Anderson's wording |
|---|---|
| **p(L₀)** *Initial Learning* | *"the probability a rule is in the learned state prior to the first opportunity to apply the rule"* |
| **p(T)** *Acquisition* | *"the probability a rule will make the transition from the unlearned to the learned state following an opportunity to apply the rule"* |
| **p(G)** *Guess* | *"the probability a student will guess correctly if a rule is in the unlearned state"* |
| **p(S)** *Slip* | *"the probability a student will slip (make a mistake) if a rule is in the learned state"* |

Mastery criterion in the original: **p(L) = 0.95**.

**No forgetting — confirmed verbatim:**
> *"There is no forgetting; rules do not make the transition in the other direction."*

Over a 15-week course that omission matters. → [spaced repetition](spaced-repetition.md)

**DKT — Deep Knowledge Tracing.** Piech et al., NeurIPS 2015. LSTM over the response
sequence. **SAKT and attention-based KT** followed.

## ⚠ Correction 1: our data volume is fine — we were counting the wrong thing

This node previously reasoned: ~90 knowledge components × ~300 interactions per semester =
~3 observations per component, therefore BKT cannot estimate anything. **That conflates two
different counts and reaches the wrong conclusion.**

**BKT parameters are never fit per student.** The canonical design (Corbett & Anderson §4.4)
is a three-level split:

| Level | What it is | How many numbers | Fit from |
|---|---|---|---|
| **1. Per-skill parameters** | p(L₀), p(T), p(G), p(S) per KC | 4 × 90 = **360** | **Pooled cohort data** |
| **2. Per-student weights** | one scalar per parameter *type* | **4 per student**, not per skill | That student's ~300 observations |
| **3. Per-student-per-skill state** | p(L) | — | **Not fitted at all** — a forward Bayesian update at inference |

Level 3 is the number our tutor actually uses, and it requires *no estimation* — just the
observations themselves. Level 2 needs 4 numbers from ~300 observations, which is
comfortable. Only Level 1 needs volume, and it pools across every student.

**And our per-student density is not thin — it is unusually good:**

| Dataset | Observations per student **per skill** |
|---|---|
| Assistments-09 | 0.27 |
| Khan Math | 0.44 |
| Assistments-14 | 0.34 |
| KDD Cup Algebra 2005-06 | 3.22 |
| **Our estimate** | **~3.3** |

We are ~10× denser per student than the datasets the entire field benchmarks on, and
essentially identical to the KDD Cup Algebra set.

**The identifiability threshold is three.** Doroudi & Brunskill (EDM 2017), via the HMM
method of moments: *"as long as we have more than two observations per student, BKT models
with reasonable parameters are identifiable and there is a single global maximum to the
likelihood function."* We sit exactly on that line — identifiable in principle, with no
margin.

**What we actually lack is cohort volume.** The benchmark datasets carry 1,851–20,797 *pooled*
observations per skill. At 300 interactions × N students ÷ 90 KCs, we need **N ≈ 100 students
for ~333 pooled observations per KC**; a 30-student section gives ~100.

**So the real levers are cohort size, pooling across semesters, and — most cheaply —
coarsening the skill graph.** See [knowledge components](knowledge-components.md), where the
comparison numbers are sobering.

## ⚠ Correction 2: the "identifiability problem" is a misdiagnosis. The real risk is degeneracy

The famous Beck & Chang (2007) claim that BKT is unidentifiable **does not survive scrutiny**.
Doroudi & Brunskill show their three "equally good" models agree only on *marginal, a-priori*
curves computed with **no data conditioned on**; conditioned on an actual response sequence
they diverge sharply. Van de Sande puts it flatly: *"The 'Identifiability Problem' for the
Knowledge Tracing Algorithm does not exist, so long as there are both correct and incorrect
steps."*

**Three things get conflated under that label. Only the third is real:**

1. **A-priori prediction ambiguity** — vanishes once you condition on data. Harmless.
2. **Multiple local optima in EM** — real, and trivially fixed. **At four parameters, a
   brute-force grid search at 0.01 resolution is affordable for all 90 KCs.** Do that, or use
   many EM restarts, and this is closed.
3. **Semantic degeneracy** — *"the model parameters that best fit the data are inconsistent
   with the conceptual assumptions underlying BKT."* This is the one to design against.
   - *Theoretical degeneracy*: p(G) > 0.5 or p(S) > 0.5
   - *Empirical degeneracy*: mastery estimate **decreases** after n correct answers, or fails
     to exceed 0.95 after m correct
   - (a) is provably equivalent to **p(G) + p(S) > 1**

**The finding that should shape our implementation:** degeneracy is a **model-misspecification**
problem, not a data-volume problem — and *its form depends on sequence length*. Fitting BKT to
data generated by a true graded-mastery process:

| | 20 observations/student | 200 observations/student |
|---|---|---|
| p(G) | 0.27 | **0.49** |
| p(S) | **0.44** | 0.13 |

> *"varying the number of observations can lead to different forms of degeneracy!… we believe
> [this is] **not the result of not having enough data (students) to fit the models well**, but
> rather the result of the mismatch between the true form of student learning and the model we
> are using."*

**Thermodynamics mastery is almost certainly graded, not binary** — a student partially grasps
entropy generation before fully grasping it. And we are in the *short-sequence* regime, where
the predicted failure mode is **inflated slip (~0.44)**: the model concludes that students who
*have* mastered a KC keep getting it wrong. The named practical harm is that such a model
*"will likely give far fewer problems to the student than they actually need in order to reach
mastery."*

**Concrete guards to build in from day one:**
- Reject any fit with **p(S) > 0.4** or **p(G) + p(S) > 1**
- Use Dirichlet priors (this, correctly understood, is Beck & Chang's real contribution)
- Consider Baker's contextual guess/slip estimation
- Grid-search the 4-parameter space rather than trusting a single EM run

## What actually beats what — the honest comparison

**BKT vs. LSTM** (Mao, Lin & Chi, *JEDM* 2018) — and note the datasets are small and one is
**physics**:

| Dataset | Students | Items | Expert KCs |
|---|---|---|---|
| **Cordillera (physics)** | 169 | 1,187 | **7** |
| Pyrenees (probability) | 475 | 176 | **10** |

Post-test RMSE (lower better): **BKT 0.147** vs LSTM 0.183 on Cordillera; BKT+SK **0.159** vs
LSTM+SK 0.180 on Pyrenees. **BKT beat the LSTM on post-test prediction on both**, and BKT+SK
reached full accuracy using only the *earliest 50%* of each student's sequence. The LSTM won
only on *learning-gain* prediction.

That is a small-data, physics-domain result where the interpretable model wins. It is the
best single argument for starting with BKT.

**But BKT is weak at next-answer prediction, and a simpler model beats it.** From BKT-LSTM
(Minn 2021), AUC across three large datasets:

| Model | Algebra 05-06 | Assist-09 | Assist-14 |
|---|---|---|---|
| BKT | 0.65 | 0.61 | 0.64 |
| **BIRT** (plain Bayesian IRT, *no temporal model*) | **0.75** | 0.67 | **0.81** |
| DKT | 0.72 | 0.70 | 0.78 |
| BKT-LSTM | 0.80 | 0.71 | 0.85 |

➕ **New and worth taking seriously: a static IRT model with no knowledge tracing at all beat
BKT on every benchmark.** If our goal were predicting the next answer, BKT would be a poor
choice. Our goal is an *interpretable per-skill mastery number that drives pedagogical
decisions* — which is what BKT buys and IRT does not. But **IRT is the baseline we should
actually have to beat**, and reporting it would strengthen any claim we make.

Piech et al.'s own numbers reinforce the caution: BKT beat the marginal baseline by only
**0.05 AUC** on Khan and Assistments, and *lost* to it on simulated data.

## Recommendation for us

**Start with BKT**, on this reasoning rather than the reasoning this node used to give:

- Four interpretable parameters that can be defended in a capstone presentation
- The three-level fitting design solves our data problem, and our per-student density is
  above field norms
- It wins on post-test prediction in small-data physics settings (Cordillera)
- A working reference implementation exists in [OATutor](../systems/oatutor-berkeley.md)

**Add these, which the earlier version of this node did not know to require:** degeneracy
guards, grid-search fitting, an **IRT baseline**, and a plan to coarsen the graph if pooled
cohort volume per KC lands below ~300.

## Open questions

- [ ] Run the pooled-volume arithmetic against the *actual* course enrollment.
- [ ] Can conversation turns count as evidence, or only graded attempts? (Eases the data
      problem; worsens the validity problem.)
- [ ] Forgetting over 15 weeks — BKT has no mechanism.
      → [spaced repetition](spaced-repetition.md)
- [ ] How do we detect graded rather than binary mastery in our own data, given that
      misspecification is the real risk?

## Connects to

- [knowledge components](knowledge-components.md) — the grain decision, now much better informed
- [ALEKS](../systems/aleks.md) — the competing formalism, and our prerequisite graph is already its input
- [OATutor](../systems/oatutor-berkeley.md) — working open-source BKT
- [spaced repetition](spaced-repetition.md) — the forgetting half
- [Cognitive Tutor](../systems/cognitive-tutor.md) — where BKT came from

## Sources

- **Corbett & Anderson (1995), "Knowledge Tracing: Modeling the Acquisition of Procedural Knowledge," *UMUAI* 4:253–278** `[read — pp. 253–258, 260–264, 267–271 of 26; visual read of a text-layer-free scan]` — the canonical source for the four parameters, no-forgetting, and cohort fitting
- [Mao, Lin & Chi, "Deep Learning vs. Bayesian Knowledge Tracing," *JEDM* 10(2) 2018](https://files.eric.ed.gov/fulltext/EJ1195512.pdf) `[read]` — BKT beats LSTM on post-test prediction; Cordillera physics dataset. **Contains no LLM comparison** — do not cite it for that.
- [Minn, "BKT-LSTM," arXiv:2012.12218](https://arxiv.org/pdf/2012.12218) `[read]` — the AUC table, including BIRT
- [Piech et al., "Deep Knowledge Tracing," NeurIPS 2015, arXiv:1506.05908](https://arxiv.org/abs/1506.05908) `[read]`
- [Doroudi & Brunskill, "The Misidentified Identifiability Problem of Bayesian Knowledge Tracing," EDM 2017](https://files.eric.ed.gov/fulltext/ED596611.pdf) `[read]` — **the correction**; identifiability threshold and the degeneracy-by-sequence-length result
- [van de Sande, "Properties of the Bayesian Knowledge Tracing Model," *JEDM* 5(2) 2013](https://files.eric.ed.gov/fulltext/EJ1115329.pdf) `[read]` — the p(G)+p(S)>1 constraint surface
- [Bhattacharyya et al., "Specialised KT Models Outperform LLMs," arXiv:2603.02830](https://arxiv.org/abs/2603.02830) `[read]` — **this** is the source of the KT-vs-LLM figures (73% vs 58–66%), from Eedi
- Beck & Chang (2007) — paywalled, no OA location; covered secondhand via Doroudi & Brunskill, which reproduces its parameters and quotes its central claim
