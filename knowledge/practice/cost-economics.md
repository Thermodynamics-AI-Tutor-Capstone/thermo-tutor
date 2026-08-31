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
- [Latency and Cost of Multi-Agent Intelligent Tutoring at Scale, arXiv:2604.24110](https://arxiv.org/html/2604.24110v1) `[found]`
- [FairTutor: Equity-Aware Pedagogical LLM Routing for Budget-Constrained AI Tutoring, arXiv:2606.20713](https://arxiv.org/pdf/2606.20713) `[found]`
