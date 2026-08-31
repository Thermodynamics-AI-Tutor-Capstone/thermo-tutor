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

## ⚠ The thermodynamics instruments — and a blocking correction

> **Corrected 2026-08-31 after reading PhysPort's own entry.** This node previously named the
> **Thermodynamics Concept Inventory (TCI)** as our validated, Penn-State-developed primary
> outcome measure. **Both halves of that were wrong, and the instrument should probably not
> be our primary measure at all.**

**Thermodynamics Concept Inventory (TCI)** — developer **Clark Midkiff**
(`Cmidkiff@eng.ua.edu`, University of Alabama). Pre/post multiple choice for introductory
college thermodynamics.

Per PhysPort:

- **The developers explicitly discourage its use**, noting that *"the development of the
  test was never finished."*
- It carries **PhysPort's lowest level of research-based validation.**
- No published psychometrics, reliability coefficients, or normative scores are available.
- Anyone interested must contact the developer directly.

**What this means for us:** our planned primary learning outcome was an unfinished instrument
whose own author advises against using it. Building a capstone's central claim on it would
have been a serious methodological error, and an obvious target for any reviewer who checked.

**The Penn State connection is also weaker than stated.** The
[PSU publication record](https://pure.psu.edu/en/publications/development-of-engineering-thermodynamics-concept-inventory-instr-2/)
for "Development of Engineering Thermodynamics Concept Inventory instruments" is real, but
the instrument PhysPort catalogues is attributed to Midkiff at Alabama. **Someone needs to
untangle the authorship before we claim an institutional connection to anyone.**

## What to use instead

PhysPort's own recommended alternatives:

- **Thermal and Transport Concept Inventory — Thermodynamics (TTCI-T)** — engineering-specific
  and, on PhysPort's ratings, better validated. **This is now the leading candidate.**
- **Survey of Thermodynamic Processes (STP)** — the other suggestion.
- PhysPort's [which-should-I-use guide](https://www.physport.org/recommendations/Entry.cfm?ID=124933)
  is the right starting point, and we should follow it rather than pick by name recognition.

## Access — start early

PhysPort gates instruments behind **educator verification**. Students can't download them;
test security is the point. Our instructor sponsor is the path.
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
| **TTCI-T normalized gain** | Engineering-specific, better validated than the TCI | Measures concepts, not the problem-solving our tutor mostly touches. Access is gated and slow |
| ~~TCI normalized gain~~ | — | **Unfinished instrument; developers discourage use. Do not build on it.** |
| Course exam performance | What students and instructors care about | Confounded by everything; needs instructor cooperation |
| Voluntary week-10 return rate | **The field's actual failure mode**; nobody reports it | Not a learning measure |
| Time-to-solution | Cheap, continuous, automatic | Faster is not better — see productive failure |

**A defensible combination:** TCI as the primary learning outcome, **voluntary return rate as
a co-primary**, with process metrics as secondary. The return-rate measure is the one where
we're most likely to produce something the field doesn't already have.
→ [engagement decay](../concepts/engagement-decay.md)

## Open questions

- [ ] Can the instructor sponsor get us PhysPort educator verification? **Ask in week 1.**
- [ ] **TTCI-T or Survey of Thermodynamic Processes** for the specific PSU course? Follow
      PhysPort's recommendation guide. **The TCI is off the table unless Midkiff says
      otherwise.**
- [ ] Untangle the TCI authorship: what is the actual relationship between the PSU
      publication record and Midkiff's instrument?
- [ ] Contact Clark Midkiff (`Cmidkiff@eng.ua.edu`) — he may know what the field now uses.
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

- [PhysPort — Thermodynamics Concept Inventory (TCI)](https://www.physport.org/assessments/assessment.cfm?A=TCI) `[read]` — **source of the correction above**
- [PhysPort — TTCI-T](https://www.physport.org/assessments/assessment.cfm?A=TTCIT) `[skimmed]`
- [PhysPort — which thermodynamics assessment should I use?](https://www.physport.org/recommendations/Entry.cfm?ID=124933) `[skimmed]`
- [Development of Engineering Thermodynamics Concept Inventory instruments — Penn State record](https://pure.psu.edu/en/publications/development-of-engineering-thermodynamics-concept-inventory-instr-2/) `[skimmed]` · [IEEE](https://ieeexplore.ieee.org/document/963691) `[found]`
- [Resource Letter RBAI-1: Research-based Assessment Instruments in Physics and Astronomy, arXiv:1605.02703](https://arxiv.org/pdf/1605.02703) `[found]`
