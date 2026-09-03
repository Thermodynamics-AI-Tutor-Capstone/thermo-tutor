# CyclePad and CycleTalk — the articulate simulator

**Type:** system
**One line:** An "articulate virtual laboratory" for engineering thermodynamics — a simulator
that explains the derivation behind every value it computes — deployed at the US Naval Academy,
Northwestern and Oxford from 1996, with a dialogue-agent successor built at CMU.
**Why we care:** **This is the closest historical precedent for our project, and the modern
LLM-tutoring literature does not cite it.** Its architecture is, in outline, the one we
independently proposed. It is downloadable and still runs.

> **Status: `[read]` — the 1999 *Artificial Intelligence* paper (all 51 pp.), the shipped software
> artifact, the ITS 2006 controlled evaluation, and — since **2026-09-03** — the **AI-ED 2005
> human-tutor study** in full. ⚠ **Reading Rosé 2005 as a primary changed what this node claims
> about human tutoring in thermodynamics; see that section.** The IJAIED 2006 account is still
> out of reach.

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
CyclePad**, intended to engage students in *"negotiation dialogues"* about design trade-offs.
⚠ **The negotiation dialogue was never built** — see below. Same ONR
funder (Cognitive and Neural Sciences, N000140410107). **Read in full below** — it answers the
question our whole project asks.

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
what students actually ask. **CycleTalk was the attempt to close that gap in 2004–2006. It
worked, modestly, and the section below is the most directly relevant evidence we have.**

---

# CycleTalk — dialogue on top of the articulate simulator

**The hypothesis**, verbatim: *"negotiation-style dialogue will lead to better learning than
previous tutorial dialogue systems because (1) it **motivates students to explain more in order
to justify their thinking**, and (2) it supports the students' **meta-cognitive ability to ask
themselves the right questions about the choices they make**."*

Domain: **Rankine cycles** — simple, with reheat, with regeneration. Students design and
**optimize** cycles rather than solve textbook problems.

## ⭐ The content-development pipeline — the most reusable thing here

This is the method the [Andes team recommended](andes.md) and that we have been considering.
CycleTalk actually did it, and validated it:

1. **Collect a corpus of human tutoring** in the real environment — from the earlier classroom
   study where human tutors supported students using CyclePad.
2. **A thermodynamics domain expert** performed a topic analysis using an exploratory corpus tool
   (InfoMagnets). Each student protocol split into 10–25 segments; **≈379 topic segments** total,
   yielding **15 distinct topics**, with each student covering 4–11 of them.
3. **Validate that the topics matter before authoring anything.** They found *"a strong and
   reliable correlation between topic coverage (i.e., percentage of topics discussed at least
   once) and post-test score, with pre-test score used as a covariate (**R² = .715, N = 21,
   p < .05**)."*
4. **Author dialogues against the validated topics** — **12 Knowledge Construction Dialogues**,
   **7 on optimization specifics, 5 conceptual**.
5. **Attach them to a tutor backbone.** They used **CTAT Pseudo Tutors** — authored *"without
   programming, namely, by demonstrating correct and incorrect solutions,"* stored as a
   **Behavior Graph** whose nodes are student actions. Dialogues fire either **on a hint request**
   or **as a success message** when a node is completed.

**Step 3 is the step to steal.** Validate topic coverage against outcomes *before* investing in
authoring. It is cheap, it is a real finding in its own right, and it tells you which topics are
worth the effort.

## What the dialogue actually sounds like

Verbatim from a real session:

> **Tutor:** Let's stop for a minute and reflect on what we have seen. Having seen how changing
> T-Max (i.e., the Maximum Temperature at the Heater Outlet) affects the efficiency of the cycle,
> do you think it is a good idea in general for the Maximum Temperature to be increased and kept
> high?
> **Student:** yes
> **Tutor:** Okay. Let's think now about one important consequence of keeping T-Max high. What
> happens to the steam quality at the turbine exit if you increase the maximum temperature of the
> cycle?
> **Student:** Increases
> **Tutor:** Right. As increasing the temperature makes the efficiency and steam quality better,
> we should increase the maximum temperature of the cycle. But **can we keep on increasing the
> maximum temperature at the heater outlet indefinitely, or are there limitations to keep in
> mind?**
> **Student:** there are limitations such as material constraints
> **Tutor:** Great. we should try to keep T-Max as high as possible without risking safety
> concerns or exceeding the maximum temperature the material can withstand…

Note the shape: **reflect on what the simulator just showed → elicit a consequence → push to the
constraint that bounds it → consolidate into a principle.** It is short, it is Socratic in the
useful sense, and every turn is anchored to something the student just *did* in the simulator.

## ⚠⚠ The human-tutor study (Rosé et al., AI-ED 2005) — read in full, and it does not say what everybody reports

> **`[read — full text, 8 pp., 2026-09-03]`.** Local copy:
> `course-materials/papers/rose-2005-npsg-human-tutor.pdf` (+ `.txt`). ⚠ **Table 1 is embedded as
> an image and does not survive text extraction** — the numbers below were recovered by pulling
> the image out of the PDF. That is why every secondhand account of this study quotes only the
> p-values.

Rosé, C. P., Aleven, V., Carey, R. & Robinson, A. (2005). *"A First Evaluation of the
Instructional Value of Negotiable Problem Solving Goals on the Exploratory Learning Continuum."*
**AI-ED 2005**, Carnegie Mellon (HCII + Mechanical Engineering).
ONR grant **N000140410107**. This is the study that produced the human-tutoring corpus CycleTalk
was built from — **not** a Wizard-of-Oz study, and not a pilot.

### The design is a 3 × 2, not a three-way

⚠ **This node previously described it as three conditions. It is six.**

**Goal Level** (the manipulation that mattered):

| Condition | What the student got |
|---|---|
| **S** — Script | Problem-solving goals **and** the suggested analyses, in a fixed order. Still requires means-ends analysis to follow |
| **PS** — Problem Solving | Goals in a fixed order; the student chooses which analyses meet them. *"Help provided in the style of typical model tracing tutors"* |
| **NPSG** — Negotiable Problem Solving Goals | Same goal list, but the student **selects and orders the goals in negotiation with a human tutor**, over VNC |

**Goal Orientation** (crossed with the above): students were told either *"your goal is to learn
as much thermodynamics as possible"* (**LO**) or *"your goal is to achieve the greatest cycle
efficiency"* (**PO**).

⭐ **Content control was unusually strict, and it is a model for our own study.** All materials —
take-home assignment, 11-page Rankine overview, three sets of focused readings, and the identical
pre/post test — were written by **a CMU mechanical engineering professor and three of his graduate
students, "with minimal input from our team,"** and were **identical across all six conditions**
except for the manipulation instructions. *"Thus, we strictly controlled for information
presentation in all written materials."*

**Procedure:** a take-home lab in week 1, then a **3-hour on-campus lab in week 2** split into 8
timed segments — 20 min pre-test (50 points), 15 min reading, 3 × ~20–25 min of focused materials
(**this is where the manipulation happened**), **40 min of unsupported Free Exploration** building
the most efficient Rankine cycle they could, 20 min post-test, questionnaire.

**Outcomes:** 32 multiple-choice/short-answer *analytical* items (heavy on **predicting how one
cycle parameter changes another**), 9 open-response *conceptual* items, and **Free Exploration
success** — did the student actually build a working optimized cycle. Test results are reported as
**residuals from a pretest→posttest regression**, not raw gains.

**Participants:** a sophomore thermodynamics course at CMU, 120 students; **67 both did the
take-home and consented**, plus 30 who did the lab but not the take-home. The learning analysis
has **df = 83**, so roughly 86 students across six cells.

### ⭐⭐ Table 1, recovered from the image — and it is much weaker than the p-values suggest

Values are **residuals** (percentage points above or below the post-test score predicted from the
pre-test), with SD in parentheses.

| Measure | **S** (script) | **PS** (pseudotutor) | **NPSG** (3 tutors) | Tutor 1 | Tutor 2 | Tutor 3 |
|---|---:|---:|---:|---:|---:|---:|
| **Free Exploration success** | **63%** | 58% | **63%** | **100%** | **38%** | **0%** |
| Total test residual | 1% (9) | **−2%** (9) | 2% (10) | 3% (6) | 3% (10) | **−7%** (9) |
| Conceptual residual | **3%** (13) | **−5%** (13) | **3%** (16) | **12%** (3) | 10% (3) | **−18%** (6) |
| Analytical residual | −1% (11) | −1% (10) | 5% (12) | 8% (10) | 4% (9) | 3% (17) |

**Read the first row before anything else. On the applied design task, human tutoring and a
written script tie exactly at 63%, and the pseudotutor is at 58%. There is no main effect for goal
level on Free Exploration at all.**

**Read the third row next. On the conceptual test, S and NPSG are identical at 3%.** The paper
concedes it: *"both S and NPSG were significantly better than PS (p < .05), whereas the difference
between NPSG and S was only a trend (p = .16)."*

The reported main effect — **F(2,83) = 3.81, p < .05, MSE = 20.9** — is on the total test, with
the order **PS < S < NPSG**, and the post-hoc breakdown is:

| Contrast | Result |
|---|---|
| **NPSG vs. PS** | **significant, p < .05** |
| NPSG vs. S | ⚠ **marginal, p = .11** |
| S vs. PS | a statistical trend only |

⚠ *This node previously reported NPSG vs. S as "p < .1". It is **p = .11** — on the wrong side of
even the marginal threshold.*

> **So the finding is not "human tutoring wins." It is: the model-tracing-style pseudotutor lost,
> and human tutoring was statistically indistinguishable from a well-written script.**

**The magnitude is the other half of it.** NPSG's advantage over the script on the total test is
**one to two percentage points against standard deviations of 9–10** — roughly **d ≈ 0.1–0.2**.
The only comfortably significant contrast, NPSG over PS, is about **5 points against SD ≈ 9**,
so **d ≈ 0.5** — and *that* is a human tutor beating a piece of software, not a design principle.

### ⚠⚠⚠ One tutor of three carries the result, and a second one lost to the software

This is the finding that should govern how the study is cited.

| | Free Exploration success |
|---|---:|
| **Tutor 1** | **100%** |
| Script (no tutor) | 63% |
| Pseudotutor | 58% |
| **Tutor 2** | **38%** |
| **Tutor 3** | **0%** |

Between-tutor difference within NPSG: **p < .005** (binomial logistic regression). **Tutor 2's
students did worse than students who had no tutor at all.** Only Tutor 1 beat the software.

And **Tutor 3's data was deleted from the learning-gains analysis.** The authors' description is
worth quoting in full because it is the clearest published account of how a human tutor fails:

> *"He was extremely terse and impatient with students. His transcripts contained almost no
> conceptual discussion, and in his impatience, **he rarely let students complete their work.
> Instead, he tended to take over and do the lab for them** through the VNC connection to their
> simulation interface."*

**Conceptual residual −18%. Free Exploration success 0%.** ⭐ **A human tutor who takes over the
work produces the worst outcome in the study — worse than no tutor, worse than the software, and
by a wide margin.** That is [VanLehn's completion mechanism](../concepts/vanlehn-2011.md)
demonstrated by its violation, in our own domain, twenty years ago: the students never
self-generated a solution, so they learned nothing.

⚠ **The authors' defence of the result is that Tutor 3's badness proves it was not a "warm body"
effect** — students did not simply benefit from having a human present. That is a fair argument
about *mechanism*. It is not a defence of *magnitude*, and it does not address the fact that
Tutor 2, who was kept in the analysis, underperformed both software conditions on the applied task.

**How to cite this study honestly:** *three graduate-student tutors produced outcomes ranging from
the best in the experiment to the worst, the mean was indistinguishable from a written script, and
the only reliable finding was that all of it beat a model-tracing-style pseudotutor.*

### ⭐ The one design-relevant confound

**NPSG students were tutored one-on-one. PS and S students sat in group lab sessions.** So
"negotiated goals" is confounded with "individual attention." Assignment was also **not random** —
students were placed *"in such a way as to maximize the evenness in distribution of grade so far
between conditions and to respect student availability during 4 lab session times."* Average
course grade was matched across conditions, which handles the obvious confound and not
self-selection by schedule.

⚠ **VanLehn's 2011 review includes this study anyway**, in his human-vs-step-based table, despite
listing random assignment as an inclusion criterion. See the discrepancy below.

### ⭐ The goal-orientation manipulation did nothing — and that is a finding for us

Students were explicitly told to prioritise **learning** or **performance**. The manipulation
check worked: LO students picked the learning-oriented answers more often (t = 2.33, p < .05 on
one item; t = 1.58, p = .11 on the other).

**And it changed no outcome.** No main effect on the total test, the conceptual test, the
analytical test, or Free Exploration; no interaction with goal level. The authors: *"in contrast
to findings in McNeil & Alibali (2000), we found very little evidence of any Goal Orientation
effect."*

> ⚠ **Telling students to adopt a learning orientation demonstrably changed what they said and
> demonstrably changed nothing they did.**

**This is a direct hit on a cheap idea our project would otherwise reach for.** Framing text —
"focus on understanding, not on getting the answer" — in a system prompt, a landing page, or an
onboarding screen is exactly this manipulation, and it is the one thing in this study that was
cleanly measured and cleanly null.
→ [engagement decay](../concepts/engagement-decay.md), [guardrails](../concepts/guardrails.md)

### ⭐⭐ The tutoring behaviour worth stealing, stated in our own domain

The authors describe one specific, recurring, implementable intervention — and it is the only
concrete piece of tutoring policy in this whole literature that is written in the language of
thermodynamic cycle design:

> *"One common pattern that we have observed is that **students start out with the idea that more
> sophisticated designs will be more efficient.** Thus, students have a tendency to be drawn
> towards the more advanced portions of the design space before they are ready to fully understand
> how to use that sophistication to an efficiency advantage. When our tutors observe this
> behavior, **they encourage students to keep it simple and direct them back to more basic design
> explorations until students demonstrate a solid understanding at that basic level.**"*

**Premature complexity is the named failure mode, and pulling the student back to the simple cycle
is the named intervention.** It is detectable from simulator state alone — a student adding reheat
and regeneration before they can predict what T-max does to steam quality — which makes it a
**deterministic trigger, not a prompt**. → [a pedagogical policy outside the prompt](../PAPER.md),
[our skill graph](../../research/domain/skill-graph-draft.md)

⚠ **Note what it is not: it is not Socratic questioning, and it is not a hint.** It is
**outer-loop task selection** — the tutor deciding what the student works on next. Which is
[the hypothesis VanLehn declared dead for human tutors](../concepts/vanlehn-2011.md), turning up
here as the thing the tutors actually did.

### ⚠ Two discrepancies with VanLehn's review, both unresolved

1. **VanLehn lists this study as `d = −0.07`** in Table A8, *Human Tutoring Versus Step-Based
   Tutoring* — i.e. the step-based tutor slightly *beat* the human tutors — with the note *"Data
   from one human tutor were excluded,"* which matches Tutor 3 exactly. **But the paper's own
   analysis reports NPSG > PS at p < .05**, which would be a positive d of roughly 0.5. **We
   cannot reconstruct −0.07 from any contrast in Table 1.** Either VanLehn used a measure or a
   pairing we cannot see, or he obtained data from the authors. **Recorded as unresolved; do not
   quote either number as though the other did not exist.**
2. **VanLehn describes the domain as "Carnot engines."** It is **Rankine** cycles — simple, with
   reheat, with regeneration. Small, but it is one more instance of detail drifting on the way
   into a review.

### What this study actually gives our project

1. ⭐ **The strongest content control in this literature, and it is copyable.** Same professor-written
   materials in every arm; only the interaction differs. **That is the design our own study should
   use**, and it is the reason this null-ish result is worth more than a bigger sloppier one.
2. ⚠ **Human tutoring in thermodynamics did not beat a good written script.** Anyone pitching an
   AI tutor against "the tutoring effect" in this domain should know that the one controlled
   attempt found *d ≈ 0.1–0.2 against text*, from graduate-student tutors, on a 3-hour dose.
3. ⭐ **Tutor variance is larger than the treatment effect.** 100% / 38% / 0%. If our tutor is
   consistent, consistency alone is a claim — a floor, not a ceiling.
4. ⭐ **A named, detectable, domain-specific failure mode** (premature design complexity) with a
   named intervention (pull back to the simple cycle).
5. ⚠ **Motivational framing text does not work.** Measured, and null.

---

## ⚠ The evidence — read carefully, because the headline overstates it

**The ITS 2006 study** replaced the human tutor with the authored dialogue agents.

- **N = 31** sophomore thermodynamics students, Carnegie Mellon, extra credit, 1.5 weeks after
  Rankine cycles were lectured
- **3-hour lab, 9 segments, strictly time-controlled** across conditions
- Conditions differed **only** in the software version: **S** (plain CyclePad), **PSHELP** (KCDs
  fire on hint requests), **PSSUCCESS** (KCDs also fire as success messages)

| Condition | Pretest | Posttest | FreeExplore 1 success | FreeExplore 2 efficiency |
|---|---|---|---|---|
| S | 20.64 (5.56) | 31.39 (5.86) | 23% | 38.14 (10.97) |
| PSHELP | 20.67 (3.56) | 27.83 (6.02) | **0%** | 38.09 (13.12) |
| PSSUCCESS | 24.86 (4.10) | 32.45 (4.06) | 20% | 34.09 (14.17) |

**⚠ The control comparison was discarded by the authors.** A quiz on Rankine cycles was
administered between the day-1 sessions (control) and the day-2 sessions (both experimental
conditions). Pretest scores rose across sessions (R² = .14, p < .05). *"we disregard the
comparison between the control condition and the two experimental conditions and focus only on
the difference between the two experimental conditions."*

**And it is worse than the quiz alone.** Assignment was **by lab session, not randomized** — both
day-1 sessions were S, day-2 session 1 was PSHELP, day-2 session 2 was PSSUCCESS. The authors
learned about the intervening quiz only after the experiment had started.

**⚠⚠ The raw gains, which the paper reports but never computes, run *against* the dialogue
conditions:** S **+10.75**, PSHELP **+7.16**, PSSUCCESS **+7.59**. And on *both* practical
measures plain CyclePad is best or tied — Free Exploration 1: **23% vs 0% vs 20%**; efficiency
achieved: **38.14 vs 38.09 vs 34.09**. The concept-level ANOVA that produces the 0.35 SD uses one
observation per concept with concept pretest as a covariate, which is why it can find an effect
the raw totals do not show.

Everyone learned regardless: main effect of test phase **F(1,60) = 44.98, p < .001**, with no
interaction with condition.

**So the headline result is a *dose* manipulation, not dialogue-versus-no-dialogue:**
PSSUCCESS > PSHELP, **p < .05, effect size 0.35 SD**, on concept-level pre/post scores.
Students in PSSUCCESS saw **2.7 KCDs on average; PSHELP saw 1.8.** Out of twelve.

**⚠ And there were no significant effects on either Free Exploration exercise** — the two
*practical* measures, fully defining a cycle and optimizing one. The learning showed up on the
conceptual test only. That echoes [Andes](andes.md) almost exactly: process and concepts move,
applied performance doesn't.

**⭐ The dialogue-versus-control comparison does exist, and it is positive** — in a follow-up at
the **US Naval Academy** contrasting S against PSSUCCESS: **F(1,86) = 5.57, p < .05, effect size
0.25 SD.** One sentence in the paper, no further detail, but it is the cleanest answer available
to *"does dialogue on top of an articulate simulator beat the simulator alone?"* — **yes, by
about a quarter of a standard deviation.**

## ⚠ The exposure problem, which is the real story

> *"only about **14% of the problem solving actions** of students were help requests."*

> *"**Only 1 of 7 KCDs** focusing on interpreting sensitivity analyses was viewed by **any**
> student in the PSHELP condition."*

> *"it is a concern that **so few of the authored KCDs were viewed by students on average even in
> the condition where they were viewed most frequently**."*

And their own closing assessment:

> *"the system we evaluated in this study still **falls far short of a full implementation of the
> NPSG condition**… the number of KCDs students view during their experience with the system
> **still need to be increased by a factor of 2 or 3**… they played more of a role of **eliciting
> reflection** from students rather than **assisting with navigation** to the same extent that the
> human tutors did."*

## ⚠⚠ The two findings that most change how we should read this

### 1. The negotiation dialogue was never built

The CHI paper is a **position paper — future tense throughout** (*"CycleTalk will engage
students…"*). Its celebrated exchange, in which a student proposes adding a second turbine and the
tutor pushes back on condensation, blade damage, reheat cost and maintenance, is an
**illustrative target, not system output.** The student holds the initiative, turns are long, and
the student ends by reasoning about payback period unprompted.

What was actually built and evaluated is **Knowledge Construction Dialogues** — directed lines of
reasoning inherited from Atlas-Andes. Compare the two excerpts on this page. In the real
transcript the **tutor** holds initiative throughout, asks a pre-scripted chain of short-answer
questions, and the student replies in one to five words (*"yes"*, *"Increases"*, *"there are
limitations such as material constraints"*) before the tutor states the principle itself.

**The 0.25–0.35 SD came from the second thing, not the first.** Nobody has ever measured the
negotiation design. When we cite CycleTalk as precedent, we are citing scripted KCDs — and the
vision document is a *specification of unfinished work*, which is a different and arguably more
useful thing to inherit.

### 2. ⭐ The dialogue agent never used the simulator's explanations

This is the most surprising finding in the whole investigation. **CyclePad's articulate
explanation facility — the entire point of the 1999 paper — is never invoked by CycleTalk.**
There is no description anywhere of the agent reading CyclePad's cycle state, component graph, or
constraint network to reason about *this particular student's design*. The coupling is shallow:
CTAT **model-traces the student's actions** against a pre-authored Behavior Graph, and KCD content
came from **corpus analysis of human tutors**, not from the simulator's own reasoning. The only
place simulator state is genuinely read is *scoring* — Free Exploration 2 was graded as "the
efficiency they achieved, as measured by the CyclePad simulator."

**So the two halves of the best precedent in our domain were never actually joined.** An
articulate simulator that can explain any value it derives, and a dialogue agent that talks about
thermodynamics, sat side by side for two years without the dialogue agent ever asking the
simulator a question.

**That is the specific unbuilt thing our project is positioned to build**, and it explains the
authors' own diagnosis: an agent that cannot see the design state cannot help you navigate it. It
can only recite reflection prompts attached to graph nodes.
→ [grounding and verification](../concepts/grounding-and-verification.md)

**Three lessons for us, and they are unusually direct:**

1. **Students almost never ask for help.** 14% of actions. A pull-only tutor in an exploratory
   environment will not be used enough to matter — which is why attaching dialogues to *success*
   events beat attaching them to *hint requests*. **Proactivity is not a nice-to-have; it was the
   experimental manipulation, and it was the thing that worked.**
   → [engagement decay](../concepts/engagement-decay.md)
2. **They got 0.25–0.35 SD while delivering 2 of 12 authored dialogues.** The authoring was
   mostly unused. Any estimate of our own content needs should assume most of it will not be
   seen unless we solve delivery.
3. **The human tutor did something the agent didn't: navigation support.** The agents elicited
   reflection well; they could not help students decide *what to do next in an open-ended design
   space*. **That is precisely the "what do I do next" request the
   [Socratic discourse taxonomy](../concepts/socratic-tutoring.md) found students make most —
   and it is exactly what an LLM is now good at.** It is the clearest statement anywhere of the
   gap our project could fill.

   ⭐ **And the 2005 human-tutor paper names the navigation move exactly**, in cycle-design terms:
   students *"are drawn towards the more advanced portions of the design space before they are
   ready,"* and the tutors *"encourage students to keep it simple and direct them back to more
   basic design explorations until students demonstrate a solid understanding at that basic
   level."* **Premature design complexity is the failure; pulling back to the simple cycle is the
   intervention; and both are detectable from simulator state without any language understanding
   at all.**

## Open questions — being read now

- [ ] The 1999 *Artificial Intelligence* paper: architecture, the reasoning engine, how
      qualitative reasoning and numerical property data interact, authoring cost
- [ ] **Any learning-outcome data from USNA, Northwestern or Oxford.** If it exists it is the
      only long-run evidence for thermodynamics tutoring anywhere. If it doesn't, that is a
      finding.
- [ ] CycleTalk's controlled evaluation (ITS 2006) — did dialogue beat unguided exploration?
- [x] ~~The Wizard-of-Oz studies~~ — **there were none.** No WoZ study is mentioned in the CHI
      paper, ITS 2006, or the ITS 2004 reference list. What preceded the system was a **human-tutor
      classroom study** (Rosé et al., AI-ED 2005), not a WoZ simulation.
- [ ] **[HIGHEST-VALUE REMAINING PULL]** Rosé, Kumar, Aleven, Robinson & Wu (2006), *"CycleTalk:
      Data Driven Design of Support for Simulation Based Learning,"* **IJAIED 16(2)**,
      DOI `10.3233/irg-2006-16(2)06`. Almost certainly the fullest account of the project —
      design rationale, corpus method, and the coupling detail. IOS Press is Cloudflare-blocked;
      **PSU library should have it.** Ask for this one by hand.
- [ ] Tuttle & Wu, *"Intelligent Computer Assisted Instruction in Thermodynamics at the U.S. Naval
      Academy"* (QR-2001) — found in the ITS 2004 reference list. A new lead for USNA outcome data.
- [x] ~~Rosé et al. (2005) AI-ED NPSG paper — every download path returns a Cloudflare challenge;
      design and results recovered secondhand from ITS 2006 §2.~~ **Read in full 2026-09-03.
      Three claims in this node were wrong: it is a 3 × 2 design not a three-way, NPSG vs. S is
      p = .11 not p < .1, and NPSG ties a written script on both the conceptual test and the
      applied design task.**
- [x] ~~The goal-orientation × tutoring-style study~~ — **it is the same study.** The
      learning-vs-performance framing manipulation **changed what students said and no outcome
      they produced.**
- [ ] ⚠ **Reconcile with VanLehn.** He lists this study at **d = −0.07** favouring the step-based
      tutor; the paper reports NPSG > PS at p < .05, which is a positive d of roughly 0.5. No
      contrast in the recovered Table 1 produces −0.07. **Ask VanLehn, or find his coding sheet.**
- [ ] **Did the promised corpus analysis of Tutors 1, 2 and 3 ever get published?** The 2005 paper
      says *"we are currently conducting an in-depth corpus analysis to gain deeper insights into
      what lead to the differences in effectiveness between Tutors 1, 2, and 3."* **That analysis
      is the single most valuable unpublished-or-unfound document in this whole line of work** —
      it is an account of what separated a 100% tutor from a 0% tutor, in thermodynamics.
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
- [**Kumar, Rosé, Aleven, Iglesias & Robinson (2006). "Evaluating the Effectiveness of Tutorial Dialogue Instruction in an Exploratory Learning Context." *ITS 2006*, LNCS 4053, pp. 666–674**](https://e-archivo.uc3m.es/bitstreams/2aa325b4-2f85-4561-9860-20ed9eb3b6ab/download) `[read]` — **the controlled evaluation.** Open copy via Universidad Carlos III (`hdl.handle.net/10016/17305`); Springer's is paywalled.
- Rosé, Aleven & Torrey. "CycleTalk: Supporting Reflection in Design Scenarios with Negotiation Dialogue." CHI workshop paper `[read]` — states the negotiation-dialogue hypothesis.
- **Rosé, Aleven, Carey & Robinson (2005). "A First Evaluation of the Instructional Value of Negotiable Problem Solving Goals on the Exploratory Learning Continuum." *AI-ED 2005*** `[read — full text, 8 pp., 2026-09-03]` — **the human-tutor study, as a primary.** Local: `course-materials/papers/rose-2005-npsg-human-tutor.pdf`. ⚠ **Table 1 is an embedded image**; extract it with `pdfimages -f 6 -l 6 -png` to get the numbers. Also indexed at [CMU KiltHub, DOI 10.1184/r1/6469769](https://doi.org/10.1184/r1/6469769) (Cloudflare-blocked).
- Rosé et al. "CycleTalk: Toward a Dialogue Agent That Guides Design with an Articulate Simulator," ITS 2004 `[found]`
- Funding: **ONR Cognitive and Neural Sciences Division, Grant N000140410107** — the same ONR line that funded [Andes](andes.md) and CyclePad itself.
