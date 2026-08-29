# The State of the Art in AI Tutoring for College Courses

**A survey for the Penn State AI Thermodynamics Tutor capstone**
*Compiled August 2026 · Living document · Entry point to the [knowledge brain](README.md)*

---

## How to read this

Every claim below links to a node with the primary sources behind it. Follow the links
when you want depth; the paper itself is the argument, not the archive.

Verification status is marked honestly throughout. Most sources here are `[skimmed]` —
abstract or secondary coverage. Where a number matters and we have only skimmed it, the
paper says so. **Do not cite anything from this document in a graded deliverable until
someone has upgraded it to `[read]`.**

---

## Executive summary

If you read nothing else:

1. **The subject-matter problem is solved. The teaching problem is not.** OpenAI's o3,
   zero-shot, solved every problem on a university thermodynamics exam correctly —
   better than every human student, scoring in the range of the best results across
   10,000+ administrations of that exam since 1985
   ([superstudent](domain/superstudent-thermodynamics.md)). In the same period,
   a purpose-built benchmark found **no** 2025-era model clears a 95% reliability bar for
   unsupervised thermodynamics tutoring ([UTQA](domain/utqa.md)). Both are true. §VI
   explains why.

2. **The pre-LLM field already set a high bar, and the LLM era has mostly not cleared
   it.** Step-based intelligent tutoring systems achieved **d = 0.76** against no
   tutoring; human tutors achieved **d = 0.79** ([VanLehn 2011](concepts/vanlehn-2011.md)).
   Systems from the 1990s and 2000s — [Andes](systems/andes.md),
   [Cognitive Tutor](systems/cognitive-tutor.md), [ALEKS](systems/aleks.md) — are the
   incumbents, not ChatGPT.

3. **The single best result for LLM tutoring is real, and narrow.** A Harvard RCT
   (n = 194) found roughly **2× the learning gains** of an excellent active-learning
   classroom, in less time ([Kestin et al. 2025](evidence/kestin-2025-rct.md)). One
   course, one physics-education-researcher instructor, heavily hand-built scaffolds.

4. **The single most important negative result is also real, and larger.** In a
   ~1,000-student RCT, students given an unguarded GPT-4 interface did **48% better
   during practice and 17% worse on the unassisted exam** than controls. Students given a
   guardrailed tutor version did 127% better during practice and **scored the same as
   controls** on the exam ([Bastani et al., PNAS 2025](evidence/bastani-2025-harm.md)).
   Read that again: the best-designed arm's effect on actual learning was *zero*.

5. **The honest state of the art is "no proven harm," not "proven benefit."** Outside a
   handful of expertly hand-built single-course deployments, nobody has demonstrated a
   robust positive learning effect from a chatbot tutor at scale. Guardrails are
   currently doing damage control, not producing gains.

6. **The field's real failure mode is engagement, not quality.** 96% of students tried
   Khanmigo at least once; the median student used it in **17% of practice sessions**
   ([Khanmigo engagement study](evidence/khanmigo-engagement-2026.md)). Roughly 5% of
   students account for most benefit from voluntary digital tools, and that 5% skews
   already-high-performing and higher-income ([equity](practice/equity.md)).

7. **Students route around Socratic design.** In 2,874 coded student turns with a
   Socratic AI physics tutor, "what do I do next" was the **second-most-common move**
   (4.4% of all turns), and the top 20 discourse categories contained essentially no
   conceptual reasoning ([Socratic subversion](concepts/socratic-tutoring.md)).

8. **Every serious system independently converged on the same architecture:** a
   constrained, retrieval-grounded, externally-verified LLM wrapped in deterministic
   policy — with the pedagogy in code, not in the prompt. §V lays out the seven layers.

9. **Grounding + verification is what separates working systems from demos.**
   [Jill Watson](systems/jill-watson.md), restricting outputs to validated course
   material and verifying each response by textual entailment, answers correctly **78.7%**
   of the time with **2.7%** harmful errors. OpenAI's own Assistant on the same task:
   **30.7%** correct, **14.4%** harmful.

10. **Cost is not the constraint.** Realistic full-semester usage runs roughly
    **$2.63–$4.79 per student** in API spend ([cost](practice/cost-economics.md)). The
    constraints are pedagogy, engagement, compliance, and faculty trust.

11. **For thermodynamics specifically, the diagram gap is the wall.** Across 19 models,
    mean accuracy on thermodynamic diagram items was **32%**, versus **67%** on text-only
    items — often at chance ([diagram reading](domain/diagram-reading.md)). P-v and T-s
    diagrams are not a nice-to-have in this subject.

12. **The benchmark we were going to build already exists.** [ThermoQA](domain/thermoqa.md)
    (293 open-ended problems, three tiers, CoolProp ground truth, six frontier models) and
    [UTQA](domain/utqa.md) (50 items, 19 models) both landed before us. This changes our
    contribution story — see §VIII.

---

## I. Prehistory: what the field already proved (1970–2015)

The LLM era did not invent tutoring systems. It inherited a fifty-year research program
that had already answered several of the questions people are currently re-asking.

### Bloom's 2 sigma, and why it was wrong

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
  cognitive models, model tracing, [knowledge tracing](concepts/knowledge-tracing.md).
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

| Metric | Jill Watson | OpenAI Assistant |
|---|---|---|
| Correct | **78.7%** | 30.7% |
| Harmful failures | **2.7%** | 14.4% |
| Confusing failures | **54.0%** | 69.2% |
| Retrieval failures | **43.2%** | 68.3% |

This is the cleanest available evidence that **architecture beats model.** Same
underlying LLM. 2.5× the accuracy, one-fifth the harmful errors. The difference is
grounding and verification — see
[grounding and verification](concepts/grounding-and-verification.md).

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

**[Stan](systems/stan-udel.md)** (Delaware, ChemE thermodynamics) is the closest *domain*
sibling — local Ollama models, RAG over Sandler, Socratic refusal, voice I/O, Fall 2025.
**Read this one first.**

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

- **[Khanmigo engagement](evidence/khanmigo-engagement-2026.md)** — two-year school
  study. 96% tried it; median student messaged it on a third of practice days and in
  **17% of practice sessions.** Near-universal access, thin engagement.

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
   scaffolds for specific problems. That does not generalize by copying the prompt.
   **The unit of success in this literature is the course, not the model.**

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

### 1. Retrieval grounding
Restrict the model to validated course material. Everyone does this. It is necessary and
nowhere near sufficient — Jill Watson's *retrieval* failure rate is still 43.2%.
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
| [Superstudent](domain/superstudent-thermodynamics.md) | o3 zero-shot solved **all** problems on a university thermo exam — better than every student, in the range of the best scores across 10,000+ exams since 1985 |
| [ThermoQA](domain/thermoqa.md) | 293 open-ended problems, CoolProp ground truth. Best composite **94.1%** (Claude Opus 4.6). But R-134a items: **44–63%** for *every* model. Supercritical water: 45–90% |
| [UTQA](domain/utqa.md) | 50 items, 19 models. Best **82%** (o3). **No model** clears the authors' 95% threshold for unsupervised tutoring |

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

2. **Diagrams.** Mean accuracy across 19 models on thermodynamic diagram items: **32%**,
   versus **67%** text-only. Often at chance. Errors are in *binding visual features to
   thermodynamic meaning*, not in low-level recognition — models find the axes and then
   misread what they mean. Since P-v and T-s diagrams are load-bearing in this subject,
   this is a wall, not a rough edge. → [diagram reading](domain/diagram-reading.md)

3. **Real fluids and edge regions.** R-134a at 44–63% versus water at 75–98% is a
   training-data bias with direct curricular consequences: the refrigeration unit is
   where the tutor will be least reliable, and vapor-compression cycles are ubiquitous.

### The one existing thermodynamics tutor

**[Stan](systems/stan-udel.md)**, Delaware ChemE, Fall 2025. Local Ollama models, RAG over
Sandler, Socratic refusal, Faster-Whisper + Silero VAD voice, Sphinx/Jupyter delivery.
Reported limitations: failures on complex problem types and constrained reasoning on
multi-step calculations — consistent with everything above.

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
   can tutor from a P-v diagram. Structured state representations plus rendered diagrams,
   rather than vision over images, is an obvious and untried direction.

6. **What "knowing thermodynamics" means, operationally.** Concept inventories measure
   conceptual gain; course grades measure problem-solving. Interventions routinely move
   one and not the other, and almost nobody reports both.
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
ground truth, six frontier models, three runs each. **We should use them as instruments,
not rebuild them.** What does *not* exist is a thermodynamics **pedagogy** benchmark — the
[MathTutorBench](evaluation/mathtutorbench.md) axis, not the correctness axis. That gap
is still open.

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
- **Own the diagram problem or scope it out explicitly.** At 32% accuracy this is the
  single biggest technical risk in our domain, and it is not solved by a better prompt.

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

**Highest-priority reading not yet done by anyone on this team:**
- [Stan](systems/stan-udel.md) — our closest competitor, full text
- [ThermoQA](domain/thermoqa.md) — the instrument we should be using
- The [Socratic discourse taxonomy](concepts/socratic-tutoring.md) — full text
- [PeteChat](systems/petechat-purdue.md) — the closest methodological sibling

---

*Maintained as part of the [knowledge brain](README.md). Corrections and upgrades from
`[skimmed]` to `[read]` are the most valuable contributions you can make to this file.*
