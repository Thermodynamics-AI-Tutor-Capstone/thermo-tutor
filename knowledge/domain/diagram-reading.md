# Diagram Reading

**Type:** concept / domain finding
**One line:** Multimodal models score ~32% on thermodynamic diagram items versus ~67% on
text — often at chance. P-v and T-s diagrams are load-bearing in our subject.
**Why we care:** This is the single biggest technical risk in our domain, it isn't fixed by
a better prompt, and it needs an explicit decision rather than a hope.

## The numbers

**Thermodynamics specifically:** across **19 models**, mean accuracy on thermodynamic
diagram tasks was **32%** — less than half the text-only mean of **67%**. Errors arise
*"chiefly in binding visual features to thermodynamic meaning rather than in low-level
recognition"*: models identify axes, reference markers, and basic curve characteristics, and
then misread what they mean. → [UTQA](utqa.md)

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

**What is not an option is assuming multimodal models handle it.** They don't, and the
literature is unambiguous.

## The research opportunity

Nobody in this sweep has built a **diagram-native** engineering tutor using the render-don't-
read inversion. Given that the diagram gap is the documented wall in engineering AI tutoring
generally — not just thermodynamics — a working demonstration would be a real contribution,
and it's technically modest: CoolProp plus a plotting library plus structured state.

**Candidate Phase 3 prototype.** → [roadmap](../../admin/roadmap.md)

## Open questions

- [ ] Do the newest multimodal models close the gap? **The 19-model figure will age; re-run
      it ourselves on a handful of real P-v/T-s items.** Cheap, and it's our own data.
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
