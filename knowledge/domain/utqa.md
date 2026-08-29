# UTQA

**Type:** benchmark
**One line:** A 50-item undergraduate thermodynamics benchmark covering ideal-gas processes,
reversibility, and **diagram interpretation** — on which no 2025-era model cleared the
authors' 95% competence bar.
**Why we care:** It's the paper that says, in print, that current LLMs are not suitable for
unsupervised thermodynamics tutoring. We should know its argument precisely, because it is
either the strongest case against our project or the clearest statement of the gap we fill.

## The benchmark

From Julius-Maximilian University Würzburg. **50 items**, single-choice, covering ideal-gas
processes, reversibility, and diagram interpretation. Reported as **33 text-only and 17
diagram-based**.

**19 models** evaluated.

## The results

- **Best overall: 82% (GPT-o3)**
- **No model exceeded the authors' 95% competence threshold**
- Text-only items outperformed image reasoning, which **often fell to chance**
- Prompt phrasing and syntactic complexity showed **modest to little correlation** with
  performance
- The gap concentrates in **finite-rate / irreversible scenarios** and in **binding visual
  features to thermodynamic meaning**

The abstract's conclusion, verbatim: *"current LLMs are not yet suitable for unsupervised
tutoring in this domain."*

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

- [ ] **Read the full paper.** Which 19 models, and the per-item breakdown.
- [ ] Is the item set public? 50 items is small enough to inspect fully, and inspecting the
      17 diagram items would tell us a lot.
- [ ] Where does 95% come from? Is it justified or asserted?
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

- [From Canonical to Complex: Benchmarking LLM Capabilities in Undergraduate Thermodynamics, arXiv:2508.21452](https://arxiv.org/abs/2508.21452) `[read — abstract]` `[skimmed — full text]` — abstract read verbatim; PDF cached locally
