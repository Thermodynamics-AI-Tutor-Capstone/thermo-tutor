# Property Data Tools

**Type:** concept / practice
**One line:** CoolProp, Cantera, and IAPWS-IF97 — the libraries that must supply
thermodynamic property values, because the model cannot be trusted to.
**Why we care:** This is the most concrete, most immediately buildable architectural decision
in the project, and the evidence for it is unusually direct.

## Why this layer is non-negotiable

[ThermoQA](thermoqa.md): every frontier model scores **44–63% on R-134a** property problems,
against 75–98% on water. Supercritical water drops to 45–90%. The authors' diagnosis is
exact: *"Models memorize discrete steam table entries... but cannot interpolate near the
critical point."*

That is a **memorization** failure, and memorization failures don't improve with better
prompting, more reasoning, or a bigger model. They're fixed by looking the value up.

[Khan Academy reached the same conclusion in math](../systems/khanmigo.md): generative AI
"generates a probable next number rather than executing a correct calculation," so they built
a separate math agent to verify every calculation.

**Rule: no thermodynamic property value reaches a student unless it came from a tool call.**
→ [grounding and verification](../concepts/grounding-and-verification.md)

## The libraries

**CoolProp** — thermophysical properties, Python bindings, wide fluid coverage including
refrigerants. The most likely primary choice. Also what [ThermoQA](thermoqa.md) uses for
ground truth, which is convenient: our tool layer and the benchmark's answer key would be the
same source.

**Cantera** — thermodynamics, kinetics, transport. Object-oriented, can generate saturated
steam tables and vapor domes. Heavier than we need for a tutor, and stronger where chemical
reactions matter.

**IAPWS-IF97** — the industrial standard formulation for water and steam. What the steam
tables in the textbook are ultimately derived from.

**Supporting:** SymPy (symbolic manipulation), Pint (units — and unit errors are a large
share of student errors, so a unit checker is a *pedagogical* tool, not just a correctness
one).

## The reference state trap — read this before writing any code

**Cantera, CoolProp, NIST, and the textbook tables do not agree on the reference state for
enthalpy and internal energy.**

Cantera uses the reaction-thermodynamics convention (zero enthalpy at 298.15 K, 1 atm).
CoolProp and NIST use different conventions. Cengel & Boles and Moran & Shapiro use their own.

Consequence: **every enthalpy and internal energy value will be offset by a constant relative
to the student's table.** Differences (Δh, Δu) are unaffected, so many problems come out
right — which is precisely what makes this dangerous. It will pass casual testing and then
produce confidently wrong absolute values on exactly the problems where absolute *h* matters.

**Actions:**
- Decide the reference convention explicitly and pin it in configuration
- Match the textbook the course actually uses
      → [ask the instructor](../../admin/canvas-access.md)
- Write a regression test comparing tool output against a table of known textbook values
  **before** building anything on top

This is the kind of bug that survives to a demo and embarrasses you in front of a faculty
panel. Handle it in week one.

## The design that follows

```
student question
   → LLM identifies what state is needed (substance, two independent properties)
   → tool call: CoolProp/IAPWS with pinned reference state
   → returns h, u, s, v, x, phase — with units
   → LLM reasons over returned values, never over recalled ones
   → verification: every number in the response traces to a tool result
   → response
```

Plus the [diagram inversion](diagram-reading.md): the same computed state renders the P-v or
T-s diagram, rather than asking a model to read one.

## Prior art

**ThermoState** ([github](https://github.com/Thermo-State/ThermoState)) — a CoolProp GUI for
power and refrigeration cycles and pure-substance state calculation. Useful precedent for how
to *present* state calculations to students, which is a UX problem we'd otherwise solve from
scratch.

**AwesomeThermodynamics** ([github](https://github.com/iurisegtovich/AwesomeThermodynamics))
— curated resource list, worth mining.

## Open questions

- [ ] Which textbook does the PSU course use? Determines the reference convention and table
      numbering. **Blocking for this work.**
- [ ] Does tool-calling actually fix the R-134a gap, or is the model's *reasoning* about
      refrigerants also wrong? **Testable directly against
      [ThermoQA](thermoqa.md) items — good early spike.**
- [ ] Latency: how slow is a CoolProp call inside a conversational turn?
- [ ] Should the tutor show the student the tool call? (Arguments both ways: transparency
      and modeling good practice, versus doing the lookup *for* them when looking it up is
      itself a skill being taught.)
- [ ] Does [Stan](../systems/stan-udel.md) do this? If not, it's a citable gap.

## Connects to

- [ThermoQA](thermoqa.md) — the evidence, and the same ground-truth source
- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis
- [grounding and verification](../concepts/grounding-and-verification.md) — the general principle
- [diagram reading](diagram-reading.md) — the render-don't-read inversion
- [Khanmigo](../systems/khanmigo.md) — the math-agent precedent

## Sources

- [CoolProp](https://sourceforge.net/projects/coolprop/) `[found]`
- [Cantera](https://cantera.org/) `[found]` — see the FAQ on reference-state differences
- [Development of a Portable Steam Table Application Integrating IAPWS-IF97 and CoolProp](https://e-journals.irapublishing.com/index.php/IRAJTMA/article/view/351) `[found]`
- [ThermoState](https://github.com/Thermo-State/ThermoState) `[found]`
- [AwesomeThermodynamics](https://github.com/iurisegtovich/AwesomeThermodynamics) `[found]`
