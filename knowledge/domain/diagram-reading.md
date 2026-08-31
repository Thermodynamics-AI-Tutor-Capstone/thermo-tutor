# Diagram Reading

**Type:** concept / domain finding
**One line:** Multimodal models score ~32% on thermodynamic diagram items versus ~67% on
text — often at chance. P-v and T-s diagrams are load-bearing in our subject.
**Why we care:** This is the single biggest technical risk in our domain, it isn't fixed by
a better prompt, and it needs an explicit decision rather than a hope.

> **Substantially revised 2026-08-31 after reading [UTQA](utqa.md) and
> [Superstudent](superstudent-thermodynamics.md) in full.** The "32% wall" framing was too
> strong: the gap is real and large, but it is **model-specific**, and the best reasoning
> models substantially clear it.

## The numbers

**Thermodynamics specifically** ([UTQA](utqa.md), 17 diagram items, 19 models):

| | Accuracy |
|---|---|
| Mean across 19 models | **32%** |
| Text-only mean, same benchmark | **67%** |
| Random-guessing baseline | 25% |
| Weakest (gpt-4.1) | **6%** — *below chance*, i.e. systematically picking distractors |
| **Strongest (gpt-o3)** | **76%** |
| Gemini 2.5 Pro / gpt-o1 | 54% / 53% |

**The spread is the story, not the mean.** A 6%-to-76% range across contemporaneous models
is not a uniform capability ceiling — it is a capability that some models have and most
don't. UTQA's own wording: gpt-o3 is *"the notable exception, which consistently handles
diagram-centric tasks better than other models."*

**Corroborating evidence that the wall is passable:** in
[Superstudent](superstudent-thermodynamics.md), o3 sat a real German thermodynamics exam
that **included graphical input and required graphical output** — and outscored all 90
students, losing only *"minor"* points on graphical representations.

Errors, where they occur, arise *"chiefly in binding visual features to thermodynamic
meaning rather than in low-level recognition"*: models identify axes, reference markers,
segmentation, and curvature correctly, then fail to map them to physics. The recurring
binding failures are computing and comparing **signed** areas ∫p dV with correct
orientation, binding leg types to axes (isochoric ↔ vertical in p–V), enforcing feasibility
across concatenated legs, and propagating state limits around a cycle.

**Engineering diagrams generally:** questions with images are significantly harder than
text-only, and **visual data extraction accounts for 68.9% of errors** (MechVQA and related
work on mechanical drawing understanding).

## Why this is a wall, not a rough edge

Thermodynamics is taught **through** diagrams. A student who cannot place a state on a T-s
diagram does not understand the process. Sketching the process on P-v or T-s is a
cross-cutting skill in [our knowledge model](../../research/domain/skill-graph-draft.md) and
a standard instruction on nearly every problem.

Concretely, a tutor that can't read diagrams cannot:
- Look at a student's sketched cycle and say what's wrong with it
- Explain why a point sits in the two-phase region on *this* diagram
- Grade or discuss the "sketch the process" half of most problems
- Interpret a textbook figure the student is asking about

And the failure mode is the dangerous kind: **the model produces a confident, fluent,
plausible reading of a diagram it has misunderstood.** At chance-level accuracy with
full-confidence delivery, that is worse than declining.

## Three ways out

**1. Render, don't read — the promising one.**

Invert the pipeline. Instead of the model reading a diagram image, the *system* computes
thermodynamic state from tool calls
([CoolProp/Cantera](property-data-tools.md)) and **renders** the diagram from that state.
The model reasons over the structured state — numbers it can handle — and the student sees a
generated, correct diagram.

This sidesteps the failure entirely for anything the system generates. It handles neither
the student's own sketch nor a textbook figure, but it covers the common case, and it's
buildable.

**2. Structured input.** Have the student specify states numerically rather than sketch, and
generate the picture. Loses the pedagogical value of sketching, which is real.

**3. Scope it out.** Declare diagram interpretation out of scope, say so plainly in the
report, and cite the 32% figure as the reason. Honest and defensible.

**What is not an option is assuming *any* multimodal model handles it.** Most don't. The
model choice is load-bearing here in a way it isn't elsewhere in our architecture — which is
itself notable, since [everywhere else](../concepts/grounding-and-verification.md)
architecture beats model choice. Diagrams are the exception.

## The research opportunity

Nobody in this sweep has built a **diagram-native** engineering tutor using the render-don't-
read inversion. Given that the diagram gap is the documented wall in engineering AI tutoring
generally — not just thermodynamics — a working demonstration would be a real contribution,
and it's technically modest: CoolProp plus a plotting library plus structured state.

**Candidate Phase 3 prototype.** → [roadmap](../../admin/roadmap.md)

## Open questions

- [ ] **Re-run the diagram items ourselves.** The
      [UTQA dataset is public](https://huggingface.co/datasets/herteltm/UTQA) and has 17
      diagram items. Testing current Claude/GPT/Gemini on them is a few hours' work, gives
      us our own data, and directly decides whether we scope diagrams in or out.
      **Highest-value cheap experiment in the whole project.**
- [ ] Is o3's advantage reproducible in its successors, and does it hold on *student*
      hand-sketched diagrams rather than clean rendered ones?
- [ ] Does higher image resolution or a cropped region help?
- [ ] Can a model read a *generated* clean diagram better than a textbook scan or a phone
      photo of a hand sketch? (Likely yes, and it changes the design.)
- [ ] How much of thermo assessment actually requires diagram *reading* vs. diagram
      *production*? Audit a real problem set before deciding scope.

## Connects to

- [UTQA](utqa.md) — the source of the 32% figure
- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis
- [property data tools](property-data-tools.md) — the render-don't-read foundation
- [our skill graph](../../research/domain/skill-graph-draft.md) — `diagram-drawing` as a KC

## Sources

- [From Canonical to Complex (UTQA), arXiv:2508.21452](https://arxiv.org/abs/2508.21452) `[skimmed]` — 32% vs 67%
- [MechVQA: Benchmarking Multimodal LLMs on Mechanical Drawing Understanding, arXiv:2605.30794](https://arxiv.org/html/2605.30794v1) `[found]`
- [Do VLMs Reason Like Engineers? A Benchmark and a Stage-wise Evaluation, arXiv:2606.10833](https://arxiv.org/pdf/2606.10833) `[found]`
- [GraphRAG for Engineering Diagrams: ChatP&ID, arXiv:2603.22528](https://arxiv.org/pdf/2603.22528) `[found]` — an alternative structural approach
