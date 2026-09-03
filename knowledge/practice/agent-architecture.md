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

All held in `course-materials/papers/`.

- ["How Fast Do Agents Rot? An Empirical Study of Long-Horizon Degradation in LLM Agents," arXiv:2609.01660](https://arxiv.org/pdf/2609.01660) `[read]` — the geometric law; 10,664 trajectories
- ["The Horizon Gap: Planning, Memory, Execution, Training, and Evaluation for Long-Horizon LLM Agents," arXiv:2608.06663](https://arxiv.org/pdf/2608.06663) `[read]` — survey of 1,547 papers
- ["Same Model, Different Harness: Different Coding-Agent Results," arXiv:2608.26218](https://arxiv.org/pdf/2608.26218) `[read]`
- ["When Agents Commit Too Soon: Diagnosing Premature Commitment in LLM Agents," arXiv:2606.22936](https://arxiv.org/pdf/2606.22936) `[read]`
- ["Toward Safe LLM Agents: A Survey of Specification, Verification, and Enforcement," arXiv:2608.14590](https://arxiv.org/pdf/2608.14590) `[skimmed]` — source of the "verifier tax": intercepting 94% of individually unsafe actions still left safe-success below 5%
