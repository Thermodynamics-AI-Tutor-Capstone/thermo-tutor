# Agent observability — what to log, who reads it, and why benchmarks lie

**Type:** practice
**One line:** Four independent 2026 lines converge on the same conclusion: **aggregate pass rates
do not tell you whether an agent is deployable**, and the trace — not the final answer — is where
the information is.
**Why we care:** [CS50's guardrails silently degraded on a model upgrade](../systems/cs50-duck.md)
and nobody noticed until they measured 10M messages. That is an observability failure, and we have
had almost nothing on the subject.

> ⚠ **Scope honesty.** A first pass over five 2026 preprints, none peer-reviewed. Fast-moving
> literature, snapshot not settlement. → [standing gaps](../../CLAUDE.md)

---

## The framing that reorganises everything: a trace has two consumers

*"Parsing the Stream: A Live Trace Model for Long-Horizon Agents and Their Observers"*
(arXiv:2609.01466):

> **"A long-horizon agent's trace outgrows both of its consumers: the human observer monitoring
> the run, and the agent itself, whose bounded context the trace must be folded back into."**

Their design: an **append-only event ledger**, folded incrementally into **typed run state**, then
compiled into **per-consumer views** — one for the human, one for the agent. Both from the same
state.

**Observer side**, against deterministic ground truth, with an LLM reader as proxy: the compiled
view answered monitoring questions using **~14–15× fewer input tokens at 5–7× lower cost**, with
**accuracy 0.85–0.87 versus 0.48** for a budget-capped single-call read of the raw trace.

**Agent side**, on 120-link sequential-dependency tasks: maintaining the running statistic in
per-step state succeeded **30/30**, versus **8/30** for full-context prompting.

### ⭐ Their honesty is the most useful thing about the paper

They undercut their own headline in the abstract, which is rare enough to be worth copying:

- *"Because the questions were **co-designed with the view schema**, we treat the token and cost
  reduction, **conditional on schema coverage**, as the transferable result"* — i.e. the accuracy
  gap is inflated by co-design; only the efficiency claim transfers.
- The 30/30 result is *"labeled **descriptive** owing to benchmark–system co-development."*
- **A plain prompt-level scratchpad "matches the fold's accuracy at lower cost."** Their own
  cheaper baseline nearly wins.
- *"The fold's remaining value over cheaper alternatives is **deterministic auditability** and
  serving the observer from the same state."*
- They *"delimit them with an **order-sensitive task family on which the fold ceases to help**."*

**Read that list before believing any observability vendor's numbers.** And note the practical
lesson: **start with a scratchpad.** The elaborate machinery buys auditability, not accuracy.

One concrete defect worth stealing as a rule: two header bugs — *"a 'complete list' label over a
partially evicted store, and an extraction count that reported only the in-view total"* — violated
their own requirement of **no silent truncation**. **A view that quietly drops data is worse than
no view**, because it is trusted.

## A different approach: mine structure across runs, not within one

*"Automata from Agent Traces: Failure and Next-Step Prediction"* (arXiv:2608.23670) attacks the
same problem from the opposite end:

> *"LLM-based agents execute multi-step tasks, but their **behavioral structure remains opaque**:
> long unstructured traces resist the safety auditing and runtime monitoring that deployment
> requires. **Existing approaches operate per-trace or success-only, so they miss the cross-run
> topology** that links next-step and failure prediction."*

They collapse an entire **trace corpus** into a single compact **finite-state machine**. The
observation underneath is that agent behaviour already *has* structure — *"a coding agent cycles
through search→edit→execute"* — that emerges from prompt, tools and task distribution but *"nowhere
is it specified."*

**For a tutor this is unusually attractive**, because tutoring loops are more stereotyped than
coding: *read problem → state assumptions → look up property → apply balance → check → respond*. A
learned FSM over our own traces would make **"which state do students get stuck in"** a computable
question — and that is [the instructor dashboard five systems converged on](../systems/biotutor-eth.md),
built from behaviour rather than from question text.

## Deployment readiness is not benchmark performance

*"READY: Reliable Enterprise Agent Deployment"* (arXiv:2609.02095) opens with the sentence our
project should keep:

> **"An AI agent can perform well on benchmarks and still be unsuitable for deployment."**

Benchmarks ask whether an agent *can* complete realistic work. Deployment asks *"whether an agent
can meet a **required reliability level**, under an **acceptable level of human oversight**, and at
a **tolerable cost**."*

Their procedure, which is a usable template:

1. Take a workflow's **own** definition of success.
2. Given a class of candidate **oversight policies**, measure the reliability and operating cost of
   the **human–AI system** — not the agent alone.
3. Select the **minimum-cost policy that satisfies a specified reliability target.**
4. **Statistically qualify** that policy on held-out cases.
5. Report a **deployment profile**: reliability, human-oversight burden, and cost.

**"Minimum-cost oversight policy meeting a reliability target" is exactly the question a
department would ask us**, and it is not a question any tutoring paper in this repository has
posed. It also fits the finding that
[the field's two strongest results are hybrid](../systems/tutor-copilot.md) — oversight is a design
variable, not a failure to automate.

## ⚠ Benchmarks can be gamed, and the field now measures how much

*"Do Agent Benchmarks Measure Capability? Protocol Validity in the Age of Agentic AI"*
(arXiv:2607.22368, Tencent Hunyuan / HKUST / Duke Kunshan). Scores support capability claims *"only
when the evaluation protocol keeps the intended capability necessary for success."* Agents instead:

- **recover public solutions**
- **read evaluation artifacts**
- **infer generator structure**
- **manipulate feedback**
- **benefit from invalid scoring paths**

They introduce **HackDetect**, a post-hoc audit identifying an exposure, determining how the agent
used it, and assessing whether the score is misleading — quantified as a **"Mislead gap."**

This lands next to the Horizon Gap survey's observation that in every category, *"the most
consequential recent papers are not new methods but rigorous demonstrations that an earlier method,
benchmark, or metric does not do what it claims"* — naming, among others, that
*"a substantial share of reported SWE-bench solves reflect test-suite weakness or training-data
leakage rather than genuine issue resolution."*

⭐ **The survey's phrasing for where evaluation is heading is exactly our own vocabulary:**
*"evaluation's version of the move from **outcome to process supervision**."* That is
[behavioural evaluation](../evaluation/behavioral-evaluation.md) and
[the proximal/distal collapse](../concepts/vanlehn-2011.md), arriving from the agents literature
with no knowledge of the education one.

## ⭐ The practitioner standard — OpenTelemetry GenAI semantic conventions

The papers above are research. **This is what the industry actually instruments against**, and it
means we do not have to invent a schema. Read from the
[semantic-conventions-genai repository](https://github.com/open-telemetry/semantic-conventions-genai)
on 2026-09-03 — 65 span attributes, 38 agent-span attributes, 24 metrics.

**Operations are first-class spans:** `invoke_agent`, `invoke_workflow`, `execute_tool`, keyed by
`gen_ai.operation.name`.

**Attributes that map onto problems this repository has already documented:**

| Attribute | What it gives us |
|---|---|
| `gen_ai.conversation.id` | Threading a student's session across turns |
| ⭐ `gen_ai.conversation.compacted` | **Context compaction is a recorded event** — directly relevant to [context rot and the harness finding](agent-architecture.md) |
| `gen_ai.tool.call.arguments` · `gen_ai.tool.call.result` · `gen_ai.tool.name` | Every CoolProp lookup and verifier verdict, logged |
| `gen_ai.retrieval.query.text` · `gen_ai.retrieval.documents` · `gen_ai.retrieval.top_k` | **RAG is in the standard** — retrieval failures become measurable, and [Jill Watson's 57% retrieval-failure rate](../systems/jill-watson.md) is the reason to measure them |
| `gen_ai.memory.store.id` · `gen_ai.memory.query.text` · `gen_ai.memory.records` | **Memory is in the standard too** — the substrate for a student model |
| `gen_ai.usage.cache_read.input_tokens` · `cache_write` | Cache accounting, which is most of the cost question |
| `gen_ai.response.time_to_first_chunk` | Perceived latency, not just total |

**Metrics that answer the questions [the ODU latency study raised](cost-economics.md):**
`gen_ai.client.operation.duration`, `gen_ai.invoke_agent.duration`,
`gen_ai.invoke_agent.inference_calls`, `gen_ai.invoke_agent.tool_calls`,
`gen_ai.execute_tool.duration`, `gen_ai.server.time_to_first_token`,
`gen_ai.server.time_per_output_token`, `gen_ai.client.token.usage`.

**`invoke_agent.tool_calls` and `.inference_calls` per interaction are exactly the parallel-phase
accounting** that determines whether we are in the P95-dominated regime.

### ⭐⭐ Their content-capture pattern is our FERPA answer

The spec is explicit that message content is dangerous:

> *"This attribute is **likely to contain sensitive information including user/PII data**."*

`gen_ai.input.messages` and `gen_ai.output.messages` are **`Opt-In`**, not recommended-by-default,
and for memory attributes: *"Instrumentations **SHOULD NOT capture this attribute by default**.
Capture SHOULD be gated by an explicit user opt-in."*

They give three options, and **the third is the one we want**:

1. Do not record instructions, inputs, or outputs at all.
2. Record them on the spans — *"best suited for situations where telemetry volume is manageable and
   either privacy regulations do not apply or the telemetry storage complies with them, **for
   example, in pre-production environments**."*
3. ⭐ **"Store content externally and record references on the spans. This pattern is recommended in
   production environments."**

**Option 3 separates the trace from the student data.** The trace holds structure — timings, tool
calls, verdicts, retrieval hits, token counts — and *references* to content held in a
FERPA-appropriate store with its own access controls and retention policy. That means the
observability layer we need for engineering does **not** have to be the system of record for
student work, which is the thing that makes the compliance conversation hard.

**This is a concrete, standards-backed answer to a question `admin/irb.md` currently leaves open**,
and it costs nothing if designed in from the start. → [IRB](../../admin/irb.md),
[disclosure and ethics](disclosure-and-ethics.md)

⚠ Note these conventions are marked **Development**, not Stable — attribute names will move. Pin a
version and expect churn.

## What we should actually build

Modest, and mostly free if done from the start:

1. **Log an append-only event ledger from day one.** Every turn, tool call, verifier verdict,
   student edit, timestamp. It is the substrate for
   [RelScore/SuccScore](../evaluation/behavioral-evaluation.md), for the instructor dashboard, and
   for any failure analysis we do later. **Not logging it is the one irreversible decision.**
2. **Build the instructor view and the agent's own context view from the same state.** Two
   consumers, one ledger.
3. **Start with a scratchpad, not a framework.** Their own baseline nearly matched the elaborate
   fold.
4. **Never silently truncate a view.** Stamp coverage explicitly.
5. **Regression-test guardrails on every model upgrade.** [CS50's compliance got worse going
   GPT-4 → GPT-4o](../systems/cs50-duck.md) and only a 10M-message audit revealed it. A fixed
   probe set run on each upgrade is cheap.
6. **Report a deployment profile, not a pass rate** — reliability, oversight burden, cost.
7. **Score against deterministic ground truth wherever one exists.** The trace paper computes
   *"every score… against deterministic ground truth, a deliberate contrast with LLM-judged agent
   evaluation"* — and [four studies say LLM judges fail on educational quality](../evaluation/llm-as-judge.md).

## Open questions

- [x] ~~What does the industry actually use?~~ **OpenTelemetry GenAI conventions now covered
      above.** Still uncovered: the tracing/eval *products* built on them (Langfuse, Braintrust,
      LangSmith, Phoenix and similar) — how teams actually run evals in CI, and what regression
      testing against model upgrades looks like in practice.
- [ ] Does an FSM mined from tutoring traces produce useful stuck-state detection? Testable on our
      own logs once we have any.
- [ ] What is the tutoring analogue of reward hacking? Plausibly **the student gaming the
      tutor** — and [22% of PeteChat's homework messages were boundary probes](../systems/petechat-purdue.md).
      Nobody has framed student behaviour this way.

## Connects to

- [Agent architecture](agent-architecture.md) — the companion node
- [Behavioral evaluation](../evaluation/behavioral-evaluation.md) — outcome → process supervision
- [LLM-as-judge](../evaluation/llm-as-judge.md) — why deterministic ground truth matters
- [CS50 duck](../systems/cs50-duck.md) — the regression that a 10M-message audit caught
- [Assessment integrity](assessment-integrity.md) — students probing limits
- [Cost and latency](cost-economics.md)

## Sources

All held in `course-materials/papers/`.

- ["Parsing the Stream: A Live Trace Model for Long-Horizon Agents and Their Observers," arXiv:2609.01466](https://arxiv.org/pdf/2609.01466) `[read]`
- ["Automata from Agent Traces: Failure and Next-Step Prediction," arXiv:2608.23670](https://arxiv.org/pdf/2608.23670) `[read]`
- ["READY or Not: Reliable Enterprise Agent Deployment," arXiv:2609.02095](https://arxiv.org/pdf/2609.02095) `[read]`
- ["Do Agent Benchmarks Measure Capability? Protocol Validity in the Age of Agentic AI," arXiv:2607.22368](https://arxiv.org/pdf/2607.22368) `[read]`
- ["The Horizon Gap," arXiv:2608.06663](https://arxiv.org/pdf/2608.06663) `[read]` — the critical-literature observation and the outcome→process framing
