# LLM Capability in Thermodynamics

**Type:** concept / synthesis
**One line:** Frontier models can beat every human who ever sat a thermodynamics exam, and
still be wrong one time in three on refrigerant problems. Both are documented.
**Why we care:** This is the central technical fact about our domain, and it determines what
our architecture has to do.

## Four results that appear to contradict each other

| Study | Setup | Headline |
|---|---|---|
| [Superstudent](superstudent-thermodynamics.md) | o3, zero-shot, a real university thermo exam | Solved **all** problems correctly — better than **every** student, in the range of the best scores across **10,000+** exams since 1985 |
| [ThermoQA](thermoqa.md) | 293 open-ended problems, CoolProp ground truth, 6 frontier models × 3 runs | Best composite **94.1%** (Claude Opus 4.6). **R-134a: 44–63% for every model** |
| [UTQA](utqa.md) | 50 items, 19 models, incl. diagrams | Best **82%** (o3). **No model** clears the authors' 95% tutoring threshold |
| [Hoffmann et al.](thermo-problem-benchmark.md) | 22 problems, 5 models, 3 repetitions | On an adiabatic process with reversibility unstated, **every model assumed reversible, every time** |

They're all correct. Reconciling them gives the single most important design fact we have.

## The resolution: peak capability is superhuman, reliability is not

**Tutoring is a worst-case discipline. Benchmarks report averages.**

A model that aces a hard exam and then scores 44% on R-134a is not a bad model — it's a
brilliant TA who is wrong a third of the time on the refrigeration unit **and never
signals which third.** For a student who cannot yet tell right from wrong in this subject —
which is the definition of the student we're serving — an unflagged 56% error rate on a
whole unit is worse than no help.

That reframes what "good enough" means. The relevant question is not *what does the model
score*, it's *can the system tell when it's in a region where the model is unreliable, and
do something else there.*

## The three named failure modes

### 1. Unstated assumptions — the deepest problem

On a problem where the text doesn't say whether an adiabatic process is reversible,
assuming reversibility is wrong. **Every model tested made that assumption, in every
repetition.**

This is not hallucination. It's a **plausible, standard, unwarranted engineering
assumption, stated confidently** — which is exactly the error our students make. A tutor
that does this doesn't just give a wrong answer; it *validates the misconception* with
apparent authority.

The mirror image is the opportunity: **"which assumptions are licensed by this problem
statement" is arguably the most valuable thing a thermodynamics tutor could teach, and it
is precisely what base models cannot do.** It's a cross-cutting skill in
[our skill graph](../../research/domain/skill-graph-draft.md) and it is near-absent from
standard assessment. → [knowledge components](../concepts/knowledge-components.md)

### 2. Diagrams — the hard wall

Mean accuracy across 19 models on thermodynamic diagram items: **32%**, versus **67%**
text-only. Often at chance. Errors are in *binding visual features to thermodynamic
meaning*, not low-level recognition — models find the axes and misread what they mean.

P-v and T-s diagrams are load-bearing in this subject. This is not a rough edge.
→ [diagram reading](diagram-reading.md)

### 3. Real fluids and edge regions

ThermoQA's most actionable finding:

| Substance / region | Model accuracy |
|---|---|
| Water | 75–98% |
| **R-134a** | **44–63%** — every model |
| Supercritical water | 45–90%, 44.5pp spread |

A training-data bias with a direct curricular consequence: **the refrigeration unit is
where our tutor will be least reliable**, and vapor-compression cycles are everywhere in a
thermo course.

## What this means for architecture

1. **Property data comes from tools, never weights.** Non-negotiable.
   → [property data tools](property-data-tools.md)
2. **Verification before display.** Any number the tutor states must trace to a tool call.
   → [grounding and verification](../concepts/grounding-and-verification.md)
3. **Region-aware confidence.** The system should know that R-134a and supercritical
   states are low-confidence territory and behave differently there — escalate, hedge, or
   show its work.
4. **Assumption-checking as a first-class feature**, not an emergent behavior.
5. **Decide about diagrams explicitly.** Either solve it structurally (render diagrams from
   computed state rather than reading images) or scope them out and say so.

## The contradiction we should keep visible

UTQA says "not suitable for unsupervised tutoring" (best 82%, threshold 95%).
ThermoQA says 94.1% composite. Same era, overlapping models.

Why they differ: **UTQA is multiple-choice including diagram items** (which crater the
score); **ThermoQA is open-ended computation with programmatic CoolProp ground truth** and
no diagrams. They are measuring different things and both are right.

The synthesis: **models are good at thermodynamic computation and bad at thermodynamic
seeing.** That is a much more actionable statement than either paper's headline, and it
follows only from reading both.

## Open questions

- [ ] Where exactly is the reliability boundary? A capability map by
      substance × region × process type would be genuinely useful and is buildable from
      existing benchmarks.
- [ ] Does tool-calling for properties fix the R-134a gap, or is the reasoning also wrong?
      **Directly testable, and a good Phase 3 spike.**
- [ ] Can a model be made to *know* when it's in a low-confidence region?
- [ ] Do the failures correlate with where *students* fail? (If so, the tutor is
      unreliable exactly where it's most needed.)

## Connects to

- [ThermoQA](thermoqa.md) · [UTQA](utqa.md) · [Superstudent](superstudent-thermodynamics.md) · [Hoffmann et al.](thermo-problem-benchmark.md)
- [diagram reading](diagram-reading.md) · [property data tools](property-data-tools.md)
- [grounding and verification](../concepts/grounding-and-verification.md)
- [our skill graph](../../research/domain/skill-graph-draft.md)

## Sources

See the individual benchmark nodes linked above.
