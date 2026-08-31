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

## ⭐ What to use instead — and there is a well-documented answer

> **Resolved 2026-08-31.** A full read of the AAPT Resource Letter and the PhysPort entries
> settles this. Note first that **Resource Letter RBAI-1 will not help**: it states explicitly
> that *"The Thermal and Transport Concept Inventory-Thermodynamics (TTCI-T) and the
> Thermodynamics Concept Inventory (TCI) were developed specifically for engineering courses,
> and **will not be discussed further here**,"* and it reports **no reliability or validity
> coefficients for any thermodynamics instrument.** Do not cite it for psychometrics.

### First choice: STPFaSL

**Survey of Thermodynamic Processes and First and Second Laws** — Brundage & Singh, University
of Pittsburgh. *Phys. Rev. Phys. Educ. Res.* 19, 020112; arXiv:2402.07906.

| | |
|---|---|
| Items | **78** multiple choice, across 19 shared contexts |
| Categories | Processes · Systems · Quantities & Relations · **Representation** · First Law · Second Law |
| Validation | **PhysPort Silver** (second-highest tier) |
| Population | Introductory college **through upper-level/graduate** |
| Access | Freely available via arXiv and PhysPort |

**Published reliability (KR-20), which is what the TCI lacks entirely:**

| Group | In person | Online |
|---|---|---|
| Upper-level / PhD (N=89 / 179) | **0.90** | **0.92** |
| Intro calculus-based (N=251 / 376) | **0.80** | **0.94** |

Three reasons it is the right pick for us:

1. **It has P–V diagram items by design.** *"The Representation category includes items in
   which a process is represented on a PV diagram."* Given that
   [diagram reasoning is our central technical risk](../domain/diagram-reading.md), an
   instrument that measures it separately is worth a great deal.
2. **It will not ceiling.** Upper-level and PhD students score only **76%**; introductory
   students move 52% → 58% pre/post. Compare [Kestin](../evidence/kestin-2025-rct.md), who
   needed quantile regression to work around ceiling effects.
3. Validated across **12 in-person classes at 4 institutions and 12 online classes at 5
   institutions**, with item difficulty, point-biserial coefficients, KR-20, expert content
   validity, and concurrent validity all reported. Item-level difficulty and distractor
   prevalence are in the appendices — **which makes it a ready-made misconception source too.**

A shorter validated version (**STPFaSL-Short**) shares all 19 contexts verbatim.

### Second choice / complement: TTCI-T

**Thermal and Transport Concept Inventory: Thermodynamics** — Miller, Streveler & Geist.
PhysPort **Silver**; administered to **>1,000 students at >10 universities**, with 12
publications reporting data. Built from a three-round Delphi study of expert engineering
faculty plus student interviews. Covers second law, energy quality, thermal-to-work
conversion, enthalpy, internal energy, and **equilibrium vs. steady state**.

Caveat: PhysPort says only that *"statistical analyses of reliability, difficulty and
discrimination found the TTCI to have acceptable values"* — **it does not publish the
coefficients.** The nearest published figure is for the *heat transfer* sibling: 12 items,
**KR-20 = 0.77**, item difficulty 0.25–0.75, discrimination > 0.20 on every item.

**Access:** email **Dr. Ron Miller, `rlmiller@mines.edu`**, with a description of the course.

### Also worth knowing

**TCS (Thermodynamic Conceptual Survey)** — Wattanakasiwich et al. (2013). Physics rather than
engineering, but per RBAI-1 *"the only thermodynamics test that asks students to interpret
P vs. V graphs"* among the physics instruments, and the only one covering the first law.

**Recommendation: STPFaSL as primary, TTCI-T as the engineering-specific complement if Miller
grants access.** Use STPFaSL's Representation subscale as a dedicated diagram-competence
measure.

## Access — start early

PhysPort gates instruments behind **educator verification**. Students can't download them;
test security is the point. Our instructor sponsor is the path.
→ [Canvas access questions](../../admin/canvas-access.md)

**This is slow. Request it in Phase 0.** → [roadmap](../../admin/roadmap.md)

## ⭐ Why this decision outranks the tutor itself

Two independent findings say the outcome measure will drive our reported effect more than the
system will:

- **Kulik & Fletcher (50 ITS evaluations): 0.73 on locally-developed tests vs 0.13 on
  standardized ones.** Same systems.
- **Steenbergen-Hu & Cooper: 0.90 against no treatment, 0.37 against a classroom, −0.25 against
  a human tutor.** Same systems.
- And [Andes](../systems/andes.md), within the same students on the same exams: **+1.21 on
  drawings, +0.69 on variable definitions, −0.08 on final answers.**

**Decide the comparison condition and the outcome measure first, then build.** And note what
Andes implies specifically: **a step-based tutor's effect does not show up in answer-only
scores.** If we measure only whether students got the right number, we should expect zero — which
makes STPFaSL's **Representation** subscale (process, P–V diagrams) more important than its
total.

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
| **STPFaSL normalized gain** | **Published KR-20 0.80–0.94**; PhysPort Silver; has a PV-diagram subscale; freely available; won't ceiling | 78 items is a long sitting; measures concepts, not problem-solving |
| TTCI-T normalized gain | Engineering-specific, Silver, >1,000 students | Coefficients unpublished; access gated behind an email to the developer |
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
- [x] ~~Which instrument?~~ **STPFaSL** primary (arXiv:2402.07906, freely available), TTCI-T
      as complement. TCI is off the table.
- [ ] Email **Ron Miller (`rlmiller@mines.edu`)** for TTCI-T access, with a course description.
- [ ] Decide whether 78 items is administrable in our setting, or whether STPFaSL-Short fits
      better.
- [ ] **Mine STPFaSL's appendices for distractor-prevalence data** — it doubles as a validated
      misconception source for
      [our catalogue](../../research/domain/skill-graph-draft.md).
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
- [Brundage & Singh, "Survey of Thermodynamic Processes and First and Second Laws," *PRPER* 19, 020112 / arXiv:2402.07906](https://arxiv.org/abs/2402.07906) `[read]` — **the recommended instrument**; KR-20 tables, Representation/PV-diagram category, appendices with item difficulty and distractor prevalence
- [PhysPort — TTCI-T](https://www.physport.org/assessments/assessment.cfm?A=TTCIT) `[read]` — Silver validation; contact Ron Miller
- [Madsen, McKagan & Sayre, Resource Letter RBAI-1, arXiv:1605.02703](https://arxiv.org/abs/1605.02703) `[read]` — **explicitly excludes the engineering instruments and publishes no thermodynamics psychometrics.** Cite only for the qualitative TCS/TCE/HTCE comparison.
- Streveler, Miller, Santiago-Román, Nelson, Geist & Olds, *Int. J. Eng. Educ.* 27(5), 968–984 (2011) — TTCI `[found]`
- Midkiff, Litzinger & Evans, 31st ASEE/IEEE FIE, F2A-3 (2001) — the TCI origin `[found]`
