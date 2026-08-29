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
checks whether the retrieved context *entails* the generated claim. Long responses get split
into sentences, each checked separately. Lightweight models (fine-tuned DeBERTa-v3-base)
are adequate and cheap.

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
