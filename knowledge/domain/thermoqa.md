# ThermoQA

**Type:** benchmark
**One line:** A three-tier, 293-problem engineering thermodynamics benchmark with
programmatic CoolProp ground truth, evaluated across six frontier models.
**Why we care:** **This is the benchmark we were going to build.** It exists, it's better
than what we'd have made, and we should use it as an instrument rather than duplicate it.

> **Verification: `[read]` — full text, 2026-08-31.**
>
> **The dataset and code are open source:
> [huggingface.co/datasets/olivenet/thermoqa](https://huggingface.co/datasets/olivenet/thermoqa).**
> That answers the blocking open question on this node: we can run it.
>
> **Provenance note, in fairness:** single author, Kemal Düzkar, at Olivenet (Kyrenia,
> Cyprus) — not a university lab. The methodology is sound and reproducible by construction,
> but this has not had the scrutiny [UTQA](utqa.md) got. Verify a sample of ground-truth
> answers ourselves before relying on it.

## Structure

**293 open-ended problems**, ground truth computed programmatically from **CoolProp 7.2.0**
(IAPWS-IF97 for water, Helmholtz EOS for R-134a) plus **NASA 7-coefficient polynomials** for
variable-cₚ air, **cross-verified to <0.01% against NIST**. No hand-authored solutions.

Four working fluids (water, air, R-134a, combined air+water), seven device types, ten cycle
variants, three analysis depths (energy balance, entropy generation, exergy destruction).

Their framing of why thermodynamics is a good testbed is worth borrowing: *"A 2% error in
enthalpy at the turbine inlet can cascade into a 10% error in cycle thermal efficiency."*
Errors propagate, and open-ended calculation removes the guessing advantage of
multiple choice.

Three tiers of escalating complexity:

| Tier | Content | Items |
|---|---|---|
| **1** | Property lookups — enthalpy, entropy, phase identification from state specs | 110 |
| **2** | Component analysis — turbines, compressors, pumps, heat exchangers, at three depths: energy balance, entropy generation, exergy destruction | 101 |
| **3** | Full cycles — Rankine, Brayton, vapor-compression refrigeration, combined-cycle gas turbine | 82 |

Note that the tier structure maps closely onto
[our own skill graph's units](../../research/domain/skill-graph-draft.md) — U2/U6 properties,
U4 devices, U8 cycles. That's convenient and worth exploiting.

## Models and results

Six frontier LLMs from five providers, **three independent runs each**, reasoning/thinking
modes at highest setting: Claude Opus 4.6, GPT-5.4, Gemini 3.1 Pro, DeepSeek-R1, Grok 4,
MiniMax M2.5.

**Composite leaderboard:** Claude Opus 4.6 **94.1%** · GPT-5.4 **93.1%** · Gemini 3.1 Pro
**92.5%**

| Tier | Top score | Range | Leader |
|---|---|---|---|
| 1 — properties | **97.9%** | 85.2–97.9% | Gemini |
| 2 — components | **92.1%** | 76.2–92.1% | Opus |
| 3 — cycles | **93.6%** | 52.7–93.6% | Opus |
| **Composite** | **94.1%** | 73.0–94.1% | **Opus** |

**Cross-tier degradation: 2.8 pp (Opus) to 32.5 pp (MiniMax).**

## The scoring scheme — steal this

Their grading design solves a problem we will otherwise solve badly:

- **±2% relative OR ±0.5 absolute**, whichever is more lenient. The 2% figure is chosen to
  match **standard engineering homework tolerance (Çengel et al., 2019)** and to exceed
  IAPWS-IF97's own <0.1% uncertainty — so it measures *model* error, not reference error.
- **Step-level weights** on Tiers 2 and 3 (5–12 steps and 15–60 steps respectively), so a
  correct method with one bad lookup doesn't score zero and a lucky final number doesn't
  score full marks.
- **Dimensionless quantities (η_th, η_II, COP) get a tighter ±0.02 absolute tolerance** —
  they found the default ±0.5 absolute was passing values with **>20% error**. A subtle,
  real trap for anyone building a thermo grader.
- **One canonical prompt**, deliberately, citing [UTQA's](utqa.md) finding that prompt
  variation doesn't fix reasoning deficits.
- **Reference states pinned explicitly** — R-134a uses the **IIR reference state**
  (h = 200 kJ/kg, s = 1.0 kJ/(kg·K) at 0 °C). Exactly the discipline our
  [property tools node](property-data-tools.md) warns is necessary.

## The four findings that matter to us

**1. Memorization ≠ reasoning.** Rankings **reshuffle across tiers**. Gemini leads property
lookup (97.9%) but ranks third on full cycles (87.5%); Opus climbs from third to first.
Cross-tier degradation ranges **2.8 to 32.5 percentage points**. Property tables are
memorized; cycles are reasoned.

**2. Supercritical water is a discriminator.** Ten questions above T = 373.95 °C and
P = 22.064 MPa produced a **44.5 pp spread**; even top performers dropped to 45–90%. The
authors: *"Models memorize discrete steam table entries... but cannot interpolate near the
critical point where properties change extremely nonlinearly."* One cited case: the model's
answer against IAPWS-IF97's h = 2,585.8 kJ/kg was **27% off**.

**3. Real fluids expose training-data bias.** **R-134a: 44–63% for every model**, against
75–98% on water. The named causes are mechanically specific and teachable: **double
interpolation to find h₂ₛ from (s₁, P₂)** for isentropic efficiency, plus the general
sparsity of R-134a tables in training data. Vapor-compression refrigeration is a standard
unit in every thermo course. **This is where our tutor will be least reliable, and it's a
whole chapter.**

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

- [x] ~~Is the dataset public?~~ **Yes** — [huggingface.co/datasets/olivenet/thermoqa](https://huggingface.co/datasets/olivenet/thermoqa), dataset *and* code.
- [ ] **Spot-check the ground truth ourselves** against textbook tables before relying on it.
      Single-author, non-academic provenance warrants it, and it's an afternoon's work.
- [ ] **Does tool-calling for properties close the R-134a gap?** Their harness makes this
      directly testable. **Highest-value experiment on this node** — it validates or kills
      our property-tools layer with real numbers.
- [ ] Licence terms, and can we extend it with a pedagogy tier?
- [ ] Contact the author: `kemal.duzkar@olivenet.io`

## Connects to

- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis
- [UTQA](utqa.md) — the other thermo benchmark, opposite conclusion
- [property data tools](property-data-tools.md) — CoolProp is their ground truth *and* our
  proposed tool layer
- [MathTutorBench](../evaluation/mathtutorbench.md) — the axis nobody has built for thermo
- [our skill graph](../../research/domain/skill-graph-draft.md) — the tiers map onto our units

## Sources

- [Düzkar, "ThermoQA: A Three-Tier Benchmark for Evaluating Thermodynamic Reasoning in Large Language Models," arXiv:2604.19758](https://arxiv.org/abs/2604.19758) `[read]` — full text
- [Dataset + code on HuggingFace](https://huggingface.co/datasets/olivenet/thermoqa) `[found]` — **download and verify**
