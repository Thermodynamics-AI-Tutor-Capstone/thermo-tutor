# Property Data Tools

**Type:** concept / practice
**One line:** CoolProp, Cantera, and IAPWS-IF97 — the libraries that must supply
thermodynamic property values, because the model cannot be trusted to.
**Why we care:** This is the most concrete, most immediately buildable architectural decision
in the project, and the evidence for it is unusually direct.

## ⭐ The transcoding principle — the strongest single design finding in our source set

Three research teams independently converged on the same answer to "how do you make a
non-embeddable engineering artifact usable by an LLM," without citing each other. **Do not
caption it, do not OCR it, do not send it to a vision model. Transcode it into its native,
complete, machine-readable text representation and index that.**

| Team | Artifact | Their solution |
|---|---|---|
| **UC Davis (ASEE 2025)** | Circuit schematics | **SPICE netlists** |
| **Stan (U. Delaware)** | Textbook content | The book's own **back-of-book index as structured JSON** |
| **CodeAid (Toronto, CHI 2024)** | C standard library | **Scraped documentation parsed into a JSON key-value store** |

**The evidence that forced it — and this is our exact problem in a different domain.** UC Davis
tested an AI TA on junior-level Microelectronic Circuits with Claude 3.5 Sonnet. On homework
whose answers are formula-based: **accuracy 5.0/5**. On homework whose answer lives *in a
figure*: **accuracy 1.6/5**. Same model, same course, same textbook. The only variable is that
the information was in a schematic.

Their three catalogued failure modes translate directly:

1. The model states it cannot view the figure
2. It "sees wrong component values or names in a figure"
3. It "answers the questions for a different circuit than the one in the figure"

The verified case is the one to internalize: given a common-source amplifier with a cascoded
load, the tutor *"answered as if the circuit was a cascode transistor M2 above common-source
M1 — **apparently it read the figure caption and then found information about a different but
similarly named circuit**."*

**The steam-table analogue is exact.** A model retrieves *"Table A-4: Saturated water —
temperature table"* **by its caption**, then generates plausible values it never read. That is
the single most dangerous failure available to a thermodynamics tutor, because every number
will look right.

**Their fix worked:** *"we wrote a SPICE netlist for this amplifier… A SPICE netlist is a
complete description of a circuit, using only text. After feeding the SPICE netlist into a
newly released LLM, it understood the circuit and its elements, and it correctly answered
questions about the circuit."* Their conclusion: *"providing the AI TA with a SPICE netlist
for each schematic is a good and effective option. However, generating a SPICE netlist for
every schematic in a circuits textbook would be a big job."*

**What this means concretely for us:**

- **Do not embed steam tables.** Transcode them into structured records — substance, table id,
  state variables, every property column, units, source page — and serve them through a
  **deterministic property-lookup tool the model calls**, with interpolation done **in code**.
- That is cheaper for us than for them: CoolProp already *is* the transcoded form. We don't
  have to hand-author netlists; we have to pin the reference state and wrap the library.
- **Reserve vector retrieval for prose**: lecture notes, worked-example narratives, sign
  conventions, definitions.
- **⚠ The corollary is uncomfortable.** A P–v or T–s *diagram* has **no lossless text form** the
  way a circuit or a table does. Expect diagrams to behave like Ethel's process diagrams —
  *"substantially less reliable than grading mathematical derivations"* — rather than like
  tables. Transcoding solves the table problem and does **not** solve the diagram problem.
  → [diagram reading](diagram-reading.md)

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

And a second rule that follows from the verification literature: **a grounding checker cannot
catch a wrong property value.** NLI-based verification demonstrably fails on claims involving
temporal reference, negation, and quantifiers — and a numeric table lookup is structurally
that same class of claim. Asking an entailment model whether a table entails
*"h_f = 191.83 kJ/kg at 45 °C"* is asking it to perform lookup and arithmetic, which is what
it cannot do. **Property values need a deterministic value-checker, not entailment.**
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

⭐ **And a second, subtler trap that CyclePad hit and solved — numerical noise is a *trust* bug.**
CyclePad deliberately **suppressed logically valid inference paths through its property tables**,
preferring analytic propagation, for two reasons: accumulated interpolation error triggered false
contradictions, and —

> *"the results of constraint propagation **look more like the work a student would do**, and thus
> the explanations provided are a better model for the student… CyclePad may display 6.60 kJ/kg at
> the inlet and 6.60001 kJ/kg at the outlet… **We found that if CyclePad did not do the "obvious"
> propagation in preference to interpolation, students trusted it less.**"*

CoolProp will happily hand us more precision than the student's tables carry, and more paths to a
value than the textbook would take. **Round to the table's precision, and follow the route the
course teaches even when a shortcut exists.** → [CyclePad](../systems/cyclepad-cycletalk.md)

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
