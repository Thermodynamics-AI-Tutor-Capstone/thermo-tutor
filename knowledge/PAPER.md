# The State of the Art in AI Tutoring for College Courses

**A survey for the Penn State AI Thermodynamics Tutor capstone**
*Compiled August 2026 · Revised 31 August 2026 after full reads · Entry point to the [knowledge brain](README.md)*

---

## How to read this

Every claim below links to a node with the primary sources behind it. Follow the links
when you want depth; the paper itself is the argument, not the archive.

Verification status is marked honestly throughout, source by source: `[read]` means someone
read the full text, `[skimmed]` means abstract or summary only, `[found]` means we know it exists
and have not opened it. As of **31 Aug 2026** the base carries **≈110 `[read]`, 73 `[skimmed]`,
72 `[found]`**, and those full reads have produced **more than twenty factual corrections**, some
of them to claims this paper previously made — flagged inline with ⚠ and tabulated in
[the correction log](README.md). **Check the node before citing anything.**

The corrections are not cosmetic. Among them: Stan is a resource pointer, not a **Socratic**
tutor *(Socratic = leading a student to the answer by asking, rather than telling)*;
the widely-quoted Maizey grade claim has no locatable study; the diagram "wall" is model-specific
(6%–76%), not a property of LLMs; voluntary AI-tutor users skew *least*-prepared, not
already-advantaged; Andes removed the Bayesian network it is famous for; and CycleTalk's
"negotiation dialogue" was never actually built.

---

## Executive summary

If you read nothing else:

1. **The subject-matter problem is solved. The teaching problem is not.** OpenAI's o3,
   **zero-shot** *(asked cold — no examples, no training on the exam)*, outscored **all 90
   students** on a real German engineering thermodynamics exam
   — diagrams included — where the student failure rate was 58% and exactly one student
   earned an A ([superstudent](domain/superstudent-thermodynamics.md)). In the same period,
   a purpose-built benchmark found **no** 2025-era model clears a 95% reliability bar for
   unsupervised thermodynamics tutoring ([UTQA](domain/utqa.md)). Both are true. §VI
   explains why.

   ⚠ *Correction: this paper previously said o3 "solved every problem correctly." The
   study's own body reports it lost points on graphical representations and made one major
   error. It won because the students did worse.*

2. **The pre-LLM field already set a high bar, and the LLM era has mostly not cleared
   it.** Step-based **intelligent tutoring systems** achieved **d = 0.76** against no
   tutoring; human tutors achieved **d = 0.79** ([VanLehn 2011](concepts/vanlehn-2011.md)).
   Systems from the 1990s and 2000s — [Andes](systems/andes.md),
   [Cognitive Tutor](systems/cognitive-tutor.md), [ALEKS](systems/aleks.md) — are the
   incumbents, not ChatGPT.

   *(**d** = Cohen's d: the gap between two groups in standard deviations. 0.2 small, 0.5 medium,
   0.8 large. d = 0.76 moves a median student to about the 78th percentile. **Every effect size
   here is in these units.** An **ITS** is the pre-LLM kind of tutor: hand-built rules plus a model
   of what the student knows. **Step-based** = it reacts to each step of your derivation, not just
   your final answer. Hold onto 0.76 vs 0.79 — **1990s software came within a rounding error of a
   human tutor.**)*

3. **The single best result for LLM tutoring is real, well-run, and explicitly does not
   claim our case.** A Harvard crossover RCT (n = 194) found **0.73–1.3 SD** greater learning
   than an excellent active-learning classroom, in **less time** (median 49 min vs. 60), with
   higher engagement ([Kestin et al. 2025](evidence/kestin-2025-rct.md)). Its
   generalizability case is stronger than usually credited — the effect held for students
   both below and above 40% on the FCI (p < 0.001 each).

   *(**RCT** = randomized controlled trial; assignment by chance, which is what buys the causal
   claim. **Crossover** = everyone gets both conditions, so each student is their own control.
   **n** = participants. **SD** = standard deviation, same unit as d. **Median** = middle value,
   used when outliers would skew the average. **FCI** = Force Concept Inventory, the standard
   validated physics concept test — we'd want a thermo equivalent, see
   [concept inventories](evaluation/concept-inventories.md). **p** = odds of a result this big if
   the treatment did nothing; <0.05 conventional, <0.001 strong. **p says an effect is real, d
   says it's big** — don't confuse them.)*

   ⚠ **But its lessons targeted Bloom's understanding/applying/analyzing levels** *(Bloom's
   taxonomy ranks thinking from remembering at the bottom through applying and analyzing to
   evaluating and creating at the top)*, which the
   authors describe as *"particularly well suited for current generative AI tutors"* — and
   they explicitly decline to claim contexts *"requiring complex synthesis of multiple
   concepts and higher-order critical thinking."* **Engineering thermodynamics is that
   excluded category.** Expect less than 2×.

4. **The single most important negative result is also real, and larger.** In a
   ~1,000-student RCT, students given an unguarded GPT-4 interface did **48% better
   during practice and 17% worse on the unassisted exam** than controls. Students given a
   **guardrailed** tutor version *(guardrails = enforced limits stopping it handing over
   answers)* did 127% better during practice and **scored the same as controls** on the exam
   ([Bastani et al., PNAS 2025](evidence/bastani-2025-harm.md)).
   Read that again: the best-designed arm's effect on actual learning was *zero*.

   Two details the coverage omits. **GPT-4 was correct only 51% of the time** on those
   problems (42% logical errors, 8% arithmetic). And **students did not perceive any
   reduction in their own learning** — self-report is worthless as an outcome here.

5. **The honest state of the art is "no proven harm," not "proven benefit."** Outside a
   handful of expertly hand-built single-course deployments, nobody has demonstrated a
   robust positive learning effect from a chatbot tutor at scale. Guardrails are
   currently doing damage control, not producing gains.

6. **The field's real failure mode is engagement, not quality — and the spread is enormous.**
   Khanmigo (two-year **cluster** RCT — *randomized by whole school or classroom rather than by
   student, since you can't give half a class a different teacher*; 18 schools): the median
   student engaged it in **17% of
   exercise sessions in which they made a mistake**, and the AI added **no** detectable
   learning over the platform alone. KAIST: **50% of 477 students never used it once**; 1.3%
   generated 30% of traffic. CS50: **only 3% never used it.** The difference is design and
   policy, not luck — see §V.

   ⚠ *Correction: this paper previously claimed voluntary-tool power users "skew
   already-high-performing and higher-income." At university level the best data says the
   opposite: at KAIST, students with **no prior coding experience averaged 62.2
   interactions** against **4.5** for advanced students, and 58% of students said they had
   previously avoided asking a human out of embarrassment.
   → [equity](practice/equity.md), [KAIST](evidence/kaist-vta-2025.md)*

   **And the scaffolding goes unused, across twenty years and two technologies**
   *(scaffolding = temporary support — hints, prompts, partial structure — meant to be withdrawn
   as the student gets it).*
   [PeteChat](systems/petechat-purdue.md) coded 284 messages from a live Purdue engineering
   course and found **hint utilisation at 0.0%** — not low, zero — with self-reflection at 1.4%.
   [CycleTalk](systems/cyclepad-cycletalk.md) in 2006 found **help requests on 14% of
   problem-solving actions**, which is why attaching dialogue to *success* events beat attaching
   it to hint requests. **A pull-based tutor is designing for a behaviour nobody has ever
   observed.** Proactivity is not a feature; it is the precondition.

7. ⭐ **The Socratic stance has a measured cost, and it lands on engagement.** In the largest
   expert evaluation in this literature — **186 pedagogy experts role-playing learners, 248 more
   rating, 2,360 conversations, 10,192 assessments** — LearnLM was preferred overall and ranked
   first in every rubric category. But among the reasons experts gave for preferring a
   *competitor*, the largest theme (**36.3%**) was **conversation style: LearnLM was described as
   "patronizing," rivals as "warmer,"** and participants rated it below GPT-4o on *"stimulating
   their interest"* and *"perceived warmth."* **A model tuned to guide rather than tell is
   experienced as condescending — by raters predisposed to approve of guiding.** Warmth and
   concision are in measured tension with the pedagogy, not decorations to add afterwards.
   → [LearnLM](systems/learnlm.md)

8. **Students route around Socratic design.** In 2,874 coded student turns with a
   Socratic AI physics tutor, "what do I do next" was the **second-most-common move**
   (4.4% of all turns), and the top 20 discourse categories contained essentially no
   conceptual reasoning ([Socratic subversion](concepts/socratic-tutoring.md)).

9. **Every serious system independently converged on the same architecture:** a
   constrained, retrieval-grounded, externally-verified LLM wrapped in deterministic
   policy — with the pedagogy in code, not in the prompt. §V lays out the seven layers.

   **And we now have the number proving why the prompt isn't enough.** Across **10 million
   messages**, CS50's Duck — the reference implementation of "won't spoil the answer" —
   produced code blocks in **22% of responses and 48% of conversations**. Upgrading GPT-4 →
   GPT-4o pushed conversation-level leakage from 44% to **56%**. A system prompt is not a
   guardrail, and guardrail behaviour is not stable across model versions.

10. **Grounding + verification is what separates working systems from demos.**
   [Jill Watson](systems/jill-watson.md), restricting outputs to validated course
   material and verifying each response by **textual entailment** *(an automatic check that the
   answer really is supported by the source text, not merely plausible)*, passes **76.7%** of
   150 course questions with **5.7%** harmful errors. OpenAI's own Assistant on the same task:
   **31.3%** correct, **16.5%** harmful. Same model underneath — the difference is entirely
   grounding and verification.

11. **Cost is not the constraint.** KAIST ran a 14-week tutor for **477 students on $180
    total** — **$0.38 per student** ([cost](practice/cost-economics.md)). The constraints are
    pedagogy, engagement, compliance, and faculty trust.

12. **No LLM can reliably tell a wrong step from a right one.** Across 223 tutoring domains,
    **no model exceeded chance at labeling incorrect student actions**, and models best at
    confirming correct work were worst at catching errors ([TutorGym](evaluation/tutorgym.md)).
    Diagnosis is the atomic act of tutoring, and it is the thing that must be handled outside
    the model.

13. **The thermodynamics diagram gap is large but model-specific.** Mean accuracy on
    diagram items is **32%** against **67%** text-only — but the range across 19 models runs
    from **6%** (gpt-4.1, *below* the 25% chance baseline) to **76%** (gpt-o3)
    ([diagram reading](domain/diagram-reading.md)).

    ⚠ *Correction: this paper previously framed 32% as a uniform "wall." It isn't. Reasoning
    models substantially clear it, and o3 handled a real exam's diagrams. Model choice is
    load-bearing here in a way it is nowhere else in the architecture.*

14. **The benchmark we were going to build already exists.** [ThermoQA](domain/thermoqa.md)
    (293 open-ended problems, three tiers, **CoolProp** ground truth *(the open-source property
    library — the software steam table)*, six frontier models) and
    [UTQA](domain/utqa.md) (50 items, 19 models, **dataset public on HuggingFace**) both
    landed before us. This changes our contribution story — see §VIII.

15. ⚠ **Stan is not the competitor we thought.** Read in full, the Delaware thermodynamics
    assistant targets **Levels 1–2 of its own six-level scale** — "resource pointer" and
    "content summarizer." Tutoring, guided problem solving, and Socratic dialogue are
    explicitly *out of scope*, it has **no property tools, no student model, no LMS
    integration, and no evaluation of any kind.** Its real contribution is instructor-facing
    lecture analytics. → [Stan](systems/stan-udel.md)

16. ⚠ **The obvious success metric will train the tutor to cheat.** Across 10,235 submissions,
    feedback that **revealed the answer** — which the pedagogical rubric marks undesired —
    produced *higher* immediate success than feedback that withheld it (**79.4% vs 53.0%**),
    because students copy. [Bastani](evidence/bastani-2025-harm.md) found the same reversal at
    semester scale (**+48% assisted, −17% unassisted**), and
    [CS50](systems/cs50-duck.md) found that **48% of conversations contain generated code against
    an explicit instruction not to generate any** — a rate that got *worse* when they upgraded
    GPT-4 → GPT-4o. Three scales, one pattern: **optimise for immediate success and the metric
    will applaud you all the way down.**
    → [behavioral evaluation](evaluation/behavioral-evaluation.md),
    [assessment integrity](practice/assessment-integrity.md)

17. ⭐ **Our exact experiment was run in 2006, and the missing piece is the piece we have.**
    [CyclePad](systems/cyclepad-cycletalk.md) — an articulate thermodynamic-cycle simulator that
    explains every derived value from its assumption chain — has been in the **US Naval Academy
    curriculum since 1996**. CMU bolted **tutorial dialogue** onto it and measured a **0.25 SD**
    gain over the simulator alone (F(1,86) = 5.57, p < .05, USNA — *an **F-test** from an
    **ANOVA**: signal over noise, bigger is stronger; the bracketed pair is degrees of freedom*).
    Gains appeared on conceptual
    tests and **not** on the open-ended design exercises; **students requested help on only 14%
    of actions**, so the winning manipulation was firing dialogue *proactively on success* rather
    than waiting to be asked. The authors' own diagnosis of what their agents could not do:
    they *"played more of a role of eliciting reflection… rather than assisting with navigation."*
    The reason is architectural: **the dialogue agent never queried the simulator.** It traced
    student actions against a pre-authored graph and never read the cycle state, so it could not
    reason about the design in front of it. **Joining a physics engine that explains itself to an
    agent that can converse is the specific thing 2006 left unbuilt.** ⚠ Cite as suggestive, not
    established — the raw gains favour the control and the vaunted "negotiation dialogue" was
    never implemented. → [CyclePad / CycleTalk](systems/cyclepad-cycletalk.md)

---

## I. Prehistory: what the field already proved (1970–2015)

The LLM era did not invent tutoring systems. It inherited a fifty-year research program
that had already answered several of the questions people are currently re-asking.

### Bloom's 2 sigma, and why it was wrong

*(**Sigma** (σ) = standard deviation. "2 sigma" is d = 2.0. Old literature says sigma, new says d.)*

Benjamin Bloom's 1984 claim — that one-to-one tutoring moves the average student two
standard deviations, to the 98th percentile of conventionally-taught students — is the
foundational myth of the field. It is quoted in nearly every AI-tutoring pitch deck,
including, implicitly, our own project brief.

It does not replicate. Kurt VanLehn's 2011 review of experiments from 1975–2010 found
**human tutoring at d = 0.79**, not 2.0 ([Bloom's 2 sigma](concepts/blooms-two-sigma.md),
[VanLehn 2011](concepts/vanlehn-2011.md)).

That correction matters for us in a specific way: **the ceiling we're aiming at is lower
than the marketing suggests, and it was nearly reached by 1990s software.**

### The step-based finding

VanLehn's more useful contribution was a taxonomy by *interaction granularity*:

| Granularity | What the student enters | Effect size vs. no tutoring |
|---|---|---|
| Answer-based | Final answer only | ~0.3 |
| **Step-based** | **Each step of a derivation** | **d = 0.76** |
| Substep-based | Sub-steps within each step | d = 0.40 |

Human tutoring beat step-based tutoring by only **d = 0.21**.

Two implications, both uncomfortable for a chatbot:

- **Granularity of interaction predicts learning better than intelligence of feedback.**
  Getting students to externalize each step mattered more than how clever the response
  was.
- A conversational interface is *not obviously* step-based. A student who types "I'm
  stuck on 4b" and reads a paragraph is doing answer-based tutoring with extra words. The
  interface design question is a learning question. See
  [knowledge components](concepts/knowledge-components.md).

### The systems that got there first

- **[Andes](systems/andes.md)** (Pittsburgh + US Naval Academy, ONR-funded) — physics.
  Students entered whole derivations: vectors, coordinate systems, variable definitions,
  equations, with feedback after each step. Bayesian networks for decision-making. Five
  years of Naval Academy evaluation showed significant learning improvement. **The
  closest historical analogue to what we're building**, and it replaced pencil and paper
  rather than the textbook or the lecture.
- **[AutoTutor](systems/autotutor.md)** (Memphis, Graesser) — natural-language dialogue
  tutoring built on *expectation and misconception-tailored* (EMT) dialogue, derived from
  ~100 videotaped human tutoring sessions. It anticipated correct answers and specific
  wrong ones, and matched student utterances against both. **This is the design pattern
  our misconception catalogue should follow.**
- **[Cognitive Tutor](systems/cognitive-tutor.md)** (CMU, Anderson & Koedinger) — ACT-R
  cognitive models, **model tracing**, [**knowledge tracing**](concepts/knowledge-tracing.md).
  *(Model tracing = following your steps against an expert model to see where you diverged.
  Knowledge tracing = keeping a running estimate of what you've mastered.)*
  A RAND trial found students gained nearly a full extra year of algebra.
- **[ALEKS](systems/aleks.md)** (UC Irvine, Falmagne, 1996; McGraw Hill 2013) — knowledge
  space theory. Assesses a student's precise knowledge state in 20–25 questions by
  searching a combinatorial space of possible states. Thirty years of continuous
  refinement, now sitting inside the publisher platform your students already use.
- **[ASSISTments](systems/assistments.md)** (WPI, Heffernan) — free, 1M+ students, and
  unusually well-evidenced: an SRI study found higher standardized scores; a Maine study
  found nearly a year of additional gains for 7th graders.
- **[Betty's Brain](systems/bettys-brain.md)** (Vanderbilt, Biswas) — learning by
  teaching. Students teach an agent, then watch it fail. A design idea almost entirely
  absent from LLM tutors, and arguably the most under-exploited one.

**What to take from this section:** if our tutor cannot beat a well-built step-based ITS,
it is not an advance. And the incumbent in a thermodynamics course is not ChatGPT — it's
[Mastering Engineering, Connect, or WileyPLUS](practice/incumbent-platforms.md), which
descend directly from this lineage.

---

## II. The first AI teaching assistant (2016–2022)

### Jill Watson

In spring 2016, Ashok Goel's *CS7637: Knowledge-Based AI* in Georgia Tech's online MS in
CS deployed a virtual teaching assistant named **Jill Watson** into the class discussion
forum. It was built on IBM Watson, trained on roughly **40,000 forum postings** from
prior terms, and gated behind a high answer-confidence threshold so it only spoke when
nearly certain.

Students did not know. When Goel revealed it at the end of term, the reaction — surprise,
delight, and some unease — became the story that put AI teaching assistants on the map.
Full history: [Jill Watson](systems/jill-watson.md).

**Three things Jill Watson established that still hold:**

1. **The bottleneck was never content, it was presence.** 300 students posting 10,000
   messages overwhelmed a professor and eight human TAs. The value delivered was
   *responsiveness*, not novel explanation. Later work found Jill Watson improved
   **teaching presence** and correlated with better academic performance — believed to be
   the first documented case of a chatbot doing so for adult online learners.
2. **Confidence gating is a feature.** Answering only when sure, and escalating
   otherwise, is a design decision the LLM era largely abandoned and is now rediscovering
   as "guardrails."
3. **The reveal is an ethics question we still haven't settled.** See
   [disclosure](practice/disclosure-and-ethics.md).

### The 2024 rebuild, and the most useful comparison in the field

DILab rebuilt Jill Watson on top of ChatGPT — but *restricting outputs to validated course
material and verifying each response using textual entailment*. Head-to-head against
OpenAI's own Assistant on the same courses (Taneja et al. 2024):

| Metric | Jill Watson | OpenAI Assistant | Legacy (2016) Jill Watson |
|---|---|---|---|
| Pass, 150 course questions | **76.7%** | 31.3% | **26.0%** |
| Harmful failures | **5.7%** | 16.5% | — |
| Confusing failures | 62.8% | 72.8% | — |
| Retrieval failures | 57.1% | 68.0% | — |

This is the cleanest available evidence that **architecture beats model.** Same
underlying LLM. 2.5× the pass rate, about a third the harmful errors. The difference is
grounding and verification — see
[grounding and verification](concepts/grounding-and-verification.md).

Note the third column. The **legacy** knowledge-based Jill Watson — the famous 2016 system
students could not distinguish from a human TA — passes **26.0%**, below an off-the-shelf
assistant. **Being indistinguishable from a TA and being correct were never the same
achievement.**

**If you take one design lesson from this entire paper, take that table.**

---

## III. The LLM explosion (2023–2026)

By 2026, roughly **74% of US institutions have at least one production AI deployment
touching students directly** ([institutional landscape](practice/institutional-landscape.md)).
The interesting deployments cluster into four patterns.

### Pattern 1 — The course-embedded tutor

**[CS50 Duck](systems/cs50-duck.md)** (Harvard, David Malan) is the largest and most
studied. A rubber-duck debugger that "only answers questions as a good tutor might,
without spoiling answers outright," explicitly aligned with CS50's academic honesty
policy. Scale: **201k students and teachers, ~35k prompts/day, 9.4M prompts**, and
**800,000+ questions in the 2024–25 academic year alone**. 88% of users rate it always or
frequently helpful. Published at SIGCSE 2024 and 2025 — including a human-feedback
evaluation using 29 teaching fellows and 1,309 pairwise comparisons.

**[PeteChat](systems/petechat-purdue.md)** (Purdue, ECE 20875) is the closest
methodological sibling to our project: a course-specific tutor built by fine-tuning
open-source LLMs on course data, deployed Spring 2025, explicitly framed as *"Tutor, Not
Solver."* It scaled to additional Python courses in Spring 2026.

**[Stan](systems/stan-udel.md)** (Delaware, CHEG231 thermodynamics, Fall 2025) is the
closest *domain* sibling — Whisper large-v3 transcription of 39 lectures, Llama 3.1 8B via
Ollama, retrieval over the textbook's own back-of-book index rather than embeddings. ⚠ It is
**not** a Socratic tutor: it deliberately stops at Levels 1–2 (point to the page, summarize
the lecture), and its actual thesis is that **instructor-facing** lecture analytics — question
mining, confusion detection — are the neglected opportunity. It reports no outcome data. Its
failure-mode taxonomy for local structured extraction is excellent and worth reading.

### Pattern 2 — The institutional platform

**[Cogniti](systems/cogniti-sydney.md)** (Sydney, Danny Liu) — the "AI stunt double for
teachers." Instructors build their own agents with their own instructions and materials,
embedded in the LMS. Won the AFR 2025 AI Award; now on Microsoft's Azure Marketplace and
used from chemical engineering to musicology. The important design commitment: **teachers
stay in control of the agent**, rather than IT shipping one tutor for everyone.

**[U-M Maizey](systems/umich-maizey.md)** (Michigan) — university-built, closed
generative AI. **3,500+ Maizey instances in production; ~15,000 users/day.** In a
1,000-student class, students who used Maizey saw grades improve **5–9%**, and the tutor
answered questions **94% as effectively as or better than** the course teaching staff.
Integrates into a Canvas side panel. This is the most directly relevant institutional
model for us, and the grade result is the strongest institutional-scale number in this
paper — with the caveat that **usage was self-selected**, so it is correlational.

*(**Correlational** = the two things moved together, but the students who opt in may already
differ. **No sample size fixes this** — only randomization does.)*

**[ASU + OpenAI](systems/asu-openai.md)** — first university OpenAI partnership (Jan
2024); by Oct 2025, ChatGPT Edu with GPT-5 free to every student and staff member; 500+
projects.

**Penn State** has its own version of this, and it changes our project's feasibility
picture materially — see §VIII and
[PSU AI landscape](practice/psu-ai-landscape.md).

### Pattern 3 — The pedagogically fine-tuned model

**[LearnLM](systems/learnlm.md)** (Google DeepMind) is the only serious attempt to move
pedagogy *into the weights* rather than the prompt. Expert raters preferred it over
GPT-4o by **+31%**, Claude 3.5 Sonnet by **+11%**, and its own Gemini 1.5 Pro base by
**+13%**. In a follow-up "arena for learning" with 189 educator role-players and 206
expert judges, Gemini 2.5 Pro was preferred in **73.2%** of matchups.

Also: students who received short LearnLM tutoring sessions were **5.5 percentage points**
more likely to solve novel problems afterward than students working with human tutors
alone. That is a real, positive, published learning effect — and it is small.

*(A **percentage point** is the raw gap between two percentages: 62% → 66% is 4 points, but only
a ~6% relative gain. Press releases blur these in the flattering direction.)*

### Pattern 4 — Human-AI hybrid

**[Tutor CoPilot](systems/tutor-copilot.md)** (Stanford, EduNLP Lab) inverts the frame:
the AI coaches the *tutor*, not the student. RCT with ~900 tutors and ~1,800 students.
Students of tutors using it were **4 percentage points** more likely to master topics —
and **9%** more for students of the *least-skilled* tutors. Tutors using it asked more
guiding questions and gave away fewer answers.

**The most interesting result in the paper for a resource-constrained team:** the highest
measured return came from using AI to raise the floor on human instruction, not from
replacing it. Open source, and embeddable in any tutoring platform.

---

## IV. What the evidence actually says

Here is where the field's public story and its empirical record come apart.

### The positive case

- **[Kestin et al. 2025](evidence/kestin-2025-rct.md)** — Harvard PS2, n = 194, RCT,
  within-subject alternating design. **~2× the learning gains** of an active-learning
  classroom, less time on task, higher engagement and motivation. Published in
  *Scientific Reports*. This is the field's best result, and it beat an already-strong
  comparison condition rather than a lecture.
- **[U-M Maizey](systems/umich-maizey.md)** — 5–9% grade improvement in a 1,000-student
  class. Correlational.
- **[Tutor CoPilot](systems/tutor-copilot.md)** — +4pp overall, +9% for students of weak
  tutors. RCT, ~1,800 students.
- **[LearnLM](systems/learnlm.md)** — +5.5pp on novel problems over human tutoring alone.

### The negative case

- **[Bastani et al., PNAS 2025](evidence/bastani-2025-harm.md)** — ~1,000 Turkish high
  school math students, three arms:

  | Arm | During AI-assisted practice | On the later unassisted exam |
  |---|---|---|
  | GPT Base (unguarded) | **+48%** vs. control | **−17%** vs. control |
  | GPT Tutor (guardrailed) | **+127%** vs. control | **≈ same** as control |
  | Control | baseline | baseline |

  Unguarded generative AI made students dramatically better while using it and
  measurably *worse* without it. Students used it as a crutch. Guardrails eliminated the
  harm — **and produced no learning benefit.**

- **[Oreopoulos & Low 2026](evidence/khanmigo-engagement-2026.md)** — a **two-year cluster
  RCT** across 18 Tennessee middle schools, and the most important **null result** in the field
  — *a **null result** is a good study that found nothing. That's evidence, not failure, and
  since nulls rarely get published the ones that do deserve extra weight.*
  Khan Academy raised achievement 0.06–0.08 SD over a school year, but those gains
  *"resemble those from Khan Academy practice without AI assistance."* **The AI tutor added
  nothing detectable.** Why: 96% tried it, but the median student engaged it in only **17% of
  exercise sessions in which they made a mistake**, and the messages were *"mostly bare
  answers or clicks on suggested prompts."* Their conclusion: *"The binding constraint appears
  to be engagement: realizing the promise of AI tutoring will require getting students to use
  it, not just giving them access."*

- **[Equity](practice/equity.md)** — roughly **5%** of students account for most benefit
  from voluntary digital learning tools, and that 5% is disproportionately already-high-
  performing and higher-income. A voluntary tutor can widen the gap it was built to close.

- **[Faculty sentiment](practice/faculty-adoption.md)** — 73% of faculty have personally
  handled AI-related integrity issues; 83% predict AI will shorten student attention
  spans; US/Canada faculty intent to use AI *fell* from 76% (2025) to 67% (2026). We are
  building into a headwind.

### How to reconcile them

The contradiction dissolves under three observations:

1. **Guardrails prevent harm; they don't create learning.** Bastani's guardrailed arm was
   neutral. Every deployed tutor's "don't give the answer" system prompt is doing damage
   control. That is worth doing, and it is not a win.

2. **Positive results come from expert hand-crafted scaffolds in a single course.**
   Kestin's tutor was built by a physics-education researcher with expert-authored
   scaffolds for specific problems. **So were Bastani's guardrails** — read in full, "GPT
   Tutor" meant a prompt containing *the correct solution to that specific problem* plus
   *teacher-authored common mistakes with matched hints*, per problem, which the authors
   call "labor-intensive." That is [AutoTutor's EMT structure](systems/autotutor.md) rebuilt
   by hand.

   So hand-authoring is necessary and not sufficient: both studies did it, one got 2× and one
   got zero. The residual differences are **dose and integration** — Kestin's tutor *was* the
   course activity for half a semester; Bastani's was four sessions bolted on, covering 15%
   of the curriculum. Nobody has run the experiment that isolates which factor carries the
   effect. **The unit of success in this literature is the course, not the model.**

3. **Measured effects shrink as sample size and setting realism grow.** Kestin: n=194,
   one course, ~2×. Tutor CoPilot: n=1,800, +4pp. Khanmigo: statewide, engagement
   collapse. This is the standard shape of an education-technology literature, and we
   should expect our own numbers to land at the small end.

**The state of the art, stated honestly: guardrailed LLM tutors are safe, popular,
cheap, and not yet demonstrably better than what students already had — except in
individual courses where a domain expert did a great deal of hand work.**

That's not a reason not to build one. It's the reason the hand work is the project.

---

## V. The convergent architecture

Independently — Georgia Tech, Harvard, Purdue, Delaware, Khan Academy, Sydney — serious
systems arrived at the same seven layers. Where they differ is mostly which layers they
skipped.

### 0. The thing that doesn't work: pedagogy in the system prompt
Stated first because almost every deployed tutor stops here. CS50 measured its own leakage
across 10M messages at **22% of responses / 48% of conversations**, worsening to 56% after a
model upgrade — *"instruction dilution"* *(the more you cram into a system prompt, the less of
it the model actually obeys)*. **Few-shot** examples *(worked examples pasted into the prompt)*
make it worse, not better, because they inflate the prompt. Their working fix was
**fine-tuning** *(retraining the model's weights on your examples, rather than instructing it at
run time)* **on 50 curated conversations** — a capstone-sized dataset.

⚠ **State this precisely, because the obvious reading is too strong.** Prompts are not useless.
In Google's learning arena, **ChatGPT-4o ranked 2nd on pedagogical quality and GPT-4o ranked
5th — the same model**, separated only by OpenAI's product wrapper
([arena](systems/learnlm.md)). A prompt layer moved one model from last to second.

So the honest formulation is: **a system prompt reliably shifts the average and cannot hold the
floor.** CS50's 22% leakage is a floor failure; the arena's ranking jump is an average shift.
Tutoring is a worst-case discipline — one answer handed over is one assignment compromised — so
the floor is what we are buying, and that is why the prompt cannot be the last line of defence.
It is still worth writing well.
→ [guardrails](concepts/guardrails.md), [CS50 Duck](systems/cs50-duck.md)

### 1. Retrieval grounding
Restrict the model to validated course material — usually **RAG**, *retrieval-augmented
generation: look the passage up first, then answer only from it*. Everyone does this. It is
necessary and nowhere near sufficient — **57.1% of Jill Watson's remaining errors are still
retrieval failures**, in the best-engineered system of its kind.
→ [RAG in education](concepts/rag-in-education.md)

### 2. External verification
Check the output before the student sees it. Jill Watson uses textual entailment. Khan
Academy built a **separate math agent** that verifies every calculation, after finding
that generative AI "generates a probable next number rather than executing a correct
calculation," and tracks math error rate as a guardrail metric.
→ [grounding and verification](concepts/grounding-and-verification.md)

### 3. Tool calls for ground truth
Anything the model is bad at should not be done by the model. For thermodynamics that
means property data from CoolProp/Cantera/IAPWS, symbolic work from a CAS, and unit
checking — never from weights.
→ [property data tools](domain/property-data-tools.md)

### 4. A pedagogical policy outside the prompt
The weakest layer in almost every deployed system, and the one the evidence says matters
most. "Be Socratic" in a system prompt is defeated by a student typing "just give me the
answer." What's needed is graduated hint levels with a productive-failure budget,
selected by deterministic code with access to the student's attempt history.

**One system has shipped a version of this at scale.** CS50's **"hearts"** throttle gives
each student 10 interactions, regenerating one every three minutes — explicitly framed as
pedagogy, not just cost control: it "encourages students to carefully consider their
questions" and "foster[s] independent problem-solving skills." Students asked for it to be
relaxed; the team declined. That is a productive-failure budget implemented as a rate limit,
running across 200,000 users. → [CS50 Duck](systems/cs50-duck.md)

And a correction to the intuition that guardrails repel students: **they don't.** Bastani's
guardrailed arm got *more* messages per problem than the unguarded one, the gap widened over
four sessions, and superficial "just give me the answer" openers fell from 42% to 37% while
*rising* from 56% to 67% in the unguarded arm.

**Three design constraints follow from the productive-failure literature** *(**productive
failure** = letting students attempt a problem and fail *before* teaching them the method, on the
theory that the struggle prepares them to absorb it)* (Sinha & Kapur, 166 comparisons, **Hedge's
g = 0.36 [0.20, 0.51]**), and all three are easy to get wrong.

*(**Hedge's g** = Cohen's d corrected for small-sample bias; read it the same way. The brackets
are the **95% confidence interval**, the range the true effect plausibly sits in. It **excludes
zero**, so the effect is real; its **width** tells you how precisely — which the headline number
alone hides.)*

1. **The ladder must terminate in an explicit contrast against the canonical solution**, not in
   refusal. "Instruction building on student solutions" is the **#1 ranked** of seven fidelity
   criteria (g = 0.56 vs 0.20, p = .02). Reaching the bottom of the ladder *is* the
   instructional phase.
2. **Students will not invent the productive wrong answers on their own.** In the university
   replication, *"only **one** student"* in the unscaffolded condition generated one of the
   three target suboptimal representations — and unscaffolded PF was **worst on transfer**
   *(transfer = using what you learned on a problem you haven't seen, as opposed to repeating the
   worked case — the outcome that actually matters and the one most likely to come out null)*. The
   tutor must actively steer students into pre-authored wrong representations, on demand, one
   at a time.
3. **But it must never show them instead of eliciting them.** A vicarious-failure condition
   that replaced generation with studying six peer-generated failed solutions lost badly:
   **PF > VF, conceptual d = 1.35, transfer d = 1.23**, and VF gained **no transfer advantage
   at all** over direct instruction.

⚠ **And the argument against us, which belongs in our own introduction:** *scaffolded*
problem-solving-before-instruction has **failed on average in meta-analysis** — *a
**meta-analysis** pools many studies into one weighted estimate, so it is much harder to dismiss
than a single result* — **g = −0.08 across 60 comparisons**, with Khan-Academy/ASSISTments-style hint
sequences named explicitly. The known exception is support that is **principle-based or
metacognitive** *(metacognitive = about how you're thinking — "what are you assuming here?" —
rather than about the next algebraic move)* rather than step-level. That exception is our design space, and the *Learning and Instruction* authors name
adaptive conversational scaffolding as the next step — **which is exactly our project.**
→ [productive failure](concepts/productive-failure.md)
→ [Socratic tutoring](concepts/socratic-tutoring.md),
[productive failure](concepts/productive-failure.md),
[guardrails](concepts/guardrails.md)

### 5. A student model that isn't the LLM
Specialized knowledge tracing models — BKT, DKT, SAKT — beat LLMs on knowledge tracing in
accuracy, latency, and cost by wide margins. The LLM converses; a statistical model owns
mastery state.
→ [knowledge tracing](concepts/knowledge-tracing.md)

### 6. Course context injection
Syllabus, assignments, due dates, notation, the instructor's conventions. This is what
separates a course tutor from ChatGPT, and it's the layer Cogniti and Maizey are
essentially *entirely about*.
→ [LMS integration](practice/lms-integration.md)

### 7. Instrumented interaction logging
Every turn, hint level, attempt, timestamp. Without it there is no student model, no
research, and no evidence. Build it first; it cannot be retrofitted onto data you didn't
capture.

### What almost nobody has built

- **Longitudinal per-concept mastery tied to a live course's assignment stream.**
  Publisher platforms do adaptive recall. LLM tutors do conversation. Nearly nobody does
  both.
- **A proactive tutor.** Almost every system waits to be asked — which is exactly how you
  get 17% session usage. The one hint in the literature that proactive tutoring narrows
  the gap between low- and high-performers is the most under-explored lead we found.
- **Learning-by-teaching in an LLM tutor.** [Betty's Brain](systems/bettys-brain.md)
  proved the mechanism twenty years ago. The LLM era has largely ignored it.

---

## VI. Thermodynamics specifically

Our domain has been studied more than we expected, and the findings are sharp.

### The capability paradox

Three 2025–26 results that appear to contradict each other:

| Study | Finding |
|---|---|
| [Superstudent](domain/superstudent-thermodynamics.md) | o3 zero-shot **outscored all 90 students** on a real German thermo exam *including diagrams*. Student failure rate 58%; one A. o3 lost minor points on graphics and made one major error |
| [ThermoQA](domain/thermoqa.md) | 293 open-ended problems, CoolProp ground truth. Best composite **94.1%** (Claude Opus 4.6). But R-134a items: **44–63%** for *every* model. Supercritical water: 45–90% |
| [UTQA](domain/utqa.md) | 50 items, 19 models. Text-only mean **67%**, diagram mean **32%**, best overall **82%**. **No model** clears the authors' 95% threshold |
| [Loubet et al.](domain/thermo-problem-benchmark.md) | 22 problems, diagrams *removed*. Advanced set: best **55.2%** (GPT-4o), Llama 3.1 70B **40.7%**. Every model assumed reversibility where unstated, every run |

They are all correct, and together they say something precise:

**Peak capability is superhuman. Reliability is not.** A model that aces a hard exam and
then scores 44% on R-134a refrigerant problems is not a tutor — it's a brilliant TA who
is wrong 1 time in 3 on the refrigeration unit and never says which time. Tutoring is a
**worst-case** discipline; benchmarks report averages.

ThermoQA's sharpest finding: **rankings reshuffle across tiers.** Gemini leads property
lookup at 97.9% but ranks third on full cycles; Opus climbs from third to first.
Cross-tier degradation runs 2.8 to 32.5 percentage points. Memorization and reasoning are
different capabilities, and property tables are memorized.

→ [full analysis](domain/llm-thermodynamics-capability.md)

### The three named failure modes

1. **Unstated assumptions.** On an adiabatic process where the problem doesn't say whether
   it's reversible, assuming reversibility is wrong — and **every model tested made that
   assumption, in every repetition** ([Hoffmann et al. 2025](domain/thermo-problem-benchmark.md)).
   Not hallucination: a plausible, standard, unwarranted engineering assumption, stated
   confidently. A tutor that does this *validates the exact error our students make.*

2. **Diagrams — a large gap, but model-specific.** Mean accuracy across 19 models on
   diagram items is **32%** against **67%** text-only. But the range is **6% (gpt-4.1, below
   the 25% chance baseline) to 76% (gpt-o3)**, and o3 handled the diagram questions on a
   real exam. Errors occur at the *binding* stage — models parse axes, endpoints and
   curvature correctly, then fail to compute signed areas ∫p dV with the right orientation,
   bind leg types to axes, or propagate state limits around a cycle.
   → [diagram reading](domain/diagram-reading.md)

   **The cheapest high-value experiment available to us:** the
   [UTQA dataset is public](https://huggingface.co/datasets/herteltm/UTQA) with 17 diagram
   items. Running current models on it ourselves is a few hours' work and decides whether we
   scope diagrams in or out.

3. **Real fluids and edge regions.** R-134a at 44–63% versus water at 75–98% is a
   training-data bias with direct curricular consequences: the refrigeration unit is
   where the tutor will be least reliable, and vapor-compression cycles are ubiquitous.

### The five named error patterns

UTQA's list, which maps almost one-to-one onto
[our misconception catalogue](../research/domain/skill-graph-draft.md) and should seed it:

1. Misuse of quasistatic templates despite explicit finite-rate cues
2. Entropy bookkeeping errors — confusing transferred entropy with entropy *production*
3. Path-dependence blind spots for work — unoriented areas, mixed sign conventions
4. Missed invariants and feasibility constraints in optimization
5. Numeric anchoring to textbook constants without checking applicability

### The existing thermodynamics tutors — there are two, and the older one matters more

**[Stan](systems/stan-udel.md)**, Delaware CHEG231, Fall 2025 — read in full, it leaves our
space largely open. Levels 1–2 only, no property tools, no student model, no LMS integration,
no evaluation. Its genuinely good contribution is instructor-facing: automated **question
mining and confusion detection** from lecture transcripts. Notably, its confusion detector
flagged *"entropy and its relation to disorder or randomness"* on the entropy lecture —
surfacing, automatically, the exact misconception in our own catalogue.

**[CyclePad](systems/cyclepad-cycletalk.md)** (Northwestern, Forbus & Whalley) is the more
important precedent, and essentially nobody in the current literature cites it. It is an
**articulate virtual laboratory** for thermodynamic cycles — students assemble Rankine, Brayton,
Otto, Diesel and refrigeration cycles from components, and the system propagates constraints,
catches contradictions, and **explains every derived value by tracing the assumption chain that
produced it**. It has been in the **US Naval Academy curriculum since 1996** and shipped
commercially. We downloaded and dissected v2.0; the archaeology is in the node.

The architectural lesson is the one our field keeps relearning: **CyclePad never guesses.** Every
number is derived by a named equation from named assumptions, and the "explain" facility is not
generated prose but a walk over a truth-maintenance system. That is exactly the guarantee an LLM
cannot give and a [tool-calling layer](concepts/grounding-and-verification.md) can.

**And CycleTalk is the experiment we were about to propose.** In 2004–2006, Rosé's group at CMU
bolted **tutorial dialogue** onto CyclePad, on the theory that the simulator alone left students
exploring without reflecting. Results, read in full:

- **The clean comparison is positive but small.** At the **US Naval Academy**, dialogue-augmented
  CyclePad beat plain CyclePad: **F(1,86) = 5.57, p < .05, effect size 0.25 SD**.
- **The CMU study's headline 0.35 SD is a *dose* effect, not a dialogue-vs-control effect** — the
  authors discarded their own control comparison because a quiz was administered between session
  days. What it compares is dialogues fired on *success events* (mean 2.7 seen) against dialogues
  fired only on *hint requests* (mean 1.8 seen).
- **Gains appeared on the conceptual post-test and on neither of the two open-ended design
  exercises.** The same conceptual-not-applied split [Andes](systems/andes.md) found.
- **Students almost never asked for help — 14% of actions.** One of seven sensitivity-analysis
  dialogues was seen by *any* student in the hint-triggered condition. **Proactivity was the
  experimental manipulation and proactivity was what worked.**
- The authors concede the system *"falls far short"* of the human tutor it imitated, and name the
  gap precisely: their agents **elicited reflection** but could not **assist with navigation** —
  help a student decide what to do next in an open design space.

**That last sentence is the thesis of our project** — and the archaeology sharpens it further.
**CycleTalk never called CyclePad's explanation facility.** The dialogue agent model-traced the
student's *actions* against a pre-authored behavior graph; it never read the cycle state or the
constraint network to reason about the design in front of it. The two halves of the best
precedent in our domain — an engine that can explain any value it derives, and an agent that
talks about thermodynamics — **sat side by side for two years and were never joined.** An agent
that cannot see the design state cannot help you navigate it; it can only recite prompts attached
to graph nodes, which is exactly what the authors observed.

The 2006 team had the simulator, had the verified physics, had validated dialogue content — and
could not do free-form navigation support because the language technology did not exist. It does
now. We are not proposing something untested; we are proposing **the specific join they never
made.**

⚠ **Two honesty notes before anyone cites this as settled.** First, the negotiation dialogue that
makes CycleTalk sound so much like our project **was never built** — the vivid trade-off exchange
in the CHI paper is a position-paper illustration in future tense, and what shipped was scripted
short-answer dialogue. Second, the CMU study's **raw gains favour the control** (S +10.75, PSHELP
+7.16, PSSUCCESS +7.59) and plain CyclePad is best or tied on both practical measures. The
0.35 SD is a concept-level ANOVA result, and assignment was by lab session rather than
randomised. **Cite CycleTalk as suggestive precedent, not as an established effect.**

Their **authoring pipeline is directly reusable**: record human tutoring in the real environment,
have a domain expert segment it into topics, **check that topic coverage predicts post-test score
before authoring anything** (R² = .715, N = 21 — ***R²** = share of variation in one measure
explained by another, so ~72% of post-test variation tracked topic coverage; **N** is just n*),
then author to the validated topics.
→ [full node](systems/cyclepad-cycletalk.md)

---

## VII. Open problems

Where the field is actually stuck. These are the places a capstone could contribute.

1. **Nobody has shown a positive learning effect from a guardrailed chatbot tutor at
   scale.** Bastani's guardrailed arm was neutral. The positive results come from
   hand-built, single-course, expert-designed systems. Whether the hand-built magic can
   be systematized is *the* open question in the field.

2. **The engagement wall.** 17% session usage, 5% power users. Every deployment hits it.
   Almost every published evaluation studies mandatory or incentivized use, so we have
   very little data on what sustains *voluntary* return. → [engagement decay](concepts/engagement-decay.md)

3. **Proactivity.** If waiting to be asked yields 17% usage, the tutor should sometimes
   speak first. Barely explored.

4. **Pedagogical policy as code.** [MathTutorBench](evaluation/mathtutorbench.md) showed
   subject expertise and pedagogical skill *trade off* — better models are not better
   teachers. Almost all deployed pedagogy is a system prompt. There is no standard
   library of hint ladders.

5. **Diagram-native tutoring in engineering.** At 32% accuracy, no current architecture
   can tutor from a P-v diagram *(pressure–volume, one of the two standard plots of a
   thermodynamic cycle alongside T-s, temperature–entropy)*. Structured state representations plus
   rendered diagrams,
   rather than vision over images, is an obvious and untried direction.

6. **What "knowing thermodynamics" means, operationally — and the instruments are weaker
   than the field pretends.** Concept inventories measure conceptual gain; course grades
   measure problem-solving; interventions routinely move one and not the other, and almost
   nobody reports both. Worse, thermodynamics' best-known inventory (the TCI) was **never
   finished** and its developers discourage using it. Physics has the FCI; engineering
   thermodynamics has nothing of comparable standing. That is a real gap in the field, and
   it constrains what any of us can credibly claim.
   → [concept inventories](evaluation/concept-inventories.md)

7. **Honest reporting of voluntary usage decay.** Nearly absent from the literature. Any
   study that reports week-10 voluntary return rates is contributing something rare.

---

## VIII. What this means for our project

### Three things that changed based on this research

**1. The thermodynamics benchmark is no longer a novel contribution.**
Our earlier plan named "build a thermodynamics tutoring benchmark" as the most likely
publishable output. [ThermoQA](domain/thermoqa.md) and [UTQA](domain/utqa.md) got there
first, and ThermoQA in particular is well-built — 293 problems, programmatic CoolProp
ground truth, six frontier models, three runs each. UTQA's dataset is public. **Use them as
instruments; don't rebuild them.**

What does *not* exist is a thermodynamics **pedagogy** benchmark. Two viable templates now:
the open-ended expert-preference approach of [MathTutorBench](evaluation/mathtutorbench.md),
or — probably more tractable — [TutorGym's](evaluation/tutorgym.md) **correct/incorrect
student-action labeling task**, which has ground truth and where *no model beats chance*.
A thermodynamics version of that is buildable by a capstone team, needs no student data, and
targets a documented, striking failure.

**⚠ 1b. Our planned outcome instrument does not hold up.**
The Thermodynamics Concept Inventory — which we had named as the defensible answer to "how do
you know they learned anything," partly on the strength of a Penn State connection — is an
**unfinished instrument whose developers discourage its use**, with PhysPort's lowest
validation rating. Switch to the **TTCI-T** or the Survey of Thermodynamic Processes, follow
PhysPort's recommendation guide rather than name recognition, and request educator
verification in week 1 because access is slow.
→ [concept inventories](evaluation/concept-inventories.md)

**2. Penn State has already solved our biggest compliance obstacle.**
PSU offers **AI Studio** to all students — a suite including **Claude, Gemini, and
ChatGPT** — alongside an **AI Center of Excellence in Teaching and Learning** that has
awarded **46 instructional innovation grants** for 2026–27. This likely means an existing
institutional agreement, which was the single scariest item on our
[compliance checklist](../admin/irb.md). **Verify this in week 1** — it could remove weeks
of blocking work, and the grant program is a plausible funding and legitimacy path for
the capstone itself. → [PSU AI landscape](practice/psu-ai-landscape.md)

**3. Cost is not a real constraint.** ~$2.63–4.79 per student per semester. Stop treating
it as a design driver. → [cost](practice/cost-economics.md)

### What the evidence says our project should actually be

The literature points somewhere more specific than "build an AI tutor":

- **The unit of success is the course, not the model.** Every positive result came from
  expert hand-work on one course's content. Our differentiator is the PSU thermodynamics
  course itself — its problems, its notation, its misconceptions — not our architecture.
  → [skill graph](../research/domain/skill-graph-draft.md)
- **Copy Kestin's study design, not his effect size.** The crossover — every student gets
  both conditions, each is their own control — is statistically efficient at our n, ethically
  clean, and (per [Corvinus](evidence/corvinus-2025-overreliance.md)) the design least likely
  to provoke a backlash over withheld AI access. Report an FCI/TTCI-T-stratified subgroup
  analysis, which is what makes his generalizability claim credible.
- **Design for the defection, not the ideal student.** "What do I do next" is the
  second-most-common thing students say. Build the hint ladder that answers it *well*
  rather than the refusal that doesn't.
- **Instrument for engagement from turn one.** The field's actual failure mode is that
  nobody comes back. Voluntary week-10 return rate should be a primary metric, not a
  footnote.
- **Consider the hybrid frame.** [Tutor CoPilot](systems/tutor-copilot.md) got its
  strongest effect by improving human tutors, especially weak ones. A tool that makes PSU
  thermo TAs better in office hours is a smaller, more tractable, better-evidenced project
  than a standalone tutor — and nobody has done it for engineering.
- **Own the diagram problem or scope it out explicitly.** Test it on the public UTQA items
  first — the answer may be "pick a reasoning model," which is far cheaper than the
  render-don't-read architecture we'd otherwise need.
- **Diagnosis, not explanation, is the hard part.** [TutorGym](evaluation/tutorgym.md) says
  no model reliably recognizes a wrong step. Everything a tutor does downstream of "is this
  right?" inherits that error. Our verification layer has to answer that question with a
  solver, not an opinion.
- **The first two interactions decide everything.** KAIST's students who used the tutor five
  times or fewer rated it *worse* afterward (3.72 → 3.26), while frequent users rated it
  *better*. Onboarding is not polish; it is the retention mechanism.

### Honest risk assessment

The most likely outcome of a well-executed capstone here, based on this literature, is a
tutor that students like, that does no harm, that ~15% of them use after week three, and
that produces a learning effect too small to detect at our sample size. **That is the
modal result in this field.** Planning for it — by measuring engagement and process
rather than betting everything on a learning-gain headline — is the difference between a
capstone with findings and one with a demo.

---

## IX. Where to go next in this wiki

**By theme:**
- The systems: [`systems/`](systems/)
- The ideas: [`concepts/`](concepts/)
- The studies: [`evidence/`](evidence/)
- Our domain: [`domain/`](domain/)
- Measurement: [`evaluation/`](evaluation/)
- Deployment reality: [`practice/`](practice/)

**If you only read four nodes:**
1. [Bastani 2025 — Generative AI can harm learning](evidence/bastani-2025-harm.md)
2. [Kestin 2025 — the Harvard RCT](evidence/kestin-2025-rct.md)
3. [LLM capability in thermodynamics](domain/llm-thermodynamics-capability.md)
4. [Socratic tutoring and how students subvert it](concepts/socratic-tutoring.md)

**Nodes now standing on full reads of their primaries (31 Aug 2026):**
[Stan](systems/stan-udel.md) · [Bastani](evidence/bastani-2025-harm.md) ·
[Kestin](evidence/kestin-2025-rct.md) · [UTQA](domain/utqa.md) ·
[ThermoQA](domain/thermoqa.md) · [Superstudent](domain/superstudent-thermodynamics.md) ·
[PeteChat](systems/petechat-purdue.md) · [CS50](systems/cs50-duck.md) ·
[TutorGym](evaluation/tutorgym.md) · [KAIST](evidence/kaist-vta-2025.md) ·
[Khanmigo](evidence/khanmigo-engagement-2026.md) ·
[knowledge tracing](concepts/knowledge-tracing.md) ·
[productive failure](concepts/productive-failure.md) ·
[Socratic discourse taxonomy](concepts/socratic-tutoring.md) ·
[Andes](systems/andes.md) · [CyclePad / CycleTalk](systems/cyclepad-cycletalk.md) ·
[behavioral evaluation](evaluation/behavioral-evaluation.md) ·
[cost and latency](practice/cost-economics.md)

**Highest-priority reading still outstanding**, with the honest reason each is still open:

| Source | Why it matters | Blocker |
|---|---|---|
| **VanLehn 2011**, *Educational Psychologist* | The field's most-cited effect sizes (human ≈ ITS) come from here and we have never read it | ⚠ Closed access; ASU now serves the author's own copies behind Cloudflare Access; **no Internet Archive snapshot. Needs PSU library.** |
| **Kulik & Fletcher 2016**, *RER* | The other headline ITS meta-analysis (g = 0.66) | Closed; the public DTIC technical report (AD1030353) has been under maintenance throughout. **Retry DTIC, else PSU library.** |
| **Rosé et al. 2006**, *IJAIED* 16(2) | Fullest account of CycleTalk — the closest precedent to this project | IOS Press blocks scripted access entirely. **PSU library.** |
| **Roscoe & Chi 2007** | Tutor-learning / explanation quality | Closed, no OA location in OpenAlex |
| **Tuttle & Wu (QR-2001)**, USNA thermodynamics ICAI | Possible learning-outcome data for CyclePad at USNA | Newly found in a reference list; not yet chased |

**These five are the whole remaining backlog worth a librarian's time.** Everything else we have
either read or established is genuinely unobtainable. Access recipes — including the DSpace REST
route that got us Sinha & Kapur after Sage refused — are in [the wiki README](README.md).

---

*Maintained as part of the [knowledge brain](README.md). Corrections and upgrades from
`[skimmed]` to `[read]` are the most valuable contributions you can make to this file.*
