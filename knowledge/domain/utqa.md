# UTQA

**Type:** benchmark
**One line:** A 50-item undergraduate thermodynamics benchmark covering ideal-gas processes,
reversibility, and **diagram interpretation** — on which no 2025-era model cleared the
authors' 95% competence bar.
**Why we care:** It's the paper that says, in print, that current LLMs are not suitable for
unsupervised thermodynamics tutoring. We should know its argument precisely, because it is
either the strongest case against our project or the clearest statement of the gap we fill.

> **Verification: `[read]` — full text, 2026-08-31.**

## The benchmark

Anna Geißler, Luca-Sophie Bien, Friedrich Schöppler, Tobias Hertel — Institute of Physical
and Theoretical Chemistry, **Julius-Maximilian University Würzburg**.

**50 single-choice items**, each with one correct answer and three distractors:
**33 text-only, 17 diagram-based**. Temperature 0.7, single-shot. **19 models** evaluated.

**The dataset is public: [huggingface.co/datasets/herteltm/UTQA](https://huggingface.co/datasets/herteltm/UTQA)** —
question texts, diagrams, answer keys, and solutions.

Item design is careful in a way worth copying: each stem isolates one construct, supplies
only necessary context, and **distractors encode real misconceptions** — the paper names
*"equating 'adiabatic' with 'reversible'"* and *"confusing dU with q"* — so accuracy
reflects reasoning rather than elimination by surface cues. Some items **omit axis labels
deliberately** to test structural understanding. Diagram types span p–V, T–S, H–p, U–V,
H–S, A–T.

Their motivating critique of existing benchmarks is sound and citable: GPQA's chemistry is
~80% organic recall with almost no entropy or reversibility; Humanity's Last Exam has the
same gap; SciBench's thermodynamics items are single-target calculations. (They note gpt-5
solved **all 26** SciBench items they judged topically aligned.)

## The results

**Text-only (33 items, 19 models):**
- Range **0.20** (gpt-3.5-turbo-0125) to **0.88** (DeepSeek R1); **grand mean 0.67**
- Above 0.80: gpt-5 high-effort, Gemini 2.5 Pro, Grok 3 Think, gpt-o3, DeepSeek R1
- Higher "reasoning budget" configurations beat lighter variants of the same family

**Diagram-based (17 items, 19 models):**
- **Mean 32%** — against a **25% random-guessing baseline**
- Weakest: **gpt-4.1 at 6%** — far *below* chance, i.e. systematically choosing distractors
- Strongest: **gpt-o3 at 76%**. Gemini 2.5 Pro 54%, gpt-o1 53%
- **gpt-o3 is the consistent exception** — it handles diagram-centric tasks far better than
  every other model tested

**Best overall across both: 82%. No model reached the authors' 95% competence threshold.**

**Prompting barely matters.** Seventeen prompt strategies were tested on gpt-4o (minimal,
suppressed-reasoning, CoT/ToT/GoT/CoS, elimination, persona, affective). Accuracies spanned
only **0.36–0.54**, and a two-phase "analyze then answer" format gave no significant gain.
Elimination-style prompts *underperformed*. Their conclusion: *"prompt design primarily
affects surface presentation and stability, but does little to correct deeper deficits in
scientific reasoning."*

**Linguistic degradation** (three perturbation families × two severities, ten runs each):
obscuring **logical clarity** hurt most (0.52 → 0.40), while moderate spelling or
terminology noise was tolerated. And **clause count showed no correlation with accuracy**
over a 1–20 range — failures reflect *conceptual integration*, not syntactic load.

The abstract's conclusion, verbatim: *"current LLMs are not yet suitable for unsupervised
tutoring in this domain."*

## The five error patterns — the most reusable list in this knowledge base

The paper names the consistent failure modes, and they map almost one-to-one onto our own
[misconception catalogue](../../research/domain/skill-graph-draft.md):

1. **Misuse of quasistatic templates despite explicit finite-rate cues**
2. **Entropy bookkeeping errors** — confusing transferred entropy with entropy production;
   applying ΔS formulas outside their domain of validity
3. **Path-dependence blind spots for work** — failing to reason with *oriented* areas in
   the p–V plane; mixing sign conventions
4. **Missed invariants and feasibility constraints** in optimization problems
5. **Numeric anchoring** to textbook exponents and constants without checking applicability

On diagrams specifically, models parse low-level features fine (axes, endpoints,
segmentation, curvature) and fail at the **binding stage**: computing and comparing signed
areas ∫p dV with correct orientation, binding leg types to axes (isochoric ↔ vertical in
p–V), enforcing feasibility across concatenated legs, and propagating state limits around a
cycle.

The authors note the human contrast: *"trained humans can often judge work or entropy trends
by quick perceptual comparison of path geometry, a classic advantage of visual reasoning."*
That perceptual shortcut is exactly what our students are being taught, and exactly what
models lack.

## The 95% threshold is the interesting move

Most benchmark papers report a score. UTQA sets a **competence threshold for a purpose** —
95% for unsupervised tutoring — and asks whether anyone clears it.

That's the right framing for our project and we should adopt it. "Claude scores X%" is not a
decision; "Claude does not clear the bar for unsupervised use in this region, therefore the
architecture must do Y" is.

We should set our own thresholds explicitly, per region, and design the system to behave
differently above and below them. → [grounding and verification](../concepts/grounding-and-verification.md)

## Why it disagrees with ThermoQA — and why that's informative

[ThermoQA](thermoqa.md) reports a 94.1% composite. UTQA reports 82% best, below threshold.
Same era, overlapping models.

The reconciliation:

| | UTQA | ThermoQA |
|---|---|---|
| Format | Single-choice | Open-ended computation |
| Ground truth | Authored | Programmatic (CoolProp) |
| **Diagrams** | **17 of 50 items** | **None** |
| Emphasis | Conceptual — reversibility, finite-rate | Computational — properties, components, cycles |

**They are measuring different capabilities, and both results are correct.** Models are good
at thermodynamic *computation* and bad at thermodynamic *seeing* and at *finite-rate
conceptual reasoning.*

That synthesis is more useful than either headline and only follows from reading both.
→ [LLM capability in thermodynamics](llm-thermodynamics-capability.md)

## The prompt-engineering finding

"Prompt phrasing and syntactic complexity showed modest to little correlation with
performance."

Worth stating plainly: **you cannot prompt-engineer your way out of this.** The failures are
capability failures, not instruction failures. The fix is architectural — tools,
verification, and scoping — not a better system prompt.

## Open questions

- [x] ~~Read the full paper~~ — done 2026-08-31
- [x] ~~Is the item set public?~~ **Yes** — [huggingface.co/datasets/herteltm/UTQA](https://huggingface.co/datasets/herteltm/UTQA).
      **Download it and inspect the 17 diagram items.**
- [ ] Where does 95% come from? The paper cites it (ref 17) but calls it "provisional."
      Chase the citation — we need a defensible threshold of our own.
- [ ] What is a "finite-rate/irreversible scenario" here, concretely? These map onto
      [our U5 knowledge components](../../research/domain/skill-graph-draft.md)
- [ ] Does the diagram gap close with better image resolution or structured input?
      → [diagram reading](diagram-reading.md)

## Connects to

- [ThermoQA](thermoqa.md) — the contrasting benchmark
- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis
- [diagram reading](diagram-reading.md) — the diagram items are the story
- [Hoffmann et al.](thermo-problem-benchmark.md) — the reversibility failure, independently

## Sources

- [Geißler, Bien, Schöppler & Hertel, "From Canonical to Complex: Benchmarking LLM Capabilities in Undergraduate Thermodynamics," arXiv:2508.21452](https://arxiv.org/abs/2508.21452) `[read]` — full text
- [UTQA dataset on HuggingFace](https://huggingface.co/datasets/herteltm/UTQA) `[found]` — **download this**
