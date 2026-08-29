# ThermoQA

**Type:** benchmark
**One line:** A three-tier, 293-problem engineering thermodynamics benchmark with
programmatic CoolProp ground truth, evaluated across six frontier models.
**Why we care:** **This is the benchmark we were going to build.** It exists, it's better
than what we'd have made, and we should use it as an instrument rather than duplicate it.

## Structure

**293 open-ended problems**, ground truth computed programmatically via **CoolProp** — which
means the answers are correct by construction rather than by human transcription. Three
tiers of escalating complexity:

| Tier | Content | Items |
|---|---|---|
| **1** | Property lookups — enthalpy, entropy, phase identification from state specs | 110 |
| **2** | Component analysis — turbines, compressors, pumps, heat exchangers, at three depths: energy balance, entropy generation, exergy destruction | 101 |
| **3** | Full cycles — Rankine, Brayton, vapor-compression refrigeration, combined-cycle gas turbine | 82 |

Note that the tier structure maps closely onto
[our own skill graph's units](../../research/domain/skill-graph-draft.md) — U2/U6 properties,
U4 devices, U8 cycles. That's convenient and worth exploiting.

## Models and results

Six frontier LLMs from five providers, **three independent runs each**:
Claude Opus 4.6, GPT-5.4, Gemini 3.1 Pro, DeepSeek-R1, Grok 4, MiniMax M2.5.

| Tier | Top score | Range | Leader |
|---|---|---|---|
| 1 — properties | **97.9%** | 85.2–97.9% | Gemini |
| 2 — components | **92.1%** | 76.2–92.1% | Opus |
| 3 — cycles | **93.6%** | 52.7–93.6% | Opus |
| **Composite** | **94.1%** | 73.0–94.1% | **Opus** |

## The four findings that matter to us

**1. Memorization ≠ reasoning.** Rankings **reshuffle across tiers**. Gemini leads property
lookup (97.9%) but ranks third on full cycles (87.5%); Opus climbs from third to first.
Cross-tier degradation ranges **2.8 to 32.5 percentage points**. Property tables are
memorized; cycles are reasoned.

**2. Supercritical water is a discriminator.** Ten supercritical-region questions produced a
**44.5 percentage point spread**; even top performers dropped to 45–90%. The authors:
*"Models memorize discrete steam table entries... but cannot interpolate near the critical
point where properties change extremely nonlinearly."*

**3. Real fluids expose training-data bias.** **R-134a: 44–63% for every model**, against
75–98% on water. Vapor-compression refrigeration is a standard unit in every thermo course.
**This is where our tutor will be least reliable, and it's a whole chapter.**

**4. Single-run evaluations are misleading.** Run-to-run standard deviations ranged from
±0.1% (GPT-5.4, Tier 3) to ±2.5% (DeepSeek-R1, Tier 2). Reliability is a separate dimension
from accuracy, and one run doesn't measure it.

That fourth point deserves emphasis for our own evaluation design: **run everything three
times.** A tutor that is right on average and inconsistent in practice is not usable, and a
single run cannot tell you which one you have.

## What this changes about our project

Our [earlier plan](../../docs/03-open-questions.md) named "build a thermodynamics benchmark"
as our most likely publishable contribution. It's been done, and done well —
programmatic ground truth is better methodology than we'd likely have achieved by hand.

**Revised position:**
- **Use ThermoQA as an instrument.** Establish what our tutor's underlying model can do
  before building on it. Cheap, fast, and it makes our claims concrete.
- **The gap that remains is pedagogy, not correctness.** ThermoQA measures whether a model
  gets the right answer. Nothing measures whether it *teaches* thermodynamics well — the
  [MathTutorBench](../evaluation/mathtutorbench.md) axis. **That is still open, and it's
  now our clearest novel contribution.**

## Open questions

- [ ] **Is the dataset public?** Everything above depends on this. Find out first.
- [ ] Can we run our own tutor against it end-to-end?
- [ ] Does tool-calling for properties close the R-134a gap? Their harness may allow testing.
- [ ] What's the licence, and can we extend it with a pedagogy tier?
- [ ] Who are the authors, and would they collaborate?

## Connects to

- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis
- [UTQA](utqa.md) — the other thermo benchmark, opposite conclusion
- [property data tools](property-data-tools.md) — CoolProp is their ground truth *and* our
  proposed tool layer
- [MathTutorBench](../evaluation/mathtutorbench.md) — the axis nobody has built for thermo
- [our skill graph](../../research/domain/skill-graph-draft.md) — the tiers map onto our units

## Sources

- [ThermoQA: A Three-Tier Benchmark for Evaluating Thermodynamic Reasoning in Large Language Models, arXiv:2604.19758](https://arxiv.org/html/2604.19758v1) `[skimmed]` — **priority full read**
