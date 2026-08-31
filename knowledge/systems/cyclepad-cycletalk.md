# CyclePad and CycleTalk — the articulate simulator

**Type:** system
**One line:** An "articulate virtual laboratory" for engineering thermodynamics — a simulator
that explains the derivation behind every value it computes — deployed at the US Naval Academy,
Northwestern and Oxford from 1996, with a dialogue-agent successor built at CMU.
**Why we care:** **This is the closest historical precedent for our project, and the modern
LLM-tutoring literature does not cite it.** Its architecture is, in outline, the one we
independently proposed. It is downloadable and still runs.

> **Status: `[read — software artifact]`, papers in progress.** The section below is original
> archaeology — we downloaded CyclePad v2.0 and read its shipped data files and help system
> directly. The paper-based sections are being read now and will be merged.

## What it is

**CyclePad** — Kenneth Forbus and the Qualitative Reasoning Group, Northwestern University.
*"The first articulate virtual laboratory the Qualitative Reasoning Group has implemented."*
NSF-funded; the Naval Academy collaboration was supported by the **Cognitive Science Division
of the Office of Naval Research** — the same programme that funded [Andes](andes.md), which is
how we found it.

Students **construct and analyse thermodynamic cycles**, and a hypertext explanation facility
gives *"access to the chain of reasoning underlying the derivation of each value."*

Field-tested in undergraduate engineering classes at **Northwestern, the U.S. Naval Academy, and
Oxford University.**

**CycleTalk** — Carolyn Rosé's group at CMU built a **tutorial dialogue agent on top of
CyclePad**, engaging students in *"dialogues negotiating the pros and cons of alternative
designs for thermodynamic cycles."* Preceded by **Wizard-of-Oz studies** and followed by a
controlled evaluation (ITS 2006).

---

## ⭐ Software archaeology — what we found by downloading it

**It is still available and intact.** `cyclepad_20010611.zip`, 3.26 MB, from
[qrg.northwestern.edu/software/cyclepad](https://www.qrg.northwestern.edu/software/cyclepad/cyclesof.htm).
45 files, 12.17 MB unpacked. Windows binary (`CPAD.EXE`) built on **Allegro Common Lisp** —
seven ACL image files totalling ~9 MB carry the compiled knowledge base. Dated **June 2001**;
the help file is dated 1998.

**This is a meaningful contrast with [Andes](andes.md), whose 356-problem library is
permanently lost.** CyclePad's domain content survived because it shipped inside the download.

### The cycle library — a machine-readable domain model, in plain text

`LIBRARY/` contains **16 `.DLB` files: eight cycle types, each in a bare and a "solved"
variant** — Rankine, Brayton, Otto, Diesel, Refrigeration, Regeneration, Reheat, and
Combined-cycle. Dated **February–September 1996**.

They are **plain-text Lisp s-expressions**, and the schema is exactly the structured
representation our architecture proposes:

```lisp
(CPAD::DESIGN :title "Rankine Cycle")
(CPAD::FLOW-TYPE :STEADY)
(CPAD::CYCLE-TYPE :HEAT-ENGINE)

(CPAD::DEVICE :type CPAD::TURBINE :symbol DATA::TUR1 :label "TUR1" ...)
(CPAD::DEVICE :type CPAD::PUMP    :symbol DATA::PMP1 :label "PMP1" ...)
(CPAD::DEVICE :type CPAD::HEATER  :symbol DATA::HTR1 :label "HTR1" ...)
(CPAD::DEVICE :type CPAD::COOLER  :symbol DATA::CLR1 :label "CLR1" ...)

(CPAD::STUFF :incpdev-name DATA::HTR1 :outcpdev-name DATA::TUR1
             :inport (:NORMAL :out DATA::HTR1) :outport (:NORMAL :in DATA::TUR1)
             :symbol DATA::S2 :label "S2")
```

**Devices are typed nodes; "stuff" is the working-fluid stream connecting them; states are
labelled S1…Sn on the edges.** A cycle is a typed, directed device graph.

And the *solved* variants add the piece that matters most to us — **modelling assumptions as
explicit, first-class, machine-readable assertions**:

```lisp
(CPAD::TEMPERATURE :C)                          ; unit declarations
(CPAD::PRESSURE :KPA)
(CL-USER::ISENTROPIC CL-USER::TUR1)             ; assumption, per device
(CL-USER::ISENTROPIC CL-USER::PMP1)
(CL-USER::SUBSTANCE-OF CL-USER::S2 CL-USER::WATER)   ; working fluid, per state
```

> **This is the single most important thing in this node.** *Assumption identification* is the
> capability [every LLM tested fails at](../domain/thermo-problem-benchmark.md) — every model in
> Loubet et al. assumed reversibility where the problem did not license it, in every repetition.
> **CyclePad's answer was to make assumptions explicit, named, per-device, retractable, and
> visually distinct — the student must *declare* `ISENTROPIC TUR1`, and can then be shown its
> consequences.** That is a structural solution to our hardest problem, and it is thirty years
> old.

### The parameter ontology, recovered from the help system

The complete parameter vocabulary, which maps almost directly onto what our
[property tools](../domain/property-data-tools.md) and
[skill graph](../../research/domain/skill-graph-draft.md) need:

`cp · cv · cop-r · Carnot cop-r · cop-hp · Carnot cop-hp · delta-H · delta-H-isentropic ·
delta-P · delta-spec-s · gamma · H · Hout-isentropic · mass-flow · max-T · min-T · molar-mass ·
net-Q · net-work · eta-isentropic · eta-thermal · P · PR · Psat · Q · Q-in · Q-out · R · S ·
shaft-work · spec-h · spec-hf · spec-hg · spec-q · spec-s · spec-sf · spec-sg ·
spec-shaft-work · spec-shaft-work-isentropic · spec-u · spec-v · T · Tout-isentropic · Tsat ·
U · V · work-in · work-out`

Knowledge-base sections: **components · processes · stuff · subcycles · modelling assumptions ·
parameters · substances · ideal gas law · thermodynamic properties.**

### Three modes: Build → Analyze → Contradiction

**Build** — pick components from a palette, drop them on the canvas, connect ports. Ports are
directional (black triangles show flow direction) and **the UI turns compatible ports green
while you drag a connection** — you cannot connect two outlets. Labels must be unique.

**Analyze** — click any icon to pop up a **meter** showing that entity's modelling assumptions
and parametric values. And the crucial detail:

> *"Initially everything in the meter is black, since the cycle's parameters are as yet
> unspecified, but as you make assumptions, you will find that the meter displays them in
> [colour]… **Note that water is in green, to indicate it is an assumption that we have
> made.**"*

**Colour encodes epistemic status.** Black = unknown, green = you assumed it, derived values
shown separately. **The student can always see, at a glance, what they assumed versus what
follows from it.** That is a beautifully cheap solution to a problem our tutor will also have.

Assumptions are made by clicking a meter's first line, which initially reads
*"Unknown assumptions re &lt;component&gt;."* And the interaction is deliberately unordered:
*"You can make assumptions and ask questions in any order you like."*

**Contradiction** — a first-class mode, and the most interesting one.

### ⭐ Contradiction Mode

> *"As you assume parameter values, you are in effect constraining the values that the other
> parameters can take on. You may inadvertently **overconstrain** the value of a parameter, in
> which case it can either not have a value at all, or CyclePad finds that it is calculating two
> or more different values for that parameter."*

> *"When these or other **simple physical intuitions are violated**, CyclePad switches to
> contradiction mode. In this mode, the report window shows you the particular intuitions that
> were violated **and the list of assumptions which caused the contradiction**."*

> *"CyclePad **will not let you proceed** until you clear the assumption."*

Three things worth stealing outright:

1. **It blocks.** You cannot continue analysing an impossible design. Compare an LLM tutor,
   which will happily reason onward from a thermodynamically impossible premise.
2. **It names the culprits** — not "something is wrong" but *the specific set of assumptions
   implicated*, which the student must then choose among.
3. **It teaches a debugging strategy**, explicitly and metacognitively:

   > *"You may find it helpful to **work backwards, asking why the contradictory facts were
   > believed** and working back to the assumptions. Or you may find it helpful to **work
   > forward from your assumptions**, moving through their consequences to see where things went
   > astray. Often a combination of working forwards and backwards provides the best results."*

   That is principle-level, metacognitive guidance with no answer given — precisely the kind of
   support the [productive-failure literature](../concepts/productive-failure.md) says works,
   as opposed to the step-level hinting that fails.

**Engineering reality is enforced too.** Devices have materials — carbon steel, stainless,
nickel-alloy, aluminium, titanium, molybdenum, and (a joke with a purpose) **unobtainium**,
*"very expensive, but it can withstand extremely high temperatures."* Each real material has a
maximum temperature, and **exceeding it raises a contradiction.** Students cannot design a
Rankine cycle at 3000 K and call it efficient.

### The explanation system — its actual question types

Recovered from the help file, the system answers a **fixed taxonomy of questions**:

- **"How could I compute &lt;X&gt;?"**
- **"What equations mention &lt;X&gt;?"**
- **"What follows from &lt;X&gt;?"**
- **"What phase can't &lt;X&gt; be?"**

Plus a **query history** — *"A record of your queries appears in the gray box at the top of this
window. You can go back to any question you have asked."*

**This is a bounded, answerable question set over a dependency structure** — not free-form
natural language. That is the trade CyclePad made: no conversation, but every answer is
guaranteed correct and traceable. **An LLM inverts the trade.** The interesting design space is
whether we can have both — which is what CycleTalk attempted.

### The coaching facility — role inference

> *"CyclePad incorporates a coaching facility… To provide this help, CyclePad first makes
> inferences about **the role that each device is playing**. A role is defined as the function
> that a particular device is intended to perform. For example, some gas liquefaction plants use
> turbines rather than throttles to expand the working fluid because a resisted expansion
> produces a larger drop in temperature… **the intended function of the turbine is to cool the
> working fluid, not to produce power.**"*

**Design-intent recognition** — inferring *why* a component is there, not just what it is. That
is a genuinely sophisticated idea and it is the thing an LLM should be *good* at, where the
1990s system had to infer it from rules.

*(Caveat: an "email coach" feature is documented as largely aspirational — *"many of the
functions are currently under development."* Note the gap between documented and shipped.)*

### Also shipped: a sensitivity-analysis tool, an economic model, and an instructor mode

The economic model prices devices by a **cost-basis parameter and a size exponent**
(*"a $50,000 pump might require 100kW of input shaft-power"*), plus fuel cost from the heater's
steady-state heat flow and a utilisation rate. There is an **Instructor menu** in the command
reference — an instructor-facing mode we should look at.

---

## Why this matters to our project

**1. It is the architecture we independently arrived at.** Compute state properly, keep it as
structured data, and reason/explain over the structure rather than over prose or images. Forbus
did it with qualitative reasoning and a rule base; we would do it with
[CoolProp/Cantera tool calls](../domain/property-data-tools.md). **The vocabulary — "articulate"
— is worth adopting**, because it names the property precisely: a simulator that can explain
the derivation of every value.

**2. It solves our hardest problem structurally.** Assumptions as explicit, retractable,
colour-coded, per-device declarations directly attacks the
[unstated-assumption failure](../domain/llm-thermodynamics-capability.md) that defeats every
LLM in our domain.

**3. Contradiction detection is the verification layer we've been describing.** And it does
something our [NLI-based verification](../concepts/grounding-and-verification.md) explicitly
*cannot*: catch a physically impossible state, name the assumptions responsible, and refuse to
proceed.

**4. Its coverage is our hardest tier.** Rankine, Brayton, Otto, Diesel, refrigeration,
regeneration, reheat, combined-cycle — precisely
[ThermoQA's Tier 3](../domain/thermoqa.md), where frontier models drop to 52.7%.

**5. The gap it leaves is exactly LLM-shaped.** CyclePad answers four fixed question types over
a dependency graph. It cannot handle *"I don't get why the pump work is so small"* — which is
what students actually ask. **CycleTalk was the attempt to close that gap in 2004–2006, and we
should know what it found before proposing the same thing with better language technology.**

## Open questions — being read now

- [ ] The 1999 *Artificial Intelligence* paper: architecture, the reasoning engine, how
      qualitative reasoning and numerical property data interact, authoring cost
- [ ] **Any learning-outcome data from USNA, Northwestern or Oxford.** If it exists it is the
      only long-run evidence for thermodynamics tutoring anywhere. If it doesn't, that is a
      finding.
- [ ] CycleTalk's controlled evaluation (ITS 2006) — did dialogue beat unguided exploration?
- [ ] The Wizard-of-Oz studies, and how human transcripts were turned into dialogue design
- [ ] The goal-orientation × tutoring-style study
- [ ] Does anyone in the modern LLM-tutoring literature cite this work?
- [ ] Can we run CyclePad? (Windows binary; needs a VM or Wine.) Worth doing — an hour with the
      actual tool is worth several papers.

## Connects to

- [Andes](andes.md) — sibling ONR project; the passage that surfaced this
- [property data tools](../domain/property-data-tools.md) — the modern articulate-simulator layer
- [thermo problem benchmark](../domain/thermo-problem-benchmark.md) — the assumption failure this addresses
- [grounding and verification](../concepts/grounding-and-verification.md) — contradiction detection as verification
- [ThermoQA](../domain/thermoqa.md) — same cycle coverage, hardest tier
- [productive failure](../concepts/productive-failure.md) — the metacognitive debugging guidance
- [Stan](stan-udel.md) — the 2026 thermodynamics assistant that doesn't cite this

## Sources

- **CyclePad v2.0 software** — [download](https://www.qrg.northwestern.edu/software/cyclepad/cyclesof.htm) `[read — artifact downloaded, library and help system analysed 2026-08-31]`. Local copy in the session scratchpad.
- [CyclePad help system](https://www.qrg.northwestern.edu/software/cyclepad/help/CyclePad_Help.html) `[read]`
- [QRG CyclePad project page](https://www.qrg.northwestern.edu/projects/NSF/Cyclepad/cyclepad.htm) `[read]`
- Forbus, Whalley, Everett, Ureel, Brokowski, Baher & Kuehne (1999). "CyclePad: An articulate virtual laboratory for engineering thermodynamics." *Artificial Intelligence* **114(1–2), 297–347.** `[in progress]`
- "Using Articulate Virtual Laboratories in Teaching Energy Conversion at the U.S. Naval Academy," *J. Educational Technology Systems* (1998), ERIC EJ561409 `[in progress]`
- Rosé et al. "CycleTalk: Toward a Dialogue Agent That Guides Design with an Articulate Simulator," ITS 2004 `[in progress]`
- "Evaluating the Effectiveness of Tutorial Dialogue Instruction in an Exploratory Learning Context," ITS 2006 `[in progress]`
