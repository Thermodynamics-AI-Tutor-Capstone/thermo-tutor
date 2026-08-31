# CyclePad and CycleTalk — the articulate simulator

**Type:** system
**One line:** An "articulate virtual laboratory" for engineering thermodynamics — a simulator
that explains the derivation behind every value it computes — deployed at the US Naval Academy,
Northwestern and Oxford from 1996, with a dialogue-agent successor built at CMU.
**Why we care:** **This is the closest historical precedent for our project, and the modern
LLM-tutoring literature does not cite it.** Its architecture is, in outline, the one we
independently proposed. It is downloadable and still runs.

> **Status: `[read]` — the 1999 *Artificial Intelligence* paper (all 51 pp.) **and** the shipped
> software artifact. CycleTalk and the classroom evaluations are still being read.

## What it is

**CyclePad** — Kenneth Forbus and the Qualitative Reasoning Group, Northwestern University.
*"The first articulate virtual laboratory the Qualitative Reasoning Group has implemented."*
NSF-funded; the Naval Academy collaboration was supported by the **Cognitive Science Division
of the Office of Naval Research** — the same programme that funded [Andes](andes.md), which is
how we found it.

Students **construct and analyse thermodynamic cycles**, and a hypertext explanation facility
gives *"access to the chain of reasoning underlying the derivation of each value."*

Field-tested in undergraduate engineering classes at **Northwestern, the U.S. Naval Academy, and
Oxford University** — *"Starting in **1995**, collaborators at Northwestern University and the US
Naval Academy started using it with their students on an experimental basis."* Web distribution
began September 1997.

**Scale of the knowledge base**, stated exactly: *"52 conceptual entities, 6 physical processes,
38 assumption classes, 195 equations, 184 pattern-directed rules and 156 background facts about
thermodynamics."* Plus 107 evidential rules for role inference, 18 norms, and 13 design cases.
Seven working fluids (water, nitrogen, ammonia, methane, R-12, R-22, R-134a). Built over
**six years**, bulk in the first four, by mechanical-engineering *and* AI faculty and students
jointly.

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

## The architecture, from the paper

Seven modules over a common substrate. The substrate is **LTRE — a logic-based truth
maintenance system coupled to a forward-chaining rule engine** (Forbus & de Kleer,
*Building Problem Solvers*), which *"serves as a blackboard, storing a design and the results of
analyzing it."*

Why an LTMS rather than the more common alternatives is a real design decision, and the
reasoning transfers: a JTMS was ruled out because *"Horn clauses are too clumsy… including
biconditionals (used in definitional consequences of modeling assumptions, e.g., a compressor is
operating isentropically exactly when its isentropic efficiency is 1.0)"*; an ATMS was ruled out
because rapid context-switching *"was not required."*

**Numbers come from constraint propagation, not from qualitative reasoning.** Each equation is
compiled into constraint rules with four slots — **Equation, Sets** (the parameter it derives),
**Uses** (parameters that must be known), and **Test** (a guard *"used to avoid numerical errors,
e.g., division by zero"*).

And then this, which is the whole hint mechanism in one sentence:

> *"Constraint rules are used in two ways. First, they are used for antecedent reasoning…
> Second, **they are used to generate advice about what a student might want to assume in order
> to derive a desired value.**"*

**Forward explanation and next-step hinting are the same data structure, run in two
directions.** That is trivially replicable and we should replicate it.

### ⭐ The interpolation decision — a trust finding, not a precision finding

Property lookup is woven into the propagator as pattern-directed rules. But they **deliberately
suppress logically valid inference paths through the tables**, and the reason is not what you'd
expect:

> *"CyclePad propagates all possible values, so it could in principle redundantly compute, say,
> the pressure, from the specific enthalpy and the temperature… it is quite possible that the
> newly estimated pressure value will be slightly different (given the accumulated inaccuracies
> in the interpolation process), **triggering a contradiction**."*

> *"**Second, the results of constraint propagation look more like the work a student would do,
> and thus the explanations provided are a better model for the student.** … CyclePad may display
> 6.60 kJ/kg at the inlet and 6.60001 kJ/kg at the outlet, for instance. **We found that if
> CyclePad did not do the "obvious" propagation in preference to interpolation, students trusted
> it less.**"*

Table lookup is deliberately **last** in the propagation queue, so analytic solution is always
preferred.

**Two lessons for us.** First, a tutor's derivation should follow **the route the textbook would
take**, even when a shortcut exists — the chain is pedagogical output, not just a means to an
answer. Second, **numerical noise in a tutor is a trust bug, not a precision bug.** A student who
sees 6.60 and 6.60001 for the same quantity stops believing the tool. Directly relevant to our
[property-tools layer](../domain/property-data-tools.md), where CoolProp will happily give us
more precision than the student's tables.

### What qualitative reasoning is actually for — and what it isn't

Narrow and precise: QR **does not compute values**. It supplies sign and ordinal constraints
that **detect physical impossibility**, via processes reified as first-class entities inside
components:

```lisp
(defProcessEpisode (heat-flow ?src-start ?src-end ?dst-start ?dst-end)
  (> (T ?src-start) (T ?dst-start))        ; the second law, as an ordinal constraint
  ...)
(defProcessEpisode (compression ?in ?out ?worker)
  (> (P ?out) (P ?in))
  (< (spec-shaft-work ?worker) 0))          ; compression eats work
```

A pump that produces work violates a constraint. Heat flowing cold-to-hot violates a constraint.
**The second law is encoded as an ordinal relation on a process episode** — and the same
definition of `compression` serves pumps and compressors, the same `heat-flow` serves heaters,
coolers and heat exchangers.

Two of the authors' own "surprises" are worth quoting because they save us effort:

> *"**Automatic model formulation, the primary focus of most research on compositional modeling,
> is irrelevant for this task.** What is important… is the ability to explicitly state and reason
> about modeling assumptions—something we want to educate the user in doing."*

> *"**Qualitative simulation was irrelevant for this task.** Qualitative reasoning about
> constraints imposed by physical processes, on the other hand, proved to be a crucial source of
> knowledge for detecting physically impossible choices for parameters."*

---

## ⭐⭐ Structured explanation systems — the most transferable idea in the paper

> *"Explanations are the heart of articulate software. An innovation developed for CyclePad is
> the idea of **structured explanation systems, an abstract layer between the reasoning system
> and interface that mediates explanation generation.**"*

Their statement of the problem is exactly ours:

> *"**Reasoning systems** need to be optimized for efficient inference… minimizing information
> about antecedents in a dependency system to the bare minimum needed for correct operation.
> **Interfaces** need to be optimized for communication with the user… including background
> information that isn't needed by the reasoning system. Obviously these constraints are in
> conflict."*

Two mediation techniques: **suppression** (hide implementation detail) and **reintroduction**
(add explicit items *not* in the dependency network that a human needs to understand the result).

**The representation is two-level.** The persistent record is the **LTMS dependency network**,
built automatically as values propagate — every value's justification records the equation *or
property table* used and the antecedent values relied on, so that *"the user [can] **trace the
derivation of any calculated value in the system back to user assumptions**."*

On top sit **e-propositions** and **e-arguments** — **16 types each** — which are **typed** and,
critically, **transient**: *"unlike TMS structures, e-propositions and e-arguments… **do not
persist over time**."* They are a "dynamically generated rational reconstruction" of the
dependency network, produced on demand.

Every e-proposition type implements two generic methods:

- **`QuestionsFor(proposition, design)`** — returns the questions that make sense *right now*,
  each with English text and a category symbol. Because the design is passed in, the list can
  include **commands**, e.g. assume or retract a value.
- **`FindAnswer(proposition, question, design)`** — builds the e-argument, choosing type by how
  the value was actually derived: `numerical-value-via-equation`, `-via-table`, or
  `-via-propagation`.

**And note four of the sixteen argument types:** `numerical-value-needs-via-equation`,
`numerical-value-needs-via-table`, `numerical-value-system-heat-flow-needs`,
`numerical-value-table-needs-prerequisites`. These answer **"what would I need to know in order
to derive this?"** — the same machinery, pointed forward. Explanation and hint, one mechanism.

### "Can't say, don't tell" — a guardrail we should copy verbatim

> *"Given any proposition in the database, CyclePad can determine whether or not that proposition
> **can be stated in English** for the user. Any antecedent that cannot be so articulated is not
> included in the antecedents for the argument. When appropriate, the antecedents for the silent
> antecedent are themselves **promoted** for potential inclusion… **This recursive process
> ensures that no aspect of the dependency structure is left out of the explanation, if there is
> some way to state it.**"*

That is a principled answer to "how much internal state do I expose to the student" — better than
either dumping the whole trace or hand-writing a summary. For us: **tag tool-call intermediate
state as student-facing or internal, and promote through the internal nodes.**

### Explicitly *not* natural-language generation

> *"**sophisticated natural language generation techniques were inappropriate for CyclePad.** The
> ability to automatically generate hypertext in response to a user's questions **obviates the
> need for discourse planning**… **Hypertext allows users to select how much they want to know
> about a topic.**"*

Per-type text renderers plus canned rationale strings. No grammar, no planner. **This is the
precise gap an LLM fills** — and it is worth being clear that the LLM fills the *rendering*
layer, not the derivation layer.

### What an explanation actually looks like

```
Q: Why is T-sat(S8) = 295.0°C?
A: T-sat(S8) = 568.2 K
   was calculated by using
       P(S8) = 80.00 bar
   to interpolate from
   saturation table for WATER
   because
   S8 is made of water
```

And the assumption-footprint query — *"Show assumptions underlying eta-thermal(CYCLE)"* — returns
the complete leaf set of the dependency network in English:

```
TUR1 works isentropically          P(S3) = 50.00 kPa
CLR1 works isobarically            m-dot(S3) = 5.00 kg/s
HTR1 works isobarically            T(S4) = 20.00°C
PMP1 works isochorically           P(S2) = 5,000 kPa
PMP1 works adiabatically           T(S2) = 500.0°C
TUR1 works adiabatically           S2 is made of water
CyclePad is not calculating velocity values     CYCLE is a heat engine
```

**Every assumption behind a 29.96% thermal efficiency, listed.** Note the meta-assumption
*"CyclePad is not calculating velocity values"* — a *reintroduction* technique, surfacing a
modelling choice the engine never had to represent explicitly.

**This is what our tutor should be able to do**, and an LLM cannot do it by narrating after the
fact. It requires the solver to build the justification structure while it computes.

---

## Coaching — four channels, and no student model

> *"CyclePad… is designed to be **more open-ended than typical ITS'** but provide **more
> scaffolding than traditional virtual laboratory software**… **In creating CyclePad we have not
> found student modeling to be necessary.**"*

**No bug library, no model tracing, no knowledge tracing, no step-level correctness grading.**
What replaces them: the physics rejects impossible states, and *teleology plus norms* flag
values that are legal but suspicious. Coaching is **pull, not push**.

That is a second independent data point alongside
[Andes' abandoned Bayesian model](andes.md) — two of the most sophisticated tutoring systems of
the era concluded they didn't need a student model.
→ [knowledge tracing](../concepts/knowledge-tracing.md)

**CARNOT — role inference.** 107 evidential rules infer each component's *functional role* from
structure, Bayesian, with a lovely robustness note: *"the introduction of significant amounts of
noise into these estimates does not materially affect the outcome."* Students can ask **why a
role is believed and why alternatives were rejected**. Its first design — dependency-directed
search — was *"far too slow to be deployed"* and produced *"a plethora of similar solutions."*

**Norms — 18 of them**, 2–6 per component, turning roles into advice. The output register is
worth copying exactly: **hedged claim + domain rationale**.

```
The temperature at S2 may be low.
   Cycle efficiency is directly related to the maximum cycle temperature,
   so making the outlet temperature as high as possible will increase
   cycle efficiency
The phase of S4 should probably be saturated liquid.
   Vapor cycles that condense their working fluid do so because pumps
   cannot handle a saturated mixture...
```

**The Guru — a server-side email coach**, and its rationale is our onboard-vs-hosted question
verbatim: instructors *"do not want to see memory requirements rise, and instructors who rely on
it daily are **adamant about keeping it stable**."* So new coaching went server-side and migrated
onboard only once stable. **A constraint we should design around now** — instructors will not
accept a tutor whose behaviour changes mid-semester.

Its help policy is a direct rebuke to the LLM instinct to be maximally helpful:

> *"**we want to nudge students in useful directions, rather than solving problems for them.**
> Consequently, the Guru provides plausible specific suggestions, but **does not attempt to
> validate those suggestions in the students' context. Understanding why a suggestion will or
> will not work in a particular circumstance is an important learning experience that we want
> students to have.**"*

**Case-based design coaching** retrieves analogous designs (MAC/FAC + the Structure-Mapping
Engine) from a library of **13 cases**, and **caps output at 2 suggestions** *"so that students
are not deluged with advice."*

### ⭐ The case compiler — the authoring model to steal

> *"our cases are **generated automatically from instructor input by a case compiler that uses
> CyclePad to build the necessary representations**… instructors provide **two snapshots of a
> CyclePad design, one before and one after their transformation**. They also specify the goals…
> **case authors only need to be thermodynamics experts, not AI experts.** … (It also checks to
> ensure that the transformation actually achieves the claimed goals, **since even experts can
> make mistakes**.)"*

**Instructors author by doing the thing in the tool.** The system compiles the formal case,
*verifies it achieves the stated goal*, and needs no indexing. Set against
[Andes' full-time knowledge engineer for nine years](andes.md), this is the authoring-cost answer
— and the modern analogue is obvious: capture instructor demonstrations as traces, auto-verify,
retrieve over the structured representation.

---

## ⚠ Contradiction detection, in full

Two sources: **numerical over-determination** (a second, materially different value for a known
parameter) and **violated qualitative constraints** (the process episodes above). Plus a
topological check at the Build→Analyze transition.

The dialog names the violated constraint *in raw predicate form* alongside the offending numbers:

```
There is a contradiction
  Symptoms of the problem
    Mutually Inconsistent-----
    (>= (T HTR1) (T S2))
    T(HTR1) = 600.0°C
    T(S2)   = 700.0°C
  You must retract one of these assumptions
    T(S2) = 700.0°C        T(HTR1) = 600.0°C
```

And it is **extensible via a stack of contradiction handlers** — out-of-table-bounds values get a
special handler showing *"a table-boundary diagram and a dot showing the location of the
out-of-bounds value."* Domain-specific visual explanation, special-cased on top of a generic
mechanism.

---

## ⚠⚠ The warning we must put in our own introduction

The single most important sentence in the paper, and it is a negative result:

> *"**Introducing CyclePad into such courses can lead to a drop in student performance, since
> students are being tested on mechanical calculation skills that in practice are automated.**
> One of the major problems we have found for instructors using CyclePad is incorporating a
> design orientation into introductory courses."*

> *"**To gain the full potential benefits of CyclePad will require rethinking what is taught in
> engineering thermodynamics.**"*

Supporting datum, from their own footnote: *"In a typical textbook we surveyed, **90% of the
exercises required numerical answers.**"*

**Twenty-seven years later this is precisely the LLM-in-the-classroom problem**, and CyclePad's
answer was that **the curriculum has to change, not the tool.** If our capstone is evaluated
against a course whose assessments reward manual property-table interpolation, we should expect
the same result — and it converges exactly with
[Andes' subscore finding](andes.md) that step-based tutoring moved process (+1.21) and not
answers (−0.08).

## ⚠ And the honest gap: there is no efficacy evidence

**The 1999 paper contains no controlled study, no learning-gain number, and no pre/post test.**
Its evidence is adoption and testimony: **2,593 distinct downloads from 63 countries (Apr 1997 –
Sept 1999)**, ~4/day, self-reported as 1,200 students / 426 professors / 598 engineers; at least
80 students per year in directly observed classroom use; and the claim that *"Advanced
thermodynamics students at the US Naval Academy were able to tackle more complex term projects
than they were able to previously, resulting in some cases in publishable technical papers."*

**Cite CyclePad for its architecture. Be explicit that its efficacy was never established the way
[Andes'](andes.md) was.** (Four Baher conference papers 1998–1999 are cited as "mounting
evidence" — a separate reader is chasing those now.)

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
- [ ] ⚠ **Running it may not be possible.** The paper states downloaded versions *"will expire
      in about a year"* — the binaries have a time bomb, and ours is a 2001 build. Worth one
      attempt in a VM, but do not plan around it.
- [ ] ⚠ **The promised open-source release never happened.** The paper says *"the source will be
      made publicly available through an open-source license in 2000"*; a GitHub code search
      returns zero repositories and QRG still distributes binaries only. **Treat "source is
      available" as false.**
- [ ] ⭐ **What *is* available in source is the reasoning substrate** — the LTRE/LTMS from
      *Building Problem Solvers* at
      [qrg.northwestern.edu/BPS](https://www.qrg.northwestern.edu/BPS/readme.html). If we want
      the dependency-network machinery, that is the real artifact to read.
- [ ] Chase the four Baher conference papers (FIE 1998, AERA 1998, AAHE 1999, FIE 1999) cited as
      the efficacy evidence.

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
- [Forbus, Whalley, Everett, Ureel, Brokowski, Baher & Kuehne (1999). "CyclePad: An articulate virtual laboratory for engineering thermodynamics." *Artificial Intelligence* **114(1–2), 297–347**](https://www.qrg.northwestern.edu/papers/Files/CyclePad_AIJ99.pdf) `[read]` — all 51 pp. plus figures. **Free PDF from QRG.**
- [Forbus & de Kleer, *Building Problem Solvers* — LTRE/LTMS source](https://www.qrg.northwestern.edu/BPS/readme.html) `[found]` — the reasoning substrate, actually available
- Everett, J. O. (1999). CARNOT teleological reasoning. *Artificial Intelligence* 113, 149–202 `[found]`
- "Using Articulate Virtual Laboratories in Teaching Energy Conversion at the U.S. Naval Academy," *J. Educational Technology Systems* (1998), ERIC EJ561409 `[in progress]`
- Rosé et al. "CycleTalk: Toward a Dialogue Agent That Guides Design with an Articulate Simulator," ITS 2004 `[in progress]`
- "Evaluating the Effectiveness of Tutorial Dialogue Instruction in an Exploratory Learning Context," ITS 2006 `[in progress]`
