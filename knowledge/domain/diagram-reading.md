# Diagram Reading

**Type:** concept / domain finding
**One line:** Reading a value off an axis is nearly solved; composing diagram geometry with a
governing physical law is not — and scaling has not fixed the second one.
**Why we care:** P–v and T–s diagrams are load-bearing in thermodynamics. This node decides
whether we scope them in, and how.

> **Rewritten 2026-08-31 after a full multimodal-literature read. Three corrections, marked ⚠.**

## The numbers

**Thermodynamics ([UTQA](utqa.md), 17 diagram items, 19 models):**

| | Accuracy |
|---|---|
| Mean across 19 models | **32%** |
| Text-only mean, same benchmark | **67%** |
| Random-guessing baseline | 25% |
| Weakest (gpt-4.1) | **6%** — *below chance*, systematically picking distractors |
| **Strongest (gpt-o3)** | **76%** |
| Gemini 2.5 Pro / gpt-o1 | 54% / 53% |

**⚠ Note that `gpt-5` and `gpt-5-high` are both in this benchmark and gpt-o3 still beats them
on diagrams.** Scale and recency did not monotonically close the gap; one newer model
*regressed* on it.

**Materials science (MatSciBench, arXiv:2510.12171)** — accuracy by image type, and the two
thermodynamics-adjacent categories are the worst in the whole benchmark:

| Image type | Accuracy |
|---|---|
| **Mechanical Plot** | **26.8%** |
| **Property Plot** | **31.1%** |
| **Phase Diagram** | **46.4%** |
| Crystal structure | 49.6% |
| Engineering schematic | 64.6% |
| Data table | 66.5% |

## ⚠ Correction 1: the 68.9% figure was misattributed *and* misused

This node previously cited "68.9% of errors are visual data extraction" as support for a
*binding-not-recognition* thesis. Both halves were wrong.

- **It is from MatSciBench, not MechVQA**, and it means *share of errors on image-bearing
  questions* (781 substantive multimodal errors), not share of all errors.
- **It argues the opposite of what we used it for.** MatSciBench finds **Visual Data
  Extraction is the dominant error source (68.9%, range 62.6–78.0%)**, with Domain Knowledge
  16.9%, Calculation 6.9%, Spatial/Geometric 4.1%. And for our diagram types specifically:
  *"Phase Diagram and Property Plot have the highest Visual Data Extraction shares among
  substantive errors, at 85.1% and 85.0%, respectively, **mainly due to misread temperatures,
  axis values, or interpolation along curved boundaries**."*

Interpolating along a curved boundary is exactly reading a saturation dome.

**Both findings can be true** — different domains, different error-attribution protocols
(MatSciBench uses an LLM error-classifier). But the honest framing is **not** "recognition is
fine, binding fails." It is: **reading engineering charts is unreliable, and the reasons
differ by chart type.** Use that framing; it is better supported and it justifies the same
architecture.

## ⚠ Correction 2: diagrams may not even be the bottleneck

**EngVQA** (arXiv:2606.10833, IIT Kharagpur) — 696 engineering problems, **thermodynamics is
its largest subject at 236 questions**. Stage-wise scoring of solution attempts:

| Stage | Qwen3-VL-8B | Gemini-2.5-Flash |
|---|---|---|
| **Visual Interpretation** | **7.49** | **8.72** ← *highest-scoring stage for both* |
| Equation Selection | 4.40 | 8.14 |
| Logical Reasoning | 4.11 | 7.48 |
| **Algebraic Accuracy** | **2.30** | **4.34** ← *the actual bottleneck* |
| Final Answer | 3.41 | 5.74 |

> *"algebraic calculation and sequential execution represent the primary cognitive bottlenecks
> for the generator model."*

Their visual-error-susceptibility scores peak at **0.59**, nowhere near 68.9%.

**This is a real tension in the literature and we should hold it honestly:** UTQA and
MatSciBench say diagram items are hard; EngVQA says that within a full solution attempt, the
arithmetic is harder than the seeing. Our architecture happens to address both — tool calls
fix the arithmetic, structured state fixes the seeing.

## ⭐ The strongest architectural evidence: ChatP&ID

**ChatP&ID** (arXiv:2603.22528, TU Delft) ran the controlled comparison our
"render, don't read" proposal needs. Same questions, same models, five representations of the
same piping-and-instrumentation diagrams:

| Representation | GPT-5 accuracy / cost | GPT-4o-mini |
|---|---|---|
| **Conceptual-level graph** | **0.94 / $0.027** | **0.78** |
| Process-level graph | 0.93 / $0.055 | 0.72 |
| Complete-level graph | 0.90 / $0.113 | 0.71 |
| **Raw flowsheet image** | **0.76 / $0.001** | **0.55** |
| Full DEXPI XML file | 0.89 / $0.175 | 0.71 |

**Structured representation beats the raw image by +18 points (GPT-5) and +23 points
(GPT-4o-mini), at 85% lower cost than the full XML.**

Two refinements that shape the design:

1. **The most *abstract* representation won.** Complete-level graphs scored *worse* than
   conceptual ones, and small models degrade monotonically as representation complexity rises.
   **Do not dump the full property object into context** — pass the minimal state needed.
2. **Images are adequate for qualitative questions and bad for precise ones.** With multimodal
   context: summarization 0.95, knowledge inference 0.91, but multi-query retrieval 0.85, path
   exploration 0.80, single graph query 0.79. **Route by question type** rather than banning
   images outright.

## ⭐ Why prompting cannot fix it: edge direction is at chance

*Nodes Are Early, Edges Are Late* (arXiv:2603.02865, Tohoku/NTT) probed a VLM's internal
representations on synthetic directed graphs:

| Visual attribute | Chance | Model |
|---|---|---|
| Node colour | 12.5 | 91.4 |
| Node shape | 20.0 | 76.6 |
| Edge existence | 50.0 | 69.6 |
| **Edge direction** | **50.0** | **49.3** ← *at chance* |
| Edge count | 20.0 | 21.6 |

> *"node information and global structural features are already linearly encoded in individual
> hidden states of the vision encoder… **edge information is not linearly separable in the
> vision encoder** and becomes linearly encoded only in the text tokens in the language model."*

**This is the mechanistic explanation for UTQA's signed-area failure.** Direction around a
thermodynamic cycle *is* an edge-direction property — and it is the one visual attribute these
models demonstrably do not encode. Compression vs. expansion, the sign of ∫p dV, the direction
of a Carnot loop: all of it rides on the attribute that sits at chance.

**Cycle direction must be carried in structured state, never read off a rendered arrow.**

## ⚠ Correction 3: hand-drawn student sketches — the 2024 result was a pipeline artifact

Two papers, apparently contradictory, and the reconciliation matters:

**(a) Kortemeyer, Nohl & Onishchuk (arXiv:2406.17859, ETH Zurich, 2024)** — grading a real
**252-student thermodynamics exam**. Problem 2a was literally *"Drawing of the engine process
qualitatively in a T-s diagram, marking relevant states."*

Result: **zero correlation with human graders on the two graphical problems.** But the cause
was transcription, not reasoning: *"graphs… were also 'overlooked' by GPT-4V when processing a
complete page"* and *"quite often, MathPix ignored these graphs."* Non-graphical problems
reached R² = 0.58–0.77.

**(b) SketchJudge (arXiv:2601.06944, 2026)** — 1,015 hand-drawn student answers fed **directly**
to modern MLLMs, no transcription step:

| | Accuracy | ebF1 |
|---|---|---|
| Human (non-expert raters) | 83.33 | 66.42 |
| **GPT-5** | **78.42** | 61.13 |
| Gemini-2.5-Flash | 77.74 | 58.30 |
| Claude-3.7-Sonnet | 73.00 | 57.11 |
| Random | 50.00 | — |

Physics subset: GPT-5 **73.4%** vs human 81.7%.

**The reconciliation: never route a student's sketch through a transcription step.** Feed the
image directly. The 2024 zero-correlation is a GPT-4V/MathPix pipeline artifact, not a ceiling.

**And two prompting results that invert our assumptions:**

| Model | Baseline | Rubric | **CoT** |
|---|---|---|---|
| Gemini-2.5-Flash | 77.74 | 76.95 | **76.16** |
| GLM-4.6V | 69.16 | 70.15 | **64.63** |
| Qwen2.5-VL-72B | 66.40 | 67.19 | **66.01** |

> *"Rubric prompting yields only modest and model-dependent changes… In contrast, **CoT
> prompting consistently hurts performance for all three models**."*

CoT raises the false-negative rate — the model becomes over-strict and rejects correct
sketches. **Do not add chain-of-thought to diagram grading.** Independently, the GPT-5
chart-reading study found prepending generated chart descriptions was non-significant overall
and **significantly negative on complex charts**.

## Is the gap closing?

**Yes on clean conventional charts.** GPT-5 scores **92.3% on TUG-K** (graph slope/area
interpretation — the closest analogue to a P–v area question) versus GPT-4o at 50.4%. And on
adversarial CHART-6 items, GPT-5 beat GPT-4o by **20–40 percentage points**, with a
pre-registered regression showing the lever is **model architecture, not prompting**
(model β = 1.469, p < 0.001; prompt conditions p = 0.93 and p = 0.36).

**No on domain-specific engineering plots.** MatSciBench property/phase plots 26.8–46.4%;
MechVQA projection/multi-view 58–60% for frontier models; UTQA diagram mean 32%.

**And the single most encouraging counter-datapoint is in our own domain:** on the RPTU exam,
[o3 constructed both a p,V diagram with isotherms and a T,s diagram with isobars](superstudent-thermodynamics.md),
marking states 1–6 and shading heat input, losing only *"minor"* points. That is diagram
**generation**, not reading — which is precisely the direction our architecture points.

## What we should actually do

1. **Render, don't read, for anything we generate.** Compute state via
   [CoolProp/Cantera](property-data-tools.md) and render the diagram. Evidence: ChatP&ID's
   +18–23 points and 85% cost reduction.
2. **Keep the structured representation minimal.** Conceptual beat complete in ChatP&ID.
3. **Carry cycle direction and state ordering as data**, never as a rendered arrow.
4. **For student sketches: feed the image directly, supply a programmatically rendered
   reference diagram alongside, use a plain or lightly-rubriced prompt, and do not add CoT.**
5. **Route by question type** — images are fine for "what kind of process is this?" and bad for
   "what is the area under this curve?"
6. **Run the [UTQA diagram items](utqa.md) ourselves** before committing. Still the cheapest
   high-value experiment we have.

## The research opening

**Nobody generates engineering diagrams from computed state for pedagogical purposes.**
DiagrammerGPT does general diagram generation; SketchJudge renders references only as benchmark
ground truth; ThermoQA computes CoolProp state and emits numbers, never plots;
[Stan](../systems/stan-udel.md) has no diagram component at all. That gap is real, it is
technically modest (CoolProp + matplotlib + structured state), and it is a defensible novelty
claim. → [roadmap](../../admin/roadmap.md)

## Open questions

- [ ] Run current models on the 17 UTQA diagram items ourselves (gated — see [UTQA](utqa.md))
- [ ] Does o3's diagram advantage persist in its successors?
- [ ] Kortemeyer's exam-logistics recommendations are directly usable if we ever collect
      handwritten work: OCR-friendly page headers, one problem part per page, **pencils not
      pens** (scribbled-out work makes OCR hallucinate), encourage students to write *more*,
      grade one part at a time, and **do not include the problem text in the OCR prompt** —
      the model "sees what it expects to see."

## Connects to

- [UTQA](utqa.md) — the 32% figure and the binding-error taxonomy
- [Superstudent](superstudent-thermodynamics.md) — o3 *constructing* T-s and p,V diagrams
- [property data tools](property-data-tools.md) — the render-don't-read foundation
- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis

## Sources

- [Geißler et al., UTQA, arXiv:2508.21452](https://arxiv.org/abs/2508.21452) `[read]`
- [MatSciBench, arXiv:2510.12171](https://arxiv.org/abs/2510.12171) `[read]` — **source of the 68.9% figure, correctly attributed**
- [Alimin & Schweidtmann, ChatP&ID, arXiv:2603.22528](https://arxiv.org/abs/2603.22528) `[read]` — the controlled representation comparison
- [Do VLMs Reason Like Engineers? (EngVQA), arXiv:2606.10833](https://arxiv.org/abs/2606.10833) `[read]`
- [MechVQA, arXiv:2605.30794](https://arxiv.org/abs/2605.30794) `[read]`
- [Yoshida et al., "Nodes Are Early, Edges Are Late," arXiv:2603.02865](https://arxiv.org/abs/2603.02865) `[read]` — edge direction at chance
- [SketchJudge, arXiv:2601.06944](https://arxiv.org/abs/2601.06944) `[read]` — hand-drawn student sketches; CoT harmful
- [Kortemeyer, Nohl & Onishchuk, "Grading Assistance for a Handwritten Thermodynamics Exam," arXiv:2406.17859](https://arxiv.org/abs/2406.17859) `[read]` — **252-student thermodynamics exam**; the transcription artifact
- [Yang & Chen, "GPT-5 Corrected GPT-4V's Chart Reading Errors, Not Prompting," arXiv:2510.06782](https://arxiv.org/abs/2510.06782) `[read]`
- [Polverini & Gregorcic, "Multimodal LLMs and physics visual tasks," arXiv:2506.19662](https://arxiv.org/abs/2506.19662) `[read]` — TUG-K graph reading at 92.3%
