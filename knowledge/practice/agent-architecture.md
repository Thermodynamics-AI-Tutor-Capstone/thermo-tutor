# Agent architecture — the components, and the one law that constrains all of them

**Type:** practice
**One line:** Multi-step agent reliability decays **geometrically** in the number of steps, and
every frontier model tested falls *"from near-perfect success to near zero within sixteen steps"*
on a genuinely agentic task — which is roughly the length of a Rankine cycle analysis.
**Why we care:** Our architecture notes came almost entirely from education papers, which lag this
literature badly. This node is the engineering side, and it changes what we should build.

> ⚠ **Scope honesty.** This is a first pass over nine papers, seven of them 2026 preprints that
> have not been through peer review. It is a snapshot of a fast-moving literature, not a settled
> account, and it is written by someone who is not a practitioner in it.
> → [standing gaps](../../CLAUDE.md)

---

## The foundations, which predate all of the above

⚠ Everything else in this node is a 2026 preprint. These three are peer-reviewed, heavily
replicated, and the vocabulary the rest of the literature assumes. **Anchoring on them is a
deliberate correction** to a node that would otherwise rest entirely on unreviewed work.

**ReAct** (Yao et al., **ICLR 2023**) is the loop nearly every agent still runs. Its observation was
that *"reasoning (e.g. chain-of-thought prompting) and acting (e.g. action plan generation) have
primarily been studied as separate topics,"* and its contribution was to **interleave** them —
generate a reasoning trace, take an action, observe, repeat. When later papers say "the agent
loop," this is it.

**Reflexion** (Shinn et al., 2023) added learning without weight updates: agents *"verbally reflect
on task feedback signals, then maintain their own reflective text in an **episodic memory buffer**
to induce better decision-making in subsequent trials."* ⚠ Note the [Horizon Gap survey's
verdict on this line](agent-architecture.md) — *"intrinsic self-correction does not reliably improve reasoning
**without external grounding**."* **Reflection needs something true to reflect against**, which for
us is the [solver](../concepts/grounding-and-verification.md).

**Chain-of-thought** (Wei et al., 2022) is the substrate both build on.

**Why this matters for a tutor specifically:** ReAct's interleaved reason→act→observe loop is
structurally the same shape as the
[sub-question / verify / respond loop](../concepts/grounding-and-verification.md), with the
student's work as an additional observation channel. We are not inventing an architecture; we are
instantiating a well-worn one with a domain solver in the action slot and a student in the loop.

## ⭐⭐ The geometric law

*"How Fast Do Agents Rot? An Empirical Study of Long-Horizon Degradation in LLM Agents"*
(arXiv:2609.01660). Nine models — six open, 1.2B to 671B, plus three deployed proprietary systems
— four task families, five horizons, three context regimes, **10,664 analysed trajectories.**

> **"Task success follows a geometric law governed by a single per-step reliability parameter,
> which rises with model scale but saturates well below 1 even for the strongest models,
> guaranteeing eventual collapse at sufficiently long horizons."**

If per-step reliability is *p*, success over *n* dependent steps goes as *pⁿ*. **p = 0.95 gives
44% at sixteen steps. p = 0.98 gives 72%.** Scale raises *p*; it does not reach 1.

> **"The effect is sharpest on the agentic task, where every model tested, including widely
> deployed systems, falls from near-perfect success to near zero within sixteen steps."**

**A full cycle analysis — draw the cycle, fix each state, apply the balances, check the
assumptions, compute efficiency — is comfortably sixteen dependent steps.** We are squarely in the
collapse regime, not adjacent to it.

### ⚠ And the obvious mitigation is backwards

> **"Degradation is driven by step count rather than context length: bounding the context window
> *steepens* decay rather than easing it (logit slope −0.69 vs −0.44, p = 3×10⁻⁶), contradicting a
> lost-in-the-middle explanation and warning against a common production shortcut."**

Trimming context to keep the agent focused **makes it worse**. The problem is the number of
dependent decisions, not how much text is in the window.

Their projection of measured reliability onto real horizons: **0.42 at GAIA-length horizons,
0.24 at hundred-step production horizons.** Their recommendation is
*"horizon-aware evaluation and reliability budgeting in place of aggregate pass-rate metrics."*

### ⭐ Why this is an argument *for* the verifier loop

**A deterministic check after every step breaks the exponent.** If each sub-answer is validated
against a solver before the next begins, an error is caught and corrected at step *k* rather than
propagating into steps *k+1…n*. The chain stops being *pⁿ* and becomes closer to *n* independent
draws with correction.

That is exactly
[the sub-question / sandbox / Answer-Verifier loop](../concepts/grounding-and-verification.md)
the ASEE petroleum tutor published and never tested — and this literature supplies the reason it
should work that has nothing to do with pedagogy. **Two independent motivations for the same
architecture is the strongest signal we have.**

---

## Three axes the field conflates

From *"The Horizon Gap"* (arXiv:2608.06663), a survey of **1,547 arXiv papers, 2024–2026**, with a
disclosed two-stage filter (26.8% of raw hits excluded as off-topic):

| Term | What it is a property of |
|---|---|
| **Long-horizon** | the **task** — how many steps it requires |
| **Long-context** | the **model** — how many tokens it can attend to at once |
| **Long-term memory** | the **system** — whether information persists across steps or sessions |

> *"Logically independent axes that a single 'long-horizon' label obscures."*

**Our problem is long-horizon, mildly long-context, and — for a tutor that tracks a student across
a semester — genuinely long-term-memory.** Those need three different solutions and we should stop
saying "context" when we mean any of them.

## The component decomposition

The survey organises its corpus into six categories tracking a long-horizon task's lifecycle:

1. **Planning and decomposition**
2. **Memory and context management**
3. **Execution control and recovery**
4. **Training for long horizons**
5. **Evaluation and measurement**
6. **Foundations, limits, and safety** of running agents unattended

Crossed with a second axis — **where the horizon is carried**: within one context, within one task
via a harness that exceeds the context window, or persistently across tasks and sessions.

Named failure modes: *"losing track of an earlier decision, declaring a half-finished job done, or
quietly drifting from the goal they were given."* The middle one should worry us most — **a tutor
that declares a half-finished derivation correct is worse than one that fails visibly.**

**On context management**, the survey's summary is blunt:

> *"Context management is **load-bearing** for whether an LLM agent's plan survives contact with a
> long trajectory, **not an implementation detail behind it**."*

The failure mode has a name — **"context rot"** — and **external memory is *"by far the largest
subcategory in the corpus."***

## ⭐ The harness matters as much as the model

*"Same Model, Different Harness: Different Coding-Agent Results"* (arXiv:2608.26218). A harness
*"decides what the model sees, which tools it can use, and how the work continues."* They held
model and task fixed and changed only the harness — mechanically shortening older tool results as
context fills, and responding to repeated or stalled work.

On SWE-bench Verified under a tight 20,480-token window, 169 tasks, fixed 480-second budget:

| | Control | Treatment |
|---|---|---|
| Mean per-task fail-to-pass fraction | **28%** | **49%** |
| Complete solutions | **43** | **72** |

And *"without model-specific retuning, the same frozen treatment also raises both endpoints… for
three additional models with different designs."*

**Nearly doubling task completion by changing context handling alone.** This is the engineering
twin of [the arena result where ChatGPT-4o placed 2nd and GPT-4o 5th](../systems/learnlm.md) — same
model, different wrapper, different outcome. **What we build around the model is not overhead; it
is most of the system.**

## ⭐ Tool-calling failures decompose, and the decomposition fits a tutor exactly

*"Calibration is the Bottleneck: An Action-Class Diagnostic of Multi-Turn Tool-Calling"*
(arXiv:2609.00949). Their complaint about aggregate metrics is the same one this repository makes
about pass rates:

> *"This metric **averages over many different multi-turn situations and obscures whether progress
> is balanced across them**."*

They decompose multi-turn failures into **two orthogonal modes** over a **four-class action
space**:

| Action class | Failure mode |
|---|---|
| **TOOL_CALL** / **ASK** / **REFUSE** / **CONFIRM** | **Action-class miscalibration** — picking the wrong *kind* of move |
| | **Action-execution failure** — right kind of move, executed wrong |

They separate the two with a self-revealing bound, **Acc ≤ GAR** (Gold Action Recall): a violation
(Acc > GAR) exposes *"state-grader masking of miscalibration"*, while large slack (GAR ≫ Acc)
localises execution failure inside TOOL_CALL.

**Their headline finding is that the first mode is invisible to standard grading** — *"the
diagnostic reveals action-class miscalibration as a substantial failure mode the state grader
cannot see,"* and this *"**inflates standing for heavily tool-trained families**."*

### ⭐⭐ That four-class space is a tutoring taxonomy

The mapping is almost too neat:

| Their class | Our tutor |
|---|---|
| **TOOL_CALL** | Look up a property, run the verifier on the student's step |
| **ASK** | Put a Socratic question back to the student |
| **REFUSE** | [Withhold the answer](../concepts/guardrails.md) |
| **CONFIRM** | Check understanding before moving on |

**"Action-class miscalibration" in a tutor is: answering when it should have asked, asking when it
should have verified, or refusing when the student genuinely needed telling.** That is a precise,
measurable frame for tutoring failure — and **nobody in the education literature has it.** Our
[behavioural evaluation](../evaluation/behavioral-evaluation.md) measures whether the student acted
on feedback; this would measure whether the tutor picked the right *kind* of move in the first
place. **The two compose, and building this taxonomy for thermodynamics tutoring is a genuinely
novel and cheap contribution.**

### ⚠ And it complicates the harness finding above

> *"Calibration is **reshapable through context-only perturbations**, but the reshape is
> **heterogeneous**: a single perturbation moves accuracy in **opposite directions across
> families (up to +11.5 vs −21.0 pp** on the same [perturbation])."*

**The same context change helped one model family by 11.5 points and hurt another by 21.**

Set that beside the harness paper's claim that *"without model-specific retuning, the same frozen
treatment also raises both endpoints… for three additional models with different designs."* **Both
are measured; they are not obviously compatible.** Different perturbations and different tasks
could explain it, but the honest reading is:

> **Harness engineering can be worth ~20 points in either direction, and whether a given change
> transfers across model families is not settled.** Do not assume our harness improvements
> generalise — measure them per model, and re-measure on every model change.

That reinforces the regression-testing point in
[observability](agent-observability.md), and it is a second reason —
beyond [CS50's instruction dilution](../systems/cs50-duck.md) — that a model upgrade is a
re-evaluation event, not a version bump.

## ⚠ Premature commitment — a failure mode a tutor would inherit

*"When Agents Commit Too Soon"* (arXiv:2606.22936):

> *"Long-horizon LLM agents can fail quietly: they **settle on one reading of the evidence early,
> then spend the rest of the run defending it**… Final-answer scoring misses the failure mode
> because it sees only the answer, not whether the process has already collapsed to a stable
> path."*

Detectable from hidden-state convergence at a fixed reasoning step, with a runtime monitor
reaching **AUROC up to 0.97** (0.85–0.88 under a stricter split).

⚠ **But read their boundary, which they call central to the claim:**

> *"It does not track correctness: committed-wrong and committed-correct questions are not
> separable in activation similarity… **Commitment tells us whether an agent has settled, not
> whether it is right**."*

**A tutor that commits early to a misreading of a student's work and then defends it is a specific,
nameable harm** — it is how a tutor talks a student out of a correct answer. Worth watching for,
though note the monitor needs hidden states, which rules it out for API-only models.

## What follows for us

1. **Decompose and verify every step.** Not for pedagogy — for the exponent.
2. **Do not trim context to "keep it focused."** Measured to make things worse.
3. **Budget reliability by horizon**, not by aggregate pass rate. Ask "how many dependent steps
   does a Rankine problem take, and what per-step reliability do we need?" before asking which
   model.
4. **Treat the harness as the product.** Half our engineering effort belongs there, not in prompts.
5. **Separate the three axes** in our own design docs — task horizon, model context, and the
   student model that persists across a semester are three different problems.

## Open questions

- [ ] Does the verifier loop actually break the geometric law, or merely soften it? **This is
      directly measurable and nobody in the education literature has measured it.** A strong
      capstone experiment.
- [ ] What *is* the step count of a typical ME 300 problem? We cannot even ask the reliability
      question until we have real problems. → [paper access and ME 300](../../admin/paper-access.md)
- [ ] Almost all of this literature evaluates coding and web agents. **How much transfers to a
      tutoring loop, where the agent's "task" is partly the student's?** Unknown, and we should not
      assume.

## Connects to

- [Grounding and verification](../concepts/grounding-and-verification.md) — the verifier loop the geometric law argues for
- [Agent observability](agent-observability.md) — the companion node
- [Cost and latency](cost-economics.md) — the ODU multi-agent latency measurements
- [LearnLM](../systems/learnlm.md) — same model, different wrapper, different result
- [Guardrails](../concepts/guardrails.md)

## Sources

**Foundations:**

- [Yao, Zhao, Yu, Du, Shafran, Narasimhan & Cao, "ReAct: Synergizing Reasoning and Acting in Language Models," ICLR 2023, arXiv:2210.03629](https://arxiv.org/pdf/2210.03629) `[read]`
- [Shinn, Cassano, Berman, Gopinath, Narasimhan & Yao, "Reflexion: Language Agents with Verbal Reinforcement Learning," arXiv:2303.11366](https://arxiv.org/pdf/2303.11366) `[read]`
- [Wei et al., "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models," arXiv:2201.11903](https://arxiv.org/pdf/2201.11903) `[read]`


- ["Calibration is the Bottleneck: An Action-Class Diagnostic of Multi-Turn Tool-Calling," arXiv:2609.00949](https://arxiv.org/pdf/2609.00949) `[read]` — the TOOL_CALL/ASK/REFUSE/CONFIRM decomposition and the heterogeneous-transfer warning

All held in `course-materials/papers/`.

- ["How Fast Do Agents Rot? An Empirical Study of Long-Horizon Degradation in LLM Agents," arXiv:2609.01660](https://arxiv.org/pdf/2609.01660) `[read]` — the geometric law; 10,664 trajectories
- ["The Horizon Gap: Planning, Memory, Execution, Training, and Evaluation for Long-Horizon LLM Agents," arXiv:2608.06663](https://arxiv.org/pdf/2608.06663) `[read]` — survey of 1,547 papers
- ["Same Model, Different Harness: Different Coding-Agent Results," arXiv:2608.26218](https://arxiv.org/pdf/2608.26218) `[read]`
- ["When Agents Commit Too Soon: Diagnosing Premature Commitment in LLM Agents," arXiv:2606.22936](https://arxiv.org/pdf/2606.22936) `[read]`
- ["Toward Safe LLM Agents: A Survey of Specification, Verification, and Enforcement," arXiv:2608.14590](https://arxiv.org/pdf/2608.14590) `[skimmed]` — source of the "verifier tax": intercepting 94% of individually unsafe actions still left safe-success below 5%
