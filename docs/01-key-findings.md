# Key Findings

Five results from the literature that constrain anything we eventually build. If a design
proposal contradicts one of these, it needs to say why.

> **This document has been superseded in scope by
> [`knowledge/PAPER.md`](../knowledge/PAPER.md)**, the full state-of-the-art survey, which
> covers these five findings plus the historical ITS literature, the university deployment
> landscape, and the thermodynamics-specific benchmark results. These five remain correct;
> read them as the short version.
>
> One correction since: the claim in
> [`03-open-questions.md`](03-open-questions.md) B4 that a thermodynamics benchmark would be
> our novel contribution was **wrong** — [ThermoQA](../knowledge/domain/thermoqa.md) and
> [UTQA](../knowledge/domain/utqa.md) already exist.

---

## 1. Socratic design gets routed around by students

**The finding.** A 2026 bottom-up taxonomy of student discourse with a Socratic AI physics
tutor coded **2,874 student turns across 221 sessions** into 357 categories. The top 25
categories account for roughly half of all turns, and they cluster into two bands:

- **Equation handling (~1/3 of top categories).** Writing energy equations (8.3%),
  solving for velocity (2.8%), computing heights (2.3%), algebraic simplification (1.7%).
  The authors call this "epistemic games" — symbol manipulation with limited conceptual
  engagement.
- **Meta-procedural requests.** Asking the tutor **"what do I do next"** was the
  **second-most-common student move overall, at 4.4% of all turns.** Plus requests for
  the relevant principle (1.5%) and the problem's assumptions (1.3%).

The top 20 categories contained *virtually no* conceptual reasoning, prediction, or
critical engagement with what the tutor suggested.

The authors' own summary: *"a tutor explicitly designed not to direct students
nevertheless elicits a discourse in which directing is the second-most-requested
service."*

**Why it matters to us.** "Use Socratic questioning" is a stance, and students route
around stances. A tutor that only ever asks questions produces a student who spends the
session asking to be told what to do. Refusal alone converts an answer-seeking student
into a frustrated answer-seeking student.

**Implication for design.** The pedagogical *move* — elicit, hint at level 1/2/3, show a
worked example, reveal — should be chosen by deterministic logic that can see the
student's attempt history, not by the language model's willingness to hold a line. The
student is allowed to ask "what do I do next." Whether that ask is granted, and at what
grain, is a policy decision with state behind it.

**Open question for our interviews.** Is "what do I do next" a failure of the student, or
a legitimate request that the Socratic frame wrongly pathologizes? Sometimes a student is
genuinely stuck at the level of strategy, not concept, and question-asking is just
obstruction. We should find out.

---

## 2. LLMs are specifically and predictably unreliable at thermodynamics

**The finding.** A 22-problem thermodynamics benchmark (arXiv 2502.05195) across GPT-3.5,
GPT-4, GPT-4o, Llama 3.1, and Mistral's le Chat:

- Simple problems: handled well. Large jump from GPT-3.5 → GPT-4; no significant
  difference GPT-4 → GPT-4o.
- Advanced problems: GPT-3.5 consistently failed to produce meaningful responses.
- **The instructive failure:** on a problem involving an adiabatic process where the text
  does *not* state whether the process is reversible, assuming reversibility is wrong —
  and **every model made that assumption, in every one of three repetitions.**

Reported weak spots elsewhere: property-table lookup, entropy calculations, symbolic
handling of van der Waals.

**Why it matters to us.** The adiabatic result is not a hallucination in the usual sense.
The model made a *plausible, standard, and unwarranted engineering assumption* — exactly
the error our students make, stated with total confidence. A tutor that does this is
worse than no tutor, because it validates the misconception.

**Implication for design.**

- Thermodynamic property values come from a computational tool (CoolProp, Cantera,
  IAPWS-IF97), never from model weights.
- **Reference-state gotcha:** Cantera uses the reaction-thermodynamics convention (zero
  enthalpy at 298.15 K, 1 atm); CoolProp and NIST use different conventions. Neither
  necessarily matches the Cengel or Moran tables in front of the student. Pin the
  convention explicitly or every enthalpy will be silently off by a constant.
- "Which assumptions are and aren't licensed by this problem statement" is arguably the
  single most valuable thing a thermo tutor could teach — and the thing base models are
  measurably worst at. That is a real opportunity.

---

## 3. Don't use an LLM as the student model

**The finding.** *Faster, Cheaper, More Accurate: Specialised Knowledge Tracing Models
Outperform LLMs* (arXiv 2603.02830). Purpose-built knowledge tracing models — BKT, DKT,
SAKT, transformer and GNN variants — beat GPT-3.5/4 on predictive accuracy and AUC for
knowledge tracing, at millisecond latency and orders of magnitude lower cost per
prediction.

**Why it matters to us.** The temptation is to ask the LLM "how well does this student
understand entropy?" It's the wrong tool: worse answers, slower, more expensive, and
non-reproducible — which also makes it unpublishable.

**Implication for design.** Separate the roles. The LLM handles dialogue. A statistical
model owns per-concept mastery state. Bayesian Knowledge Tracing is the right starting
point for a capstone: four interpretable parameters (prior knowledge, slip, guess,
learn), a forty-year track record, and you can actually explain it in a defense. DKT as a
comparison arm if there's time.

---

## 4. Tutoring quality is now measurable — and it trades off against subject expertise

**The finding.** A benchmark ecosystem now exists:

- **MathTutorBench** (EMNLP 2025, ETH LRE) — three axes: subject expertise, student
  understanding (verify/locate/correct a student's solution), and teacher response
  generation. Open-ended pedagogical quality is scored by a reward model trained to
  discriminate expert from novice teacher responses.
- **MRBench** — partial tutor-student conversations from MathDial and Bridge, each
  cut at the moment the student errs or shows confusion.
- **BEA 2025 shared task** on pedagogical ability assessment of AI tutors.

Headline result: **subject expertise does not translate into good teaching.** Pedagogy
and subject expertise form a trade-off navigated by how tutoring-specialized the model
is.

**Why it matters to us.** This is the difference between "we made a chatbot" and "we made
a measurable contribution." It also means raw model capability is not our lever — a
smarter base model does not make a better tutor, and might make a worse one.

**Implication for design.** A thermodynamics analogue of MathTutorBench does not exist.
Building one is tractable for a capstone team, useful to other people, and independently
publishable even if the tutor itself never ships.

---

## 5. We have a validated pre/post instrument, and it's ours

**The finding.** The **Thermodynamics Concept Inventory (TCI)** was developed at Penn
State, patterned on the Force Concept Inventory: brief, minimal computation, repeatable
across diverse populations, measures conceptual understanding rather than
problem-solving. A related **Thermal and Transport Concept Inventory — Thermodynamics
(TTCI-T)** also exists. Both are catalogued on PhysPort with usage guidance.

**Why it matters to us.** A validated instrument developed at our own institution removes
the largest methodological objection to a capstone learning study — "how do you know they
learned anything?" Normalized gain on a published concept inventory is a defensible
answer.

**Implication.** Get access early. PhysPort gates these instruments behind educator
verification; our instructor sponsor is the path. Also decide now whether we're measuring
conceptual gain (TCI) or problem-solving performance (course grades), because they are
not the same thing and the literature is full of interventions that move one and not the
other.

---

## Cross-cutting: the thing all five have in common

Every one of these findings points the same direction: **the intelligence is not the hard
part.** The hard parts are policy, state, verification, and measurement — all of which
live outside the model. Any design that puts pedagogy in a system prompt is repeating a
known failure.
