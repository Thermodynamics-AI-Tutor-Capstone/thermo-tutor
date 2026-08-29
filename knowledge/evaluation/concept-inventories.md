# Concept Inventories

**Type:** instrument
**One line:** Validated multiple-choice instruments that measure conceptual understanding
rather than problem-solving skill — including a thermodynamics one developed at Penn State.
**Why we care:** They are the defensible answer to "how do you know they learned anything,"
and one of them is ours institutionally.

## The idea

Patterned on the **Force Concept Inventory** (physics, 1992), which changed physics education
research by giving everyone a common yardstick. Design constraints:

- **Brief** — one class period
- **Minimal or no computation** — measures understanding, not arithmetic
- **Repeatable across diverse populations**
- **Distractors are real misconceptions**, so wrong answers are diagnostic

Typically administered **pre and post**, reporting **normalized gain**:

```
g = (post − pre) / (100 − pre)
```

Normalized gain rather than raw gain, because students starting higher have less room to
improve.

## The thermodynamics instruments

**Thermodynamics Concept Inventory (TCI)** — developed **at Penn State**, patterned on the
FCI, for engineering courses. Tests the change in conceptual understanding across an
introductory engineering thermodynamics course.

**Thermal and Transport Concept Inventory — Thermodynamics (TTCI-T)** — a related instrument,
also engineering-specific.

Both catalogued on **PhysPort**, which also publishes a
[which-should-I-use guide](https://www.physport.org/recommendations/Entry.cfm?ID=124933).

**The TCI was developed here.** That's not a small thing: it removes the largest
methodological objection to a capstone learning study, and the institutional connection is a
plausible route to both access and advice.

## Access — start early

PhysPort gates instruments behind **educator verification**. Students can't just download
them; test security is the whole point. Our instructor sponsor is the path.
→ [Canvas access questions](../../admin/canvas-access.md)

**This is slow. Request it in Phase 0.** → [roadmap](../../admin/roadmap.md)

## The measurement choice we have to make

Concept inventories measure **conceptual understanding**. Course grades measure
**problem-solving performance**. These are different, they can move independently, and the
education literature is full of interventions that shift one and not the other.

Worse, they can move in *opposite* directions — which is exactly what
[Bastani](../evidence/bastani-2025-harm.md) found between assisted practice performance
(+127%) and unassisted learning (≈0).

**Decide before collecting anything**, or we'll be accused — fairly — of choosing the metric
that won. → [open question C3](../../docs/03-open-questions.md)

Candidate primary outcomes, with honest trade-offs:

| Outcome | For | Against |
|---|---|---|
| **TCI normalized gain** | Validated, published, PSU-developed, defensible | Measures concepts, not the problem-solving our tutor mostly touches |
| Course exam performance | What students and instructors care about | Confounded by everything; needs instructor cooperation |
| Voluntary week-10 return rate | **The field's actual failure mode**; nobody reports it | Not a learning measure |
| Time-to-solution | Cheap, continuous, automatic | Faster is not better — see productive failure |

**A defensible combination:** TCI as the primary learning outcome, **voluntary return rate as
a co-primary**, with process metrics as secondary. The return-rate measure is the one where
we're most likely to produce something the field doesn't already have.
→ [engagement decay](../concepts/engagement-decay.md)

## Open questions

- [ ] Can the instructor sponsor get us PhysPort educator verification? **Ask in week 1.**
- [ ] TCI or TTCI-T for the specific PSU course? PhysPort's guide answers this.
- [ ] Who developed the TCI at Penn State, and are they reachable?
- [ ] What sample size do we need to detect a plausible effect? **Run the power calculation
      early** — it may show that a learning-gain headline is out of reach at our n, which
      would be extremely useful to know before designing the study around it.
- [ ] Are there published TCI norms to compare against?

## Connects to

- [Kestin 2025](../evidence/kestin-2025-rct.md) — what did they measure? Model for us
- [MathTutorBench](mathtutorbench.md) — measuring the *tutor* rather than the student
- [engagement decay](../concepts/engagement-decay.md) — the co-primary outcome argument
- [open questions C3](../../docs/03-open-questions.md) — the outcome decision

## Sources

- [PhysPort — Thermodynamics Concept Inventory (TCI)](https://www.physport.org/assessments/assessment.cfm?A=TCI) `[skimmed]`
- [PhysPort — TTCI-T](https://www.physport.org/assessments/assessment.cfm?A=TTCIT) `[skimmed]`
- [PhysPort — which thermodynamics assessment should I use?](https://www.physport.org/recommendations/Entry.cfm?ID=124933) `[skimmed]`
- [Development of Engineering Thermodynamics Concept Inventory instruments — Penn State record](https://pure.psu.edu/en/publications/development-of-engineering-thermodynamics-concept-inventory-instr-2/) `[skimmed]` · [IEEE](https://ieeexplore.ieee.org/document/963691) `[found]`
- [Resource Letter RBAI-1: Research-based Assessment Instruments in Physics and Astronomy, arXiv:1605.02703](https://arxiv.org/pdf/1605.02703) `[found]`
