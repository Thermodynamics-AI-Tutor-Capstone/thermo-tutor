# The KLI framework — what kind of knowledge, therefore what kind of instruction

**Type:** concept / theoretical framework
**One line:** Koedinger, Corbett & Perfetti's argument that **instructional principles are not
properties of subjects, they are properties of *knowledge components*** — and their three
taxonomies (kinds of knowledge → kinds of learning → kinds of instruction) plus the mapping
between them.
**Why we care:** It is the theory that should ground
[our ~90 hand-authored knowledge components](../../research/domain/skill-graph-draft.md), which
currently have none. It gives **two operational tests of KC complexity** we can run on real course
data. And its KC-type → learning-process → instructional-principle mapping is **exactly the
decision table a tutor needs to choose what to do next**, which nothing else in this base
provides.

> **Verification: `[read — full text, 35 pp., 2026-09-03]`.** Local copy:
> `course-materials/papers/koedinger-2012-kli-framework.pdf` (+ `.txt`). Authors' final version.
> **This was `[found]` in the knowledge-components node and nowhere else.**

Koedinger, K. R., Corbett, A. T. & Perfetti, C. (2012). *"The Knowledge-Learning-Instruction (KLI)
Framework: Bridging the Science-Practice Chasm to Enhance Robust Student Learning."*
**Cognitive Science** 36(5), 757–798.
[DOI 10.1111/j.1551-6709.2012.01245.x](https://doi.org/10.1111/j.1551-6709.2012.01245.x).
Pittsburgh Science of Learning Center.

⭐ **The line to draw first:** Koedinger and Corbett are two of the four authors of **Anderson,
Corbett, Koedinger & Pelletier (1995)** — the paper
[VanLehn credits with first proposing the completion mechanism](vanlehn-2011.md), that all
self-generated correct solutions are equally effective. **This is the same group, seventeen years
later, saying what the *components* of that solution are and how each kind gets learned.** The two
papers are halves of one argument: VanLehn says *the student must generate the solution*; KLI says
*here is what the solution is made of and what each part needs.*

---

## ⭐⭐⭐ The central claim, and it is a claim about our field's arguments

> *"A hypothetical principle **'drill and practice is not effective for mathematics' is at the
> wrong level of analysis** because it does not describe what it is about mathematics that makes
> drill and practice unsuitable."*

> *"Rather than associate optimal instructional choices with domains (as disparate literatures on
> math education, physics education, reading, and second language learning are wont to do), the
> KLI framework suggests that **instructional choices depend on the kinds of KCs being
> targeted.**"*

**Almost every design debate in this knowledge base is conducted at the domain level and is
therefore, on this account, unanswerable as posed.** "Should a thermodynamics tutor be Socratic?"
has no answer. "Should a tutor use Socratic dialogue on a *knowledge component that has a
rationale*?" has one.

The authors name the fights this dissolves:

> *"The various instructional recommendations seem mutually incompatible without the taxonomy.
> They would reflect **'education wars':** More worked example study is at odds with more testing
> of recall, blocked comparison of examples is at odds with spacing, pure non-verbal practice is
> at odds with prompts for self-explanation and extended classroom dialogue and argumentation."*

⭐ **And they apply it to the biggest one we carry.** *Desirable difficulties* (Bjork, Roediger —
make it harder) versus *cognitive load theory* (Sweller — make it easier) look like a direct
contradiction. KLI's diagnosis: **the two literatures study different KCs, different learning
processes and different tests.** Desirable-difficulties research works on **facts**, **memory
processes** and **long-term retention tests**; cognitive-load research works on **rules and
schemas**, **induction/compilation**, and **transfer tests**. **They are not disagreeing. They are
describing different cells of the same table.**
→ [productive failure](productive-failure.md), which sits on the desirable-difficulties side and
should say which cell it occupies.

---

## Taxonomy 1 — kinds of knowledge component

A KC is a **condition → response** pair. Four distinctions, and they compose (Table 3):

| Application conditions | Response | Relationship | Rationale? | Common label |
|---|---|---|---|---|
| constant | constant | non-verbal | no | **association** |
| constant | constant | **verbal** | no | **fact** |
| **variable** | constant | non-verbal | no | **category** |
| **variable** | constant | **verbal** | no | **concept** |
| **variable** | **variable** | non-verbal | no | **production, schema, skill** |
| **variable** | **variable** | **verbal** | no | **rule, plan** |
| **variable** | **variable** | **verbal** | ⭐ **yes** | **principle, rule, model** |

**Read the four distinctions as four questions to ask of every component in our skill graph:**

1. **Does it apply in one situation or many?** (constant vs. variable *conditions*)
2. **Is the answer always the same, or does it depend?** (constant vs. variable *response*)
3. **Can the student say it in words?** ⚠ **This is not the same as whether they can do it.**
4. ⭐ **Does it have a rationale — a reason it is true — or is it a convention?**

⚠ **Distinction 4 is the one that decides whether Socratic dialogue is worth anything:**

> *"Instruction that involves students in explicitly discovering KCs from data or **deriving KCs
> through argumentation may be productive for KCs with a rationale, but not for ones without.**"*

**You cannot argue a student into a steam table.** The value of `T_sat` at 2 MPa is a convention
of measurement — a constant-constant fact with no rationale — and asking a student to reason
towards it is wasted effort. **The First Law applied to an open system has a rationale, and
argumentation is exactly right for it.** Our tutor needs to know which is which, per component,
before it decides how to respond.

### ⭐ Integrative KCs — the ones you cannot see in a single task

> *"KCs sometimes are **not inferable from a single behavioral pattern**, but only from
> behavioral patterns across task situations varying in complexity."*

The canonical example: Heffernan & Koedinger (1997) found students far worse at translating
**two-step** algebra story problems (`800 − 40x`) than at two matched **one-step** problems
(`800 − y` and `40x`). The missing thing is not either skill — **it is the component that lets you
embed one expression inside another.** Instruction targeted at that specific component
significantly improved performance.

⭐⭐ **The discovery method is arithmetic and we can run it.** If the integrative KC's probability
`Pi` is independent of the supporting KC's `Ps`:

```
Pi  =  P(success on the hard task)  ÷  P(success on the easy task)
```

**Every thermodynamics problem that combines two steps students can each do separately is a test
for a hidden integrative component.** *Can they find `h` from a table? Yes. Can they apply the
energy balance given `h`? Yes. Can they do a problem needing both? Much less often — and the gap
is a nameable, teachable component.* → [our skill graph](../../research/domain/skill-graph-draft.md)

⚠ **And integrative KCs change the instruction:** *"For integrative knowledge, non-verbal forms of
instruction (e.g., example study, repeated practice) may not be optimal… Providing and eliciting
explanations may be critical to help learners break down or externalize the complex inference
needed when processing negative feedback."* **Practice does not fix an integration failure.
Explanation does.**

### ⭐⭐ Two operational ways to measure KC complexity — both runnable on our course

**1. Description length.** *"The more complex the description of the KC, the more complex is the
KC."* Their own worked count across three domains:

| KC type | Words to describe it |
|---|---|
| constant-constant | 9, 6, 6 |
| variable-constant | 11, 12, 10 |
| variable-variable | 12, 21, 21 |

**A free, immediate audit of our own skill graph: write each component as a complete
condition→response sentence and count the words.** Components that will not fit the pattern are
probably two components.

**2. ⭐⭐ Median correct-execution latency.** From learning curves in real tutoring systems:

| KC type | Example | Time to execute correctly |
|---|---|---|
| constant-constant | Chinese character → English word | **3–6 s** |
| variable-constant | *"if the referent was previously mentioned, use 'the'"* | **6–10 s** |
| variable-variable | *"if you need the area of a circle with radius R, compute 3.14 × R²"* | **10–14 s** |

**Latency separates KC types by a factor of two to three, and every step-based tutor logs it for
free.** That makes it an empirical check on a decomposition rather than an argument about one —
and it is the only method in this base that can tell us our grain is wrong *from data*.
⚠ *Their curves come from typed entry in a structured interface; a chat turn is not comparable, so
this is another reason [the solving surface has to be structured](vanlehn-2011.md).*

---

## Taxonomy 2 — kinds of learning process

Three, in the authors' own terms:

| Process | What it is | Verbal? |
|---|---|---|
| **A. Memory and fluency building** | *"strengthening memory and compiling knowledge, producing more automatic and composed ('chunked') knowledge"* — making the condition→response link direct, consistent, interference-resistant and fast | non-verbal |
| **B. Induction and refinement** | *"improve the accuracy of knowledge… perception, generalization, discrimination, classification, categorization, schema induction, and causal induction"* — modifying **which conditions** trigger a KC | non-verbal |
| **C. Understanding and sense-making** | *"explicit, verbally-mediated learning in which students attempt to understand or reason"* — comprehension, self-explanation, scientific discovery, deduction | **verbal** |

⚠ **B is where misconceptions come from, and they are usually invisible to the student.** Their
example: from diagrams where equal angles *look* equal, a geometry novice induces *"if angles look
equal, then they are equal."* **The rule produces correct answers and is wrong**, and *"this
induction may be done with little or no deliberate awareness."*

**In thermodynamics the analogue is immediate and it is on our own list:** a student who only ever
sees frictionless quasi-static examples induces *"processes are reversible unless told otherwise"*
— which is
[the failure every LLM makes too, in every run](../domain/thermo-problem-benchmark.md). **Both the
student and the model are doing over-generalized condition induction from unrepresentative
examples.** Fixing it is a *refinement* problem — add the missing discriminating feature — not an
explanation problem. → [AutoTutor's misconception catalogue](../systems/autotutor.md)

⭐ **And a warning about assessment that our design must absorb:** *"Non-verbal induction can lead
to a situation in which students can correctly perform mathematics… that they cannot explain."*
**Doing and explaining are different KCs.** A tutor that grades explanations is not measuring the
same thing as a tutor that grades derivations, and either can pass while the other fails.
→ [behavioral evaluation](../evaluation/behavioral-evaluation.md)

---

## ⭐⭐⭐ The mapping — Table 4, the practical payload

**Which learning processes are effective for which kinds of KC** (`++` most important, `+`
relevant, `-` not):

| Learning process ↓ / KC → | **Facts** (constant-constant) | **Rules** (variable-condition) | **Principles** (verbal + rationale) |
|---|---|---|---|
| **Understanding & sense making** | **−** *nothing to explain* | **−** *implicit rule learning is more efficient* | **++** *principles must be understood* |
| **Induction & refinement** | **−** *no generalization needed* | **++** *rules must be induced* | **+** *principles can be inert without associated rules* |
| **Memory & fluency building** | **++** *facts must be memorized* | **+** *rules (& instances) must be remembered* | **+** *principles must be remembered, but can be reconstructed* |

⭐ **The asymmetry hypothesis, which is the single most useful sentence for a tutor's policy:**

> *"Simple instructional principles are generally relevant, but **more complex principles are only
> relevant for the most complex kinds of knowledge.**"*

**Spacing, testing and optimized scheduling help everything. Self-explanation and argumentation
help only complex knowledge with a rationale — and on facts they are, in their word,
*wasted*.** *"To learn an arbitrary constant-constant association (a fact), a generalization
process like that implemented by category induction is unneeded… an explanation structure cannot
be used to generate or re-derive a KC."*

⚠ **Read that against a Socratic system prompt.** A tutor instructed to always elicit reasoning
will elicit reasoning about the saturation temperature of water at 2 MPa. **There is no reasoning
to elicit.** That is not a stylistic misstep; on this account it is time taken from learning.
→ [Socratic tutoring](socratic-tutoring.md), where students are already documented routing around
it; [bioTutor](../systems/biotutor-eth.md), whose student said *"for some questions I find this
somewhat unnecessary and would prefer to simply receive an answer."*

⭐ **And the stage of learning changes the answer too:** *"in learning of a rule, inductive
processes are critical for initial formation of the rule and refinement for improvement, but then
memory and fluency processes are important to improve retrieval reliability and application
speed."* **The same component needs different treatment at different points**, which is an
argument for [knowledge tracing](knowledge-tracing.md) that has nothing to do with problem
selection.

---

## Taxonomy 3 — the instructional principles, and where each belongs

Table 5, ordered simplest to most complex:

| Learning process | Principle | What it says | Source |
|---|---|---|---|
| **Memory & fluency** | **Spacing and Testing** | Retention improves with longer intervals between practice and when **active recall** is required | Cepeda et al. 2006 |
| | **Optimized Scheduling** | Choose practice instances from prior statistics **and this student's history with this KC** | Pavlik 2007 |
| | **Timely Feedback** | An evaluative response soon after an attempt at a task **or step** | Corbett & Anderson 2001 |
| **Induction & refinement** | ⭐ **Feature Focusing** | Instruction is more robust when it **directs attention to the valid or relevant features** of the target KC | Dunlap et al. 2011 |
| | **Worked Examples** | Interleaving worked-example study with problem solving beats all-problem-solving | Sweller & Cooper 1985 |
| **Understanding & sense-making** | **Prompted Self-Explanation** | Prompting students to explain steps to themselves beats not prompting **and beats providing the explanation** | Chi et al. 1994; Hausmann & VanLehn 2007 |
| | **Accountable Talk** | Talk moves holding students accountable to accurate knowledge, rigorous reasoning and the community | Michaels, O'Connor & Resnick 2008 |

⭐ **Feature focusing is the one we have no version of, and it is cheap.** Their example: Chinese
characters are compounds, and merely **highlighting the semantic radical as the mouse moves over
it** improved learning — *"a short instruction to focus on the semantic radical brings improvement
that is dramatic and immediate."*

**The thermodynamics analogue writes itself.** The features that discriminate a correct model
choice — *is the container rigid? is it insulated? is mass crossing the boundary? is the working
fluid near saturation?* — are exactly the ones students fail to encode, and
[exactly the ones every LLM fails to encode too](../domain/llm-thermodynamics-capability.md).
**Highlighting them in the problem statement, before any dialogue, is one line of interface and
it is a named principle with experimental support.**
→ [diagram reading](../domain/diagram-reading.md), where the features are on a T–s plot.

⭐ **Prompted self-explanation is stronger than it looks and it is the cheapest thing on the
list.** Aleven & Koedinger (2002) added self-explanation prompts to tutored practice **without
adding instructional time** and got greater explanation ability and conceptual transfer *while
maintaining* performance on isomorphic problems. And Hausmann & VanLehn found prompting
self-explanation in an **electricity** unit accelerated learning in a later **magnetism** unit —
transfer across topics. ⚠ A follow-up found **justification-based prompts** ("what principle
licenses this step?") beat **metacognitive prompts** ("how does this relate to what you know?").
**If we prompt, prompt for the justification.**

---

## ⭐ "Robust learning" — the outcome definition we should adopt

> *"Learning is **robust** when it lasts over time (**long-term retention**), **transfers** to new
> situations that differ from the learning situation along various dimensions, or **accelerates
> future learning** in new situations."*

**Three components, and our evaluation currently plans for at most one.**

| Component | Our current plan |
|---|---|
| Long-term retention | ⚠ nothing beyond end-of-semester |
| Transfer | [concept inventory, unassisted](../evaluation/concept-inventories.md) — planned |
| ⭐ **Accelerated future learning** | **nothing** |

⭐⭐ **The third is the interesting one and nobody in this base measures it.** Its operational form
is a *preparation-for-future-learning* test: teach unit A with the tutor, then measure how fast
students learn unit B **without** it. In thermodynamics the natural pair is right there in the
syllabus — **first-law energy balances, then second-law entropy balances** — and
[Hausmann & VanLehn ran exactly this design across electricity → magnetism](../systems/andes.md).

**It is also the outcome most immune to
[the proximal/distal collapse](vanlehn-2011.md)**, because the tutor is absent from the
measurement by construction.

⚠ **And KLI insists the denominator is time:** *"outcomes must not only last and transfer, but
also be achieved with **less time** or, at least, without extra time. **Too many theoretical
analyses and experimental studies do not address the time costs** of instructional methods…
Practically, use of more complex instructional strategies may not always be worth the extra time
they tend to require."* Their unit is **robust learning efficiency** — gain per instructional
minute. **[Kestin's result is stated in these terms](../evidence/kestin-2025-rct.md) — ~2× the
learning in less time — and almost nothing else here is.**

---

## ⚠ What this framework is not

The authors are unusually careful about their own status, and we should carry it:

> *"Many efforts at instructional 'theory' are really **frameworks**… because they do not lead
> directly to precise predictions."*

> *"The framework is **not a set of frozen taxonomies** but an interconnected set of theoretical
> and empirical propositions that imply hypothesis-testing experiments."*

**Tables 4 and 6 are hypotheses with partial experimental support, not measured effects.** Table 6
in particular is a *"possible correlation"* whose cells are `+` / `0` / blank, where blank means
**no relevant experiment exists** — and most of it is blank. The alignment-versus-asymmetry
question is explicitly unsettled.

⚠ **So do not cite Table 4 as though it were an effect-size table.** Cite it as the best available
map of which experiments have been run.

⚠ **And they name their own field's problem, which is ours:** *"careful cognitive task analysis of
domain knowledge is **not a standard research practice in any discipline**"*, with psychologists
valuing domain-general results, domain experts valuing new results in their domain, and
educational researchers valuing holistic explanations. **A defensible KC model for engineering
thermodynamics may be a contribution simply because nobody makes them.**

## What we should do with this

1. ⭐⭐ **Tag every component in [our skill graph](../../research/domain/skill-graph-draft.md) with
   the four distinctions** — constant/variable conditions, constant/variable response,
   verbal/non-verbal, rationale/convention. That is an afternoon's work on ~90 components, it
   requires no data, and **it converts a list into a decision table the tutor can act on.**
2. ⭐ **Then read the tutor's policy off Table 4.** Steam-table lookups and unit conversions are
   constant-constant: **spacing, retrieval practice, no dialogue.** Model selection and assumption
   identification are variable-condition: **feature focusing and worked examples, not
   explanation.** The laws and their applicability are principles with rationales: **argumentation
   and self-explanation, justification-flavoured.**
3. ⭐ **Run the two complexity tests.** Word-count every KC description now; log per-KC latency
   once anything is deployed. Either can show the grain is wrong.
4. ⭐ **Hunt integrative KCs with the `Pi = P(hard)/P(easy)` ratio** on paired problems. This is
   how a *hidden* component gets found, and our
   [cross-cutting skills](knowledge-components.md) are probably integrative KCs by another name.
5. **Add a preparation-for-future-learning measure** to the evaluation plan. First law → second
   law is the natural pair.
6. **Report gain per instructional minute**, not just gain.

## Open questions

- [ ] **Does DataShop hold a KC model for engineering thermodynamics?** KLI is the PSLC's
      framework and DataShop is the PSLC's repository; if a model exists anywhere it is there.
      Still unchecked. → [knowledge components](knowledge-components.md)
- [ ] **Are our cross-cutting skills integrative KCs?** `assumption-identification` and
      `model-selection` look exactly like components that are invisible in single tasks and only
      appear in the gap between paired problems. **Testable with the subtraction logic.**
- [ ] **Which of our ~90 components have rationales and which are conventions?** Nobody has asked,
      and the answer changes what the tutor is allowed to do on each one.
- [ ] Aleven & Koedinger (2002) on self-explanation in a Cognitive Tutor, and Hausmann & VanLehn
      (2007) on cross-topic transfer — **both are cited here as the evidence for the cheapest
      intervention on the list, and we hold neither.**
- [ ] Salden et al. (2008) — adaptive fading of worked examples, individualised **per KC**. KLI's
      own worked demonstration that KC-level individualisation beats non-individualised
      instruction. Not held.
- [ ] Is the asymmetry hypothesis right? It is the framework's most useful claim and its least
      tested.

## Connects to

- [Knowledge components](knowledge-components.md) — the grain problem, which this gives a vocabulary for
- [VanLehn 2011](vanlehn-2011.md) — the other half: the student must generate the solution; KLI says what the solution is made of
- [Cognitive Tutor](../systems/cognitive-tutor.md) — Koedinger and Corbett's own system, and the 1995 paper this descends from
- [Knowledge tracing](knowledge-tracing.md) — estimates mastery per KC; KLI says which KCs even need it
- [Productive failure](productive-failure.md) — a desirable-difficulties intervention that should say which KC type it targets
- [Spaced repetition](spaced-repetition.md) — the memory-and-fluency column, in full
- [Socratic tutoring](socratic-tutoring.md) — only licensed for KCs with a rationale
- [Our skill graph draft](../../research/domain/skill-graph-draft.md) — the ~90 components to tag
- [Thermo problem benchmark](../domain/thermo-problem-benchmark.md) — the reversibility over-generalisation, as a condition-induction failure
- [Concept inventories](../evaluation/concept-inventories.md) — transfer, one of robust learning's three legs

## Sources

- [Koedinger, Corbett & Perfetti (2012), "The Knowledge-Learning-Instruction (KLI) Framework: Bridging the Science-Practice Chasm to Enhance Robust Student Learning," *Cognitive Science* 36(5), 757–798](https://doi.org/10.1111/j.1551-6709.2012.01245.x) `[read — full text, 35 pp., 2026-09-03]` — authors' final version. Local: `course-materials/papers/koedinger-2012-kli-framework.pdf`
- [LearnLab / PSLC background readings](https://learnlab.org/index.php/background-readings) `[found]` — where this and the rest of the PSLC corpus live
- Anderson, Corbett, Koedinger & Pelletier (1995), "Cognitive tutors: Lessons learned," *Journal of the Learning Sciences* 4, 167–207. `[found]` — the same group's earlier paper, and [the origin of the completion mechanism](vanlehn-2011.md)
</content>
