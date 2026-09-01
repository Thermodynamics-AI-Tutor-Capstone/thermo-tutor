# The RAG + SRL engineering tutor (large southeastern public university)

**Type:** system
**One line:** A deployed, RAG-grounded, Self-Regulated-Learning-scaffolded AI tutor in two
undergraduate engineering courses — **27,242 real interactions, 116 users, Fall 2025** — and the
closest thing to our proposed system that anyone has actually shipped and measured.
**Why we care:** Everything else in this base is either a benchmark, a prototype, or a different
discipline. This is a full deployment in engineering, with usage curves, a quality audit, and
honest effect sizes. **It is the best available preview of what our Phase 2 looks like.**

> **Verification: `[read]` — full text, 26 pp., 2026-09-01.**

*"Leveraging RAG-Enhanced LLMs for Engineering Education: Design and Evaluation."*
**ASEE 2026** ([peer.asee.org/59993.pdf](https://peer.asee.org/59993.pdf)). A large public
research-intensive institution in the southeastern United States. **IRB-approved.**

## What they built — three modes, not one chatbot

The design commitment is that LLMs *"often fall short of engineering pedagogical standards due to
hallucination and misalignment with core instructional principles,"* so they add **RAG for
accuracy** and **a pedagogical control layer** on top. Explicitly grounded in **Self-Regulated
Learning** theory, on the reasoning that *"current LLMs often fail to support SRL, as they tend to
provide direct answers rather than scaffolding."*

| Mode | What it does | Circuit Analysis | Signal Processing |
|---|---|---|---|
| **Solution feedback** | Critiques the student's own work | 67 | 15 |
| **Guided support (SRL)** | Problem-specific scaffolding | **76** | **37** |
| **Open-ended Q&A** | Free questions | 30 | 35 |

**Separating the modes is the design idea worth stealing.** It makes "check my work" a different
interaction from "explain this," which is exactly the distinction
[a UIC student described as their ideal workflow](../evidence/student-ai-perceptions-2025.md).
Note that **guided support was the most-used mode in both courses** — students did opt into
scaffolding when it was offered as a distinct choice rather than buried behind a hint button.
That is a meaningful counterweight to
[PeteChat's 0% hint utilisation](petechat-purdue.md): **framing, not appetite, may be the problem.**

## Deployment reality

- **Circuit Analysis: 72 of 113 students (64%)** used it. **Signal Processing: 44 of 166**, but
  capped at 50 accounts, so **44/50 = 88% of available slots.**
- **27,242 interactions** (15,809 + 11,433), where an interaction is one question-answer dyad.
- Circuit Analysis users averaged **34.3 unique problems** and a **52.5-day** span; Signal
  Processing **17.9 problems**, **48.9 days**.

### ⚠ Two usage patterns we should design around

**1. The novelty curve is real and it has a floor.** *"A classic 'novelty effect'. Both courses
see rapid adoption in the first three weeks… and a gradual decrease of users is observed post-HW3.
However, a sustained user base in both courses indicates a core group of students who have
successfully integrated the tool into their regular workflow."*
→ [engagement decay](../concepts/engagement-decay.md)

**2. Usage is pulsatile and deadline-driven.** *"Usage spiked sharply in the days leading up to
homework deadlines and dropped to near zero immediately after."*

**That is the adversarial concurrency profile [the ODU latency study](../practice/cost-economics.md)
warns about**, now confirmed in a real engineering deployment. Everyone arrives at once, the night
before. Load-test at the peak, not the mean, and pick the throughput tier accordingly.

## The quality audit — and where it fails is where we'd expect

They hand-reviewed **260 sampled interactions** (<1% of the corpus, limited by evaluator time)
across six metrics:

| Metric | Result |
|---|---|
| Self-awareness | **98.46%** pass |
| Relevance | **98.08%** |
| Coherence | **97.69%** |
| ⚠ **Guidance targeting** | **7.31% failure** — the largest |
| ⚠ Factual accuracy | 5.77% failure |
| ⚠ Judgmental accuracy | 5.38% failure |

**Guidance targeting is the top failure**, meaning the tutor *"occasionally struggles to adapt to
the student's dynamic level of understanding, leading to either repetitive questioning or overly
complex explanations."* That is precisely
[MathTutorBench's long-dialogue degradation](../evaluation/mathtutorbench.md) and
[LearnLM being rated "patronizing"](learnlm.md), observed a third time in a live deployment.
**Adapting the register to the student is the unsolved problem, not generating good explanations.**

And their diagnosis of the other two failures is the thesis of our architecture, stated by
someone else: the causes *"stem from the inherent limitations of LLMs in performing numerical
verification and domain-specific fact-checking **without the support of external tools**."*
**RAG grounding alone did not fix numerical accuracy.** → [GPThermo](gpthermo-wpi.md),
[grounding and verification](../concepts/grounding-and-verification.md)

## ⚠ The outcome analysis — read the caveat, which they wrote themselves

Clean **dose-response** across usage tiers, in Glass's Δ (used rather than Cohen's d because
*"the score variances between AI tutor users and non-users differ"*):

| Usage tier | Glass's Δ vs non-users |
|---|---|
| Occasional | **0.09** |
| Moderate | 0.18 – 0.24 |
| Frequent | **0.33** |
| Top 10 users | **0.43** (Circuit Analysis) · **0.60** (Signal Processing) |

They also report **variance compression**: heavy users show *"tightly clustered distributions,
effectively eliminating the lower performance tail,"* where non-users show scores down to 20% and
grades of 0.0.

⚠⚠ **But usage was voluntary, and the authors say plainly what that means:**

> *"Glass's Δ is reported here solely to characterize between-group differences and **carries no
> causal interpretation.** Establishing whether AI tutor usage causally affects academic
> performance would require experimental or quasi-experimental designs in future work."*

**This is a textbook self-selection pattern**: students who voluntarily work 59+ problems with a
tutor are the conscientious ones, and conscientiousness produces both the usage and the grade. The
dose-response gradient and the vanishing low tail are exactly what selection looks like.
→ [correlational vs causal](../PAPER.md)

**Credit where due — they flagged it themselves, in the paper, unprompted.** Most deployment
papers do not. But the number that will get quoted from this paper is 0.60, and it should not be.

## What we should take

1. **Ship distinct modes, not one chat box.** Solution feedback / guided support / open Q&A was
   the most-used design decision here, and guided support won.
2. **RAG is not enough for numbers.** Their own failure analysis says so. The tool layer is
   separate and necessary. → [property data tools](../domain/property-data-tools.md)
3. **Expect the novelty curve, and measure the floor rather than the peak.** Adoption collapses
   after roughly the third assignment and then stabilises at a real core.
4. **Design for the deadline spike.** Near-zero usage between assignments, everyone at once before.
5. **We can beat this paper on exactly one axis: causal design.** They had 116 students, a
   deployed system, and had to disclaim causality. A crossover design at our scale
   ([Kestin's](../evidence/kestin-2025-rct.md)) would produce a claim they could not make.
   **That is a concrete, achievable way for a capstone to contribute something a well-resourced
   deployment did not.**

## Open questions

- [ ] Which institution? The paper says only "a large public research-intensive institution in the
      southeastern United States." Worth identifying — they are a year ahead of us.
- [ ] Do they publish the SRL prompt scaffolding? That is the reusable artefact.
- [ ] The quality audit covers <1% of interactions and is single-rater as far as stated. No
      inter-rater reliability is reported. Worth checking a follow-up.

## Connects to

- [GPThermo](gpthermo-wpi.md) — the tool layer this system is missing
- [PeteChat](petechat-purdue.md) — the other deployed engineering-course tutor; opposite result on hint uptake
- [Engagement decay](../concepts/engagement-decay.md) — the novelty curve, with a floor
- [Cost and latency](../practice/cost-economics.md) — pulsatile deadline-driven load, confirmed
- [MathTutorBench](../evaluation/mathtutorbench.md) — guidance targeting fails the same way here
- [Student AI perceptions](../evidence/student-ai-perceptions-2025.md)

## Sources

- ["Leveraging RAG-Enhanced LLMs for Engineering Education: Design and Evaluation," *ASEE 2026*](https://peer.asee.org/59993.pdf) `[read — full text, 26 pp., 2026-09-01]`
