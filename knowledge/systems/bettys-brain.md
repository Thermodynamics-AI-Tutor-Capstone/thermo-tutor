# Betty's Brain

**Type:** system
**One line:** A Vanderbilt "learning by teaching" environment where students teach a software
agent via causal concept maps, then watch it fail quizzes.
**Why we care:** We called this "the most under-exploited idea in the knowledge base." After
reading the primary literature: **the mechanism is beautifully specified and the evidence for
it is far weaker than we assumed.** It remains a defensible design bet. It is not an
evidence-backed claim.

> **Substantially corrected 2026-08-31.** This node previously implied a proven learning
> mechanism and asked "what are the effect sizes?" as an open question. The answer is that
> **they were largely never published**, and where a controlled comparison exists, learning by
> teaching **did not beat being tutored**. Corrections marked ⚠.

## How it actually works — now fully specified

Gautam Biswas, Krittaya Leelawong and colleagues, Vanderbilt.

**Betty's brain is a directed concept map with three link types:**

1. **Causal** — *"specifies an active relationship on how a change in the originating concept
   affects the destination concept,"* and the student **must explicitly mark each as increase
   (++) or decrease (−−)**
2. **Hierarchical** — class structure ("fish is a type of animal")
3. **Property** — annotations ("fish live by rocks")

**Betty does not machine-learn.** *"Betty does not use machine learning techniques to learn
from examples or by induction; **she knows and reasons with what she has been taught by the
student**."* And *"Betty never forgets what she is taught."*

**Inference is qualitative propagation** — a simplified implementation of Forbus's qualitative
process theory. Breadth-first forward propagation of an increase/decrease along outgoing causal
links, composed pairwise via a sign table; propagation **halts at any node with ≥2 incoming
links** until all are resolved, then a combination algebra resolves them. With ≥3 incoming
links, magnitudes bucket into six levels (−L, −, −S, +S, +, +L) and combine smallest-first.

Query template: *"If Concept A increases (decreases), what happens to Concept B?"*

**Explanations are back-traces, not forward traces** — a deliberate choice: *"Though Betty
reasons forward, she explains her answer using a back trace. We have found that students find
it easier to follow the reasoning process and the explanation, if it is chunked in this way."*

**Mr. Davis**, the mentor agent, holds the **complete expert concept map**, overlays the
student's map on it, and generates hints from the diff — originally in **three escalating
levels**: point at the relevant resource → name the missing concept or relation → say exactly
where to insert the link.

## ⚠ Correction 1: the evidence is much thinner than we claimed

**The 10-year retrospective (Biswas, Segedy & Bunchongchit, IJAIED 2016) reports no effect
sizes at all** — no Cohen's *d*, no sigma, no p-values, no pre/post means, no controlled
between-condition learning comparison. Its quantitative content is process analytics, not
outcomes. The strongest claims are *"led to better pre-post learning gains"* and *"demonstrated
more effective learning behaviors"*, both without numbers.

**The one controlled study we could read (Biswas et al. 2005, n = 45, three groups of 15,
fifth-graders, six 45-minute sessions) found the conditions equal on immediate learning:**

> *"students in all conditions showed improved performance from pre- to posttest… **However,
> there was no improvement in their understanding of ecosystem balance. There were few
> differences between the conditions** in terms of the quality of their final maps."*

The advantage appeared only **~7 weeks later**, on a *preparation-for-future-learning* transfer
task (build a map for a never-taught domain) — and it belonged to the **self-regulated-learning
group**, which beat *baseline learning-by-teaching* as well as the tutored condition:

> *"Students in all three groups demonstrated the same learning performance in traditional
> learning tasks, but the SRL group demonstrated better ability to learn new material without
> the scaffolds."*

**So the measured benefit came from the metacognitive scaffolding layer, not from the teaching
framing per se.** And the SRL group was *slowest* initially — roughly two of six sessions went
to learning the strategies before productivity rose.

*(The 2008 paper's abstract claims the two learning-by-teaching groups outperformed the tutored
group. That conflicts with the 2005 report of the same study family. We could not obtain the
2008 full text — every route was blocked. **Treat "learning by teaching beats being tutored" as
unconfirmed.**)*

## ⚠ Correction 2: it is K-12 only, and roughly half of students fail the task

Every Betty's Brain study is **grades 5–6 science** — river ecosystems, climate change, human
thermoregulation. **No university, no STEM problem-solving, no engineering, anywhere.** The
only generality claim in the retrospective is a citation to Roscoe & Chi (2007) on the tutor
learning effect, which we have not read.

And the task is hard for the intended population. From a 40-student classroom study: **18
students "made very little progress"** teaching Betty; 16 taught a correct or nearly correct
map; 6 made meaningful progress. **45% effectively failed.** Separately: *"**77% of the feedback
delivered by Betty and Mr. Davis were ignored by students**."* The retrospective admits the
performance dichotomy *"persisted even as we designed new feedback."*

## ⚠ Correction 3: the theory points *away* from our use case — or possibly straight at it

Both AutoTutor reviews independently place teachable agents at the **high-prior-knowledge end**
of their interaction-control continuum, on the reasoning that teaching requires the highest
learner contribution. Nye et al. are explicit that this is **untested**:

> *"it is not noted in the table because **conclusive evidence is not yet available**, it is
> hypothesized that **teachable agents will be most beneficial for high-knowledge learners**."*

**This cuts both ways for us.** Undergraduate engineering students are exactly the
high-prior-knowledge population the theory predicts should benefit most — **and the population
nobody has tested.** That is a genuine opening rather than a reason to stop. But it must be
stated as a bet, not as evidence.

## The 2025 replication attempt, and why it proves less than it appears

Liu et al., *Scientific Reports* 15:40971 — 533 middle-school students, 2,729 dialogue sessions
with a **GenAI-powered** teachable agent (not Betty's Brain) on the Math Nation platform.

Genuinely interesting descriptive findings:
- **The "declined" group did more and finished less**: 6.66 sessions vs 3.79, completion rate
  **0.35 vs 0.58**
- Interaction mode: declined students **36% passive**; improved students **62.8% constructive**
- **The improved group showed 9× more frustration/confusion** (14.81% vs 1.57%) — consistent
  with confusion being productive
- **Boredom made up 50.4% of the declined group's non-neutral emotions and rose as sessions
  progressed**
- Both groups showed *"minimal evidence of higher-order reasoning"*

**But three flags we are raising, not the authors:**
1. **Regression to the mean is uncontrolled and probably dominant.** Groups were *defined* by
   the sign of change on the *same 15-item test*. The declined group started **higher**
   (pre 0.48 → post 0.29); the improved group started lower (0.34 → 0.58). The word
   "regression" does not appear in the paper.
2. **There is no control group.** This paper contains **no evidence that teachable agents help
   or harm learning.** It is descriptive learning analytics on one cohort.
3. An internal inconsistency: Methods defines session length as a **count of responses**;
   Results reports *"a mean session duration of 52.84 min."* Those cannot both be true.

**Their design recommendations are usable regardless:** a co-set time box with visible
countdown, **real-time off-task detection via semantic similarity to the session goal**
(they suggest a 0.45 threshold), a **"curiosity list"** that banks off-topic questions for a
post-task window, and staged redirection ending in a 2-minute lock to task-relevant options.

## Where this leaves the idea for us

**Still worth prototyping, for reasons that survive the corrections:**

- The mechanism directly attacks our central failure mode. A student demanding "just give me
  the answer" is asking to receive; **there is no answer to receive when you are the teacher.**
  → [Bastani's crutch effect](../evidence/bastani-2025-harm.md)
- An LLM removes the original ceiling. Betty needed knowledge in a *formal* representation
  because that is all she could reason over; concept maps were a laborious interface. An LLM
  can adopt a stated — possibly wrong — model of thermodynamics and reason from it in natural
  language. And [TutorGym](../evaluation/tutorgym.md) shows LLMs produce *"remarkably
  human-like learning curves"* as simulated students, which is exactly the capability a
  teachable agent needs.
- The theory predicts it suits our population, and nobody has checked.

**But scope it honestly:** this is a **Phase 3 Wizard-of-Oz prototype answering a named
question**, not a proven mechanism to build the project on. And the hard engineering problem is
real — models are trained to be right, so making one faithfully hold and act on a student's
*wrong* model is the thing to test first.

## Open questions

- [ ] **Read Roscoe & Chi (2007)**, *Review of Educational Research* — the only cited basis for
      generality beyond K-12. Also Bargh & Schul (1980) and Benware & Deci (1984) on the
      prepare-to-teach effect.
- [ ] Obtain Leelawong & Biswas (2008) full text and resolve the conflict with the 2005 results.
- [ ] Can an LLM be made to hold a wrong model faithfully? **Testable in an afternoon.**
- [ ] Does the qualitative-propagation idea transfer? Thermodynamics has genuine signed causal
      structure (raise T at fixed V → raise P) — a Betty-style causal map may fit our domain
      *better* than it fits ecosystems.

## Connects to

- [productive failure](../concepts/productive-failure.md) — Betty failing is the point
- [Bastani 2025](../evidence/bastani-2025-harm.md) — the crutch effect this defeats structurally
- [TutorGym](../evaluation/tutorgym.md) — LLMs as credible simulated students
- [AutoTutor](autotutor.md) — same research tradition, opposite interaction-control end
- [our roadmap](../../admin/roadmap.md) — a Phase 3 prototype candidate

## Sources

- [Biswas, Leelawong, Schwartz & Vye, "Learning by Teaching: A New Agent Paradigm for Educational Software," *Applied AI* 19(3–4) 2005](https://www.tandfonline.com/doi/full/10.1080/08839510590910200) `[read]` — **the knowledge representation and the n=45 controlled study**
- [Biswas, Segedy & Bunchongchit, "From Design to Implementation to Practice a Learning by Teaching System: Betty's Brain," *IJAIED* 26(1) 2016](https://link.springer.com/article/10.1007/s40593-015-0057-9) `[read]` — the 10-year retrospective; **reports no effect sizes**
- Leelawong & Biswas, "Designing Learning by Teaching Agents," *IJAIED* 18(3) 2008 `[abstract only]` — full text unobtainable; its abstract conflicts with the 2005 results
- [Liu et al., "Engagement patterns of middle school students with AI teachable agents in mathematics learning," *Scientific Reports* 15:40971 (2025)](https://www.nature.com/articles/s41598-025-24841-8) `[read]` — descriptive only; no control group
- Roscoe & Chi (2007), *Review of Educational Research* `[found]` — **the generality claim rests here; read it**
