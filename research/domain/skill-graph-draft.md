# Thermodynamics Knowledge Model — First Draft

**Status: unreviewed strawman.** Written from the standard undergraduate engineering
thermodynamics sequence (Cengel & Boles; Moran & Shapiro). It has **not** been checked
against the actual PSU course, and it is not authoritative until the instructor sponsor
has red-penned it.

## Why this exists in a research repo

It's domain analysis, not code. Three things depend on it:

1. Question C2 — what is the right *grain* for a concept? You can't answer that without a
   candidate list to argue about.
2. Any mastery tracking needs a unit of mastery. This is the candidate unit.
3. It's the artifact nobody else can produce for us. Papers and products give us
   architecture; only a domain expert plus this course gives us the map.

## The grain problem

- `entropy` — too coarse. A student can be fluent with the ideal-gas entropy relations
  and completely lost on entropy generation in an open system. One number hides that.
- `interpolating linearly between two rows of Table A-6` — too fine. Thousands of items,
  and a semester never produces enough observations per item to estimate anything.

Working target: **~80–120 knowledge components**, each one something an instructor would
recognize as a distinct thing a student can independently get or not get, and each one
observable in at least a handful of problems per semester.

## ⭐⭐ Next action on this file: tag every component on KLI's four axes

**This draft currently has no theoretical grounding, and
[the framework that should supply it](../../knowledge/concepts/kli-framework.md) is now read in
full.** Koedinger, Corbett & Perfetti define a knowledge component as a `condition → response`
pair and classify it on four axes. **Adding four columns to the lists below is an afternoon of
work, needs no data, and converts this list into a decision table the tutor can act on:**

| Column | Values | What it decides |
|---|---|---|
| `conditions` | constant / variable | variable conditions must be **induced**, and mis-induction *is* the misconception |
| `response` | constant / variable | |
| `verbal` | yes / no | ⚠ **doing and explaining are different components.** A student can find the right angle and not say why |
| ⭐ `rationale` | **reason / convention** | **Socratic dialogue and self-explanation are only worth spending time on where there is a rationale.** `T_sat` at 2 MPa is a convention; the second law is not |

**Then the tutor's policy reads off KLI's Table 4:**

- **Constant-constant** (property-table lookups, unit conversions, definitions) → **spacing,
  retrieval practice, timely feedback. No dialogue — there is nothing to explain.**
- **Variable-condition rules** (`model-selection`, `assumption-identification`) → **feature
  focusing and worked examples.** Explanation is *less* efficient here than induction.
- **Principles with rationales** (the laws, and when they apply) → **self-explanation and
  argumentation**, and prompt for the **justification** ("what principle licenses this step?")
  rather than metacognitively.

⭐ **Two empirical checks on the grain**, once there is any data:
**word-count each component's `if…then…` description** (6–9 words ≈ fact, 10–12 ≈ rule, 12–21 ≈
schema), and **compare median correct-execution latency** (3–6 s / 6–10 s / 10–14 s by type).
Components designed as peers whose latencies sit two tiers apart are wrongly grouped.

⭐ **And hunt for hidden *integrative* components** — ones invisible in any single task — with
`P(integrative) = P(hard task) ÷ P(easy task)` on paired problems. The cross-cutting skills below
are exactly that shape.

Sanity check nobody has run yet: how many graded interactions does one student actually
produce in a semester? If it's ~300, then 100 KCs means ~3 observations each, which is
not enough for BKT to say anything. **This calculation may force the grain coarser.**
Someone should run it (question C2).

---

## Draft units and knowledge components

Prerequisite edges are noted as `← depends on`. Only non-obvious edges are marked; within
a unit, order implies dependency.

### U1 — Concepts and definitions
- `system-boundary-selection` — closed vs. open vs. isolated; **choosing** the boundary
- `property-state-process-cycle`
- `intensive-vs-extensive`
- `equilibrium-quasi-static`
- `pressure-absolute-vs-gauge`
- `temperature-scales-zeroth-law`
- `unit-systems-conversion` *(cross-cutting; failure here masks every other skill)*

### U2 — Properties of pure substances
- `phase-diagrams-pv-tv-pt`
- `saturation-quality` — quality *x*, saturated mixtures ← `phase-diagrams-pv-tv-pt`
- `property-table-lookup` — finding the right table, reading it
- `table-interpolation` ← `property-table-lookup`
- `compressed-liquid-approximation`
- `ideal-gas-equation-of-state`
- `ideal-gas-validity-judgment` — **when is the assumption licensed?**
- `compressibility-factor`

### U3 — First law, closed systems
- `energy-forms-internal-kinetic-potential`
- `heat-vs-work-distinction` *(major misconception site)*
- `sign-conventions`
- `boundary-work-pdv` ← `phase-diagrams-pv-tv-pt`
- `first-law-closed-system` ← `energy-forms-internal-kinetic-potential`, `sign-conventions`
- `specific-heats-cv-cp`
- `du-dh-ideal-gas` ← `specific-heats-cv-cp`, `ideal-gas-equation-of-state`
- `incompressible-substance-model`
- `polytropic-processes`

### U4 — Control volumes
- `conservation-of-mass-steady-flow`
- `flow-work-and-enthalpy` — why *h* and not *u* ← `first-law-closed-system`
- `steady-flow-energy-balance` ← `flow-work-and-enthalpy`
- `device-nozzle-diffuser`
- `device-turbine`
- `device-compressor-pump`
- `device-throttle` — isenthalpic
- `device-heat-exchanger`
- `device-mixing-chamber`
- `transient-charging-discharging` ← `steady-flow-energy-balance`

### U5 — Second law
- `thermal-reservoirs`
- `heat-engine-thermal-efficiency`
- `refrigerator-heat-pump-cop`
- `kelvin-planck-clausius-statements`
- `reversible-vs-irreversible` *(the assumption the models all get wrong — see key
  finding #2)*
- `carnot-cycle`
- `carnot-efficiency-limits` ← `carnot-cycle`, `heat-engine-thermal-efficiency`

### U6 — Entropy
- `clausius-inequality`
- `entropy-definition`
- `increase-of-entropy-principle` ← `entropy-definition`
- `entropy-change-pure-substance` ← `property-table-lookup`
- `entropy-change-ideal-gas` — constant and variable specific heats
- `entropy-change-incompressible`
- `isentropic-process` ← `entropy-change-ideal-gas`
- `tds-relations`
- `reversible-steady-flow-work`
- `isentropic-efficiency-turbine` ← `isentropic-process`, `device-turbine`
- `isentropic-efficiency-compressor` ← `isentropic-process`, `device-compressor-pump`
- `isentropic-efficiency-nozzle` ← `isentropic-process`, `device-nozzle-diffuser`
- `entropy-balance-generation` ← `increase-of-entropy-principle`

### U7 — Exergy *(confirm whether in scope for the PSU course)*
- `exergy-fixed-mass`
- `exergy-flow-stream`
- `reversible-work-irreversibility`
- `second-law-efficiency`

### U8 — Cycles
- `rankine-cycle-ideal` ← `steady-flow-energy-balance`, `isentropic-efficiency-turbine`
- `rankine-reheat`
- `rankine-regeneration`
- `brayton-cycle`
- `otto-cycle`
- `diesel-cycle`
- `vapor-compression-refrigeration` ← `device-throttle`, `refrigerator-heat-pump-cop`

### X — Cross-cutting skills (the ones that actually predict success)

These aren't chapters, and standard courses rarely assess them directly. They may matter
more than anything above.

- `assumption-identification` — **what is and isn't licensed by this problem statement.**
  The single skill every LLM in arXiv:2502.05195 failed. Plausibly the highest-value
  thing a tutor could teach, and a genuine differentiator.
- `model-selection` — ideal gas vs. tables vs. incompressible
- `sanity-checking` — order of magnitude, sign, does this violate the second law
- `problem-decomposition` — what's known, what's asked, what connects them
- `diagram-drawing` — sketching the process on P-v or T-s

---

## Known misconceptions to catalogue

Separate file eventually. Seeds, from the physics/engineering education literature and
from teaching experience — **needs a real literature search** (see bibliography "to
find"):

- Heat and temperature conflated; "heat" treated as a substance contained in a body
- Work or heat treated as a property of a state rather than a path quantity
- "Entropy is disorder" as a working definition, which then fails on every calculation
- Sign convention confusion, particularly *W* for compressors vs. turbines
- Assuming any adiabatic process is isentropic ← *this is the LLM failure too*
- Treating efficiency and COP as the same kind of quantity
- Believing the second law forbids any local entropy decrease

The misconception catalogue may be more useful than the skill graph. Mastery tracking
tells you *that* a student is struggling; a misconception tells you *what to say*.

---

## Open items

- [ ] Instructor review of the whole list — is this the actual course?
- [ ] Is exergy (U7) in scope?
- [ ] Which textbook does the course use? Determines notation and table numbering.
- [ ] Run the observations-per-KC calculation (question C2)
- [ ] Map the KCs to actual assignment problems for one semester — the real test of
      whether the grain is right
- [ ] Literature search on thermo misconceptions
