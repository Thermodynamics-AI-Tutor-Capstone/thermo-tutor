# Cost Economics

**Type:** practice
**One line:** A full semester of realistic tutor usage costs roughly **$2.63–$4.79 per
student** in API spend.
**Why we care:** It closes an open question in our plan and removes cost as a design
constraint. Stop optimizing for it.

## The measured number

**The best figure is not an estimate — it's from a real deployment.**

[KAIST](../evidence/kaist-vta-2025.md) ran an LLM teaching assistant for **477 students over
14 weeks** at a total operational cost of **$180**, covering API usage *and* conversation-log
storage.

| Basis | Cost |
|---|---|
| Per enrolled student | **$0.38** |
| Per student who actually used it (235 of 472) | **$0.76** |
| Total, full course, full semester | **$180** |

For comparison, the modelled estimates from vendor analysis — ~2.5 cents per turn on
frontier pricing, ~$2.63–4.79 per student per semester at ~675 questions — are **roughly an
order of magnitude higher** than what KAIST actually spent. The gap is mostly the
[engagement reality](../concepts/engagement-decay.md): half the class never used it, so
half the modelled cost never materialized.

Even the pessimistic modelled figure stays far below a STEM textbook ($100–200).

## Why the structure matters more than the number

**Pay-per-token scales with actual usage.** Classical ITS infrastructure scales with *peak
capacity* regardless of demand. Commercial vendors (Khanmigo, MagicSchool, Curipod) price
per-student or per-teacher, scaling with **enrollment** rather than with tutoring actually
delivered.

Given [17% session engagement](../evidence/khanmigo-engagement-2026.md), per-seat pricing
means paying for a great many students who never open the thing. **Token pricing means the
engagement problem is not also a cost problem** — which is a genuine and underappreciated
advantage of building rather than buying.

## ⚠ Latency is the real operational constraint, not cost

Cost is settled. **Latency under classroom-scale concurrency is not**, and it is the thing
that will actually break a deployment.

*Latency and Cost of Multi-Agent Intelligent Tutoring at Scale* (Elhaimeur & Chrisochoides,
**Old Dominion University**, arXiv:2604.24110) instrumented **ITAS**, a four-agent tutoring
system on **Gemini 2.5 Flash / Google Vertex AI**, across three throughput tiers and eleven
concurrency levels up to 50 simultaneous users — **3,000+ requests from a live graduate STEM
deployment**.

Architecture: three parallel specialist agents (video context, content, guidance) feeding a
sequential synthesizer — **four API calls per student interaction**, all of which must
complete before the student sees anything.

| Tier | Behaviour |
|---|---|
| **Priority PayGo** | **Flat sub-4-second responses across the full load range** |
| Standard PayGo | **Degrades substantially under classroom-scale concurrency** |
| Provisioned Throughput | Lowest latency at low concurrency; **saturates above ~20 concurrent users** |

Both pay-per-token tiers came in well below the alternatives on cost.

**Why this matters to our architecture specifically.** Their named mechanism is the
**"parallel-phase maximum effect"**: in a multi-agent system, latency is the *maximum* of the
parallel calls, not the average — so the slowest agent sets the response time, and adding
specialists makes the tail worse. Our
[seven-layer design](../PAPER.md) is exactly this shape: retrieval, property tool calls,
verification, and policy all sit between the student's question and the answer.

And the concurrency profile of a course is adversarial: **everyone works the night before the
problem set is due.** A tutor that is fast in testing and slow at 11pm on Wednesday is a tutor
students abandon. → [engagement decay](../concepts/engagement-decay.md)

**Action:** budget a latency envelope early, measure it under simulated concurrency, and
treat the priority pricing tier as a requirement rather than an upgrade. The cost difference
is trivial at our scale; the latency difference is not.

### The measured numbers (full read, 2026-08-31)

**Costs, per student per semester.** Their headline table uses a deliberately absurd ceiling of
10,000 questions (100/day, every day) — **Standard $39.26, Priority $70.67**, both under a STEM
textbook ($100–200). Their own plausible scenario is **675 questions** (15/day × 45 class days):

| Tier | Realistic (675 q) | Worst case (10,000 q) |
|---|---|---|
| Standard PayGo | **$2.63** | $39.26 |
| Priority PayGo | **$4.79** | $70.67 |
| Provisioned Throughput | — | **>$225 at any scale** unless utilisation is kept high |

**Cost is not a design constraint for us. Stop treating it as one.**
Priority costs a **1.8× per-token premium** over Standard, which at realistic volume is
**about two dollars per student per semester.**

**Latency, by concurrency.** At **c = 20** — a 40-student class at peak — Priority holds a
**3.6 s median while Standard degrades to 7.8 s**, a 2.2× difference. Priority stays flat at
**3.5–4.0 s regardless of concurrency, with a zero failure rate.** Provisioned is fastest below
c = 20 and loses above it, as its fixed 7-GSU allocation begins queuing.

Their tier guidance, which we can adopt directly: **seminar (≤10 concurrent) Standard is fine;
classroom (40 students, peak ≈20) Priority; department and university scale Priority**, which
scales transparently with no capacity planning. *"The choice between them is ultimately a question
of traffic predictability, not scale."*

### ⭐ The two findings that should shape our architecture

**1. Optimise P95, not median — you pay the maximum of N draws.** The parallel phase accounts for
**65–70% of end-to-end latency** across all tiers, and because the system waits for the slowest of
three agents, its duration exceeds the median of any individual agent. How much it exceeds it
depends entirely on *variance*: *"a tier that stabilizes P95 stabilizes the maximum of three
parallel draws from that distribution."* Standard PayGo's **P95 hits 14.1 s at c = 40 — more than
double its own median.** Median latency is the wrong number to report or to tune.

**2. The bottleneck is set by input size, and it is stable.** The video agent — the one receiving
the lecture transcript — was the slowest of the three in **50–54% of requests**, versus 24–26% for
guidance and 21–24% for code, *"nearly identical across all three tiers and all concurrency
levels."* The agent with the biggest prompt is your latency, predictably.

**For a thermodynamics tutor this maps almost one-to-one.** Their video/code/guidance split
becomes something like property-and-solver, diagram-or-work-state, and Socratic guidance, feeding
a synthesizer. The lesson is that **whichever of ours carries the largest context — most likely
retrieved course material or a state table dump — will set the response time**, so that is the one
to trim, cache, or pre-compute. Trimming the others buys nothing.

Two implementation details worth copying: **structured JSON output schemas** to eliminate parsing
overhead, and **thinking disabled (`thinking_budget=0`)** on latency-critical agents.

⚠ **Scope limits.** Single provider (Vertex AI), single model (Gemini 2.5 Flash), c ≤ 50, and the
Provisioned crossover point is *"a property of our specific GSU allocation."* The authors note
OpenAI and Anthropic expose structurally identical tier models and argue the effect is a property
of queueing rather than of any provider — reasonable, but not tested here. They also did not
instrument the provider-side queue, so their explanation of the crossover is *"consistent with,
but not directly proven by"* their data — their words.

## What this means for us

**1. Cost is not a design constraint at our scale.** Anchoring on KAIST, a 100-student
semester pilot is **$40–80**; on the conservative modelled figure, $300–500. Either way it is
a departmental line item, not a funding application, and possibly a rounding error if
[PSU AI Studio](psu-ai-landscape.md) covers it.
[Open question D4](../../docs/03-open-questions.md) is answered.

**2. Don't compromise architecture to save tokens.** Verification passes, multi-step
reasoning, tool calls, a second model as judge — all cheap relative to the total, and all
worth far more than the savings.
→ [grounding and verification](../concepts/grounding-and-verification.md)

**3. Local models are a privacy choice, not an economic one.**
[Stan runs on Ollama locally](../systems/stan-udel.md), which is defensible for data
sovereignty. It is *not* justified by cost, and it comes at a real capability price given
[what frontier models already struggle with in thermodynamics](../domain/llm-thermodynamics-capability.md).
If [PSU AI Studio](psu-ai-landscape.md) provides a compliant channel to frontier models, the
privacy argument for local weakens considerably too.

**4. The real costs are elsewhere.** Domain authoring, IRB, integration, and — largest of
all — the [hand-crafted course-specific scaffolding](../evidence/kestin-2025-rct.md) that the
evidence says is where the learning effect actually lives. Those are measured in person-weeks,
and person-weeks are what a capstone team is short of.

## Open questions

- [ ] What does [AI Studio](psu-ai-landscape.md) cost us — is it free at point of use for a
      research pilot?
- [ ] Actual questions-per-student for a course tutor? Our estimate rests on a K-12-derived
      figure.
- [ ] Latency budget: how much does a verification pass and a tool call add per turn, and at
      what point does a student give up waiting?
- [ ] Does prompt caching materially change the numbers for long course-context prompts?
      (Likely yes — course context is highly cacheable across turns.)

## Connects to

- [PSU AI landscape](psu-ai-landscape.md) — possibly free and compliant
- [engagement decay](../concepts/engagement-decay.md) — why per-seat pricing is a trap
- [Stan](../systems/stan-udel.md) — local models as a privacy choice
- [open questions D4](../../docs/03-open-questions.md) — answered

## Sources

- [Kweon et al., KAIST VTA deployment, arXiv:2506.17363](https://arxiv.org/abs/2506.17363) `[read]` — **the $180 / 477 students figure. Use this one.**
- [ibl.ai, "What AI Tutoring Actually Costs in 2026"](https://ibl.ai/blog/what-ai-tutoring-actually-costs-2026) `[skimmed]` — the modelled per-student figures. Vendor blog; runs ~10× above measured reality.
- [Elhaimeur & Chrisochoides, "Latency and Cost of Multi-Agent Intelligent Tutoring at Scale," arXiv:2604.24110](https://arxiv.org/pdf/2604.24110) `[read — full text, 11 pp., 2026-08-31]` — Old Dominion University; 3,000+ requests from a live graduate STEM deployment
- [Xu, Q., "FairTutor: Equity-Aware Pedagogical LLM Routing for Budget-Constrained AI Tutoring," arXiv:2606.20713](https://arxiv.org/pdf/2606.20713) `[read — full text, 15 pp., 2026-09-01]` — read in full and written up in [equity](equity.md); this node's tag was stale
