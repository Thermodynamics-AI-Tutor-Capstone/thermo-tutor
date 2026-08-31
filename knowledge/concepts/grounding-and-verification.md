# Grounding and Verification

**Type:** concept
**One line:** Anchoring a tutor's outputs to authoritative sources, and checking them before
a student sees them — the technical layer that separates working systems from demos.
**Why we care:** It produced the largest measured improvement in this knowledge base, from
the same underlying model.

## The result that should settle the argument

[Jill Watson](../systems/jill-watson.md) restricts outputs to validated course material and
verifies each response using **textual entailment**. Against OpenAI's own Assistant on the
same courses:

| Metric | Jill Watson | OpenAI Assistant |
|---|---|---|
| Correct | **78.7%** | 30.7% |
| Harmful failures | **2.7%** | 14.4% |
| Confusing failures | 54.0% | 69.2% |
| Retrieval failures | 43.2% | 68.3% |

**Same underlying LLM. 2.5× accuracy, one-fifth the harmful errors.**

For comparison, [LearnLM's](../systems/learnlm.md) pedagogical fine-tuning bought +13% expert
preference over its own base model. **Architecture is a bigger lever than model choice or
model training, by a wide margin.**

## The three layers

### 1. Retrieval grounding
Restrict the model to validated course material. Everyone does this.
→ [RAG in education](rag-in-education.md)

Necessary, nowhere near sufficient: Jill Watson's *retrieval* failure rate is still 43.2%.
Grounding fails when the right passage isn't retrieved, and the model then answers from
weights anyway.

### 2. Tool calls for ground truth
Anything the model is unreliable at should not be done by the model.

[Khan Academy's](../systems/khanmigo.md) account: generative AI "generates a probable next
number rather than executing a correct calculation." Their fix was a **separate math agent**
verifying every calculation and expression in real time.

For thermodynamics this means property data from CoolProp/Cantera/IAPWS, symbolic
manipulation from a CAS, unit checking from a units library — never from weights. The
evidence for the necessity is unusually direct: [ThermoQA](../domain/thermoqa.md) shows
every frontier model scoring **44–63% on R-134a** property problems.
→ [property data tools](../domain/property-data-tools.md)

### 3. Output verification
Check the generated response before it reaches the student.

**Textual entailment / NLI** is the standard technique: a natural language inference model
checks whether the retrieved context *entails* the generated claim.

### ⭐ How to configure it — measured, and the defaults are wrong

From GASP (arXiv:2607.04223), span-level AUC on RAGTruth with a Qwen2.5-1.5B scorer. **This is
the most directly actionable table in the knowledge base:**

| Verifier configuration | Span AUC |
|---|---|
| Perplexity baseline | 0.565 |
| NLI `deberta-v3-**small**`, **whole context** | **0.532** — barely above chance |
| NLI `deberta-v3-**large**`, whole context | 0.605 |
| **NLI `deberta-v3-large`, max over K=5 chunks** | **0.677** ← best measured |
| SelfCheckGPT-NLI (N=4 regenerations) | **0.486** — *at chance*, at 4× the cost |

**Three findings to build on:**

1. **Never run NLI over the whole retrieved context.** Run it **per chunk and take the max**:
   +0.072 AUC, same model, zero extra research. The cause is mundane — a cross-encoder's
   **512-token limit truncates away the supporting evidence**.
2. **Model size is worth another +0.073.** `deberta-v3-small` over whole context scores 0.532,
   which means **a verification layer configured that way does essentially nothing** while
   appearing to work. This node previously recommended exactly that configuration; it was
   wrong.
3. **Do not build self-consistency checking.** SelfCheckGPT-style resampling is at chance in a
   grounded setting and costs N full regenerations.

Useful free signal: *"does any retrieved chunk entail this sentence at all"* separates grounded
from hallucinated spans at **0.56 vs 0.28** best-chunk entailment. And max-likelihood-drop
attribution agrees with the NLI-top-ranked chunk **69% of the time against a 20% chance rate** —
so the verifier gives you per-claim citations for free.

**Latency cost is unmeasured anywhere in this literature.** Every paper describes sentence-level
entailment as "costly" without a number. If we need a latency budget, **we have to measure it
ourselves** — and given that
[multi-agent latency compounds as the max of parallel calls](../practice/cost-economics.md),
we should.

### ⚠ What entailment verification cannot do

The grounding survey (KDD 2024) names three claim types where NLI models fail: **temporal
statements, negation, and quantifiers.** A numeric lookup out of a table is structurally the
first case — asking an NLI model whether a table entails *"h_f = 191.83 kJ/kg"* is asking it to
perform lookup and arithmetic.

**So an NLI layer will not catch a wrong steam-table value.** Property numbers need a
**deterministic value-checker** against structured data.
→ [property data tools](../domain/property-data-tools.md)

Also worth adopting: the survey's distinction between **grounding** (*"attribution to a
user-specific knowledge base"*) and **factuality** (*"attribution to commonly agreed world
knowledge"*). A claim can be perfectly true and still **ungrounded**. For us that is exactly
right — an answer using a *different textbook's sign convention for work* is correct in the
world and wrong in this course, and should be flagged.

Off-the-shelf production services worth benchmarking before building: **Google Vertex AI
"Check grounding"** and **Azure AI Content Safety "Groundedness detection."**

The architectural principle — worth stating plainly because it's easy to violate —
**separate the generating logic from the validating logic.** A model checking its own work
is not verification.

## The guardrail metric idea

Khan Academy tracks **math error rate** as a *guardrail metric*: a number that must not
degrade, monitored continuously in production, separate from any success metric.

We should define ours early. Candidates: property-value error rate, rate of unwarranted
assumptions (the [adiabatic trap](../domain/thermo-problem-benchmark.md)), rate of
unverified numbers reaching the student.

**A number that goes in a dashboard on day one and gets watched forever.** Cheap to build,
impossible to reconstruct later.

## Open questions

- [ ] What NLI model and threshold does Jill Watson use? Is it published?
- [ ] What does a 43.2% retrieval failure rate consist of? Chunking? Query formulation?
      Missing content?
- [ ] What's the latency cost of entailment checking on every turn?
- [ ] Can verification catch a *pedagogically* bad response, or only a factually wrong one?
      (Probably only factual — which means it doesn't help with
      [guardrails](guardrails.md) at all.)

## Connects to

- [Jill Watson](../systems/jill-watson.md) — the exemplar
- [RAG in education](rag-in-education.md) — the retrieval layer
- [property data tools](../domain/property-data-tools.md) — our domain's tool layer
- [Khanmigo](../systems/khanmigo.md) — the math agent and guardrail metric
- [LLM capability in thermodynamics](../domain/llm-thermodynamics-capability.md) — what needs
  verifying in our subject

## Sources

- [Georgia Tech, "Jill Watson Outperforms ChatGPT in Real Classrooms" (2025)](https://news.research.gatech.edu/2025/09/02/georgia-techs-jill-watson-outperforms-chatgpt-real-classrooms) `[skimmed]`
- [Khan Academy blog on building a better AI tutor](https://blog.khanacademy.org/how-khan-academy-is-building-a-better-ai-tutor-our-most-recent-learnings/) `[skimmed]`
- [Grounding and Evaluation for LLMs: Practical Challenges and Lessons Learned, arXiv:2407.12858](https://arxiv.org/pdf/2407.12858) `[found]`
- [Detecting Hallucinations in RAG through Grounding-Aware Sensitivity by Perturbation (GASP), arXiv:2607.04223](https://arxiv.org/pdf/2607.04223) `[found]`
