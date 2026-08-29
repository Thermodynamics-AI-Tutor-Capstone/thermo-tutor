# Annotated Bibliography

Grouped by what each source is good for. Verification status is honest: **[read]** means
someone on the team read the full text, **[skimmed]** means abstract/summary only,
**[found]** means we know it exists and haven't opened it.

---

## Primary evidence that AI tutoring works

**Kestin, G., Miller, K., Klales, A., Milbourne, T., Ponti, G. (2025). "AI tutoring
outperforms in-class active learning: an RCT introducing a novel research-based design in
an authentic educational setting." *Scientific Reports*.** [skimmed]
https://www.nature.com/articles/s41598-025-97652-6
194 students, Harvard Physical Sciences 2, Fall 2023. ~2× learning gains vs.
active-learning classroom, less time on task, higher engagement. Within-subject
alternating design. **Our methodological template.** Read in full before designing any
study.
Popular coverage: https://hechingerreport.org/proof-points-ai-tutor-harvard-physics/ ·
https://news.harvard.edu/gazette/story/2024/09/professor-tailored-ai-tutor-to-physics-course-engagement-doubled/

**"AI tutoring can safely and effectively support students: An exploratory RCT in UK
classrooms" (2025), arXiv:2512.23633 / LearnLM.** [found]
https://arxiv.org/abs/2512.23633 ·
https://storage.googleapis.com/deepmind-media/LearnLM/learnLM_nov25.pdf
165 students, five UK secondary schools, Eedi maths platform. LearnLM prompted to guide
students to find their own mistake. Useful for safety framing and for how DeepMind
defines "safely."

**"Socratic AI in K–12 Science Classrooms: Effects on Critical Thinking, Motivation, and
Self-Regulation in a Randomized Controlled Trial."** [found]
Three-arm RCT (AI-powered argument-driven inquiry vs. traditional ADI vs. control).

---

## The findings that constrain design

**"A bottom-up taxonomy of student discourse with a Socratic AI physics tutor" (2026),
arXiv:2608.07373.** [skimmed]
https://arxiv.org/html/2608.07373v1
2,874 student turns, 221 sessions, 357 categories. "What do I do next" is the
second-most-common move at 4.4%. **The most important paper in this bibliography for our
design.** Someone needs to read this in full and present it to the team.

**"Using Large Language Models for Solving Thermodynamic Problems" (2025),
arXiv:2502.05195.** [skimmed]
https://arxiv.org/abs/2502.05195
22-problem benchmark, five models. The adiabatic-reversibility failure (all models, all
repetitions). **Directly on our domain.** Read in full; consider extending their
benchmark rather than starting from scratch.

**"Faster, Cheaper, More Accurate: Specialised Knowledge Tracing Models Outperform LLMs"
(2026), arXiv:2603.02830.** [skimmed]
https://arxiv.org/pdf/2603.02830
Settles the "should the LLM track mastery" question. No.

**Khan Academy blog, "How Khan Academy Is Building a Better AI Tutor: Our Most Recent
Learnings."** [skimmed]
https://blog.khanacademy.org/how-khan-academy-is-building-a-better-ai-tutor-our-most-recent-learnings/
Source for the separate math-agent architecture and math-error-rate guardrail metric.
Practitioner writeup, not peer-reviewed, but unusually candid.

**"AI Tutoring with Khanmigo in a Two-Year School Experiment" (2026), EdWorkingPapers.**
[skimmed]
https://edworkingpapers.com/sites/default/files/ai26-1551.pdf
Source of the engagement numbers: 96% tried it, median student used it in 17% of practice
sessions. Coverage:
https://www.chalkbeat.org/2026/08/25/ai-tutoring-students-khanmigo-khan-academy-engagement-study/
**Read this before we assume students will use what we build.**

---

## Domain-specific: thermodynamics + AI

**"Stan: An LLM-based thermodynamics course assistant" (2026), arXiv:2603.04657.**
[skimmed — PDF cached locally]
https://arxiv.org/pdf/2603.04657
University of Delaware ChemE. Ollama/local models, RAG over Sandler, Socratic refusal,
Faster-Whisper + Silero VAD voice, Sphinx/Jupyter delivery. **Closest competitor.**
Highest-priority full read. Consider contacting the authors.

**"Exploring the Role of AI in Learning and Teaching Thermodynamics: A Case Study with
ChatGPT," *The Physics Educator*.** [found]
https://www.worldscientific.com/doi/10.1142/S2661339524500136
Classical thermodynamics scenarios at varied complexity.

---

## Evaluation and benchmarking

**MathTutorBench (EMNLP 2025 Oral), arXiv:2502.18940.** [skimmed]
Paper: https://arxiv.org/abs/2502.18940 · Code: https://github.com/eth-lre/mathtutorbench
Three axes: subject expertise, student understanding, teacher response generation. Reward
model scores open-ended pedagogical quality. **The template for a thermo analogue.**

**"Unifying AI Tutor Evaluation: An Evaluation Taxonomy for Pedagogical Ability
Assessment of LLM-Powered AI Tutors," arXiv:2412.09416.** [found]
https://arxiv.org/html/2412.09416v1
Source of MRBench (MathDial + Bridge).

**BEA 2025 Shared Task** — pedagogical ability assessment of AI tutors, 20th Workshop on
Innovative Use of NLP for Building Educational Applications. [found]
Example system paper: https://arxiv.org/pdf/2506.10627

**"The Missing Evaluation Axis: What 10,000 Student Submissions Reveal About AI Tutor
Effectiveness," arXiv:2605.05648.** [found]

**AITutor-EvalKit, arXiv:2512.03688.** [found] https://arxiv.org/pdf/2512.03688

---

## Concept inventories (assessment instruments)

**PhysPort — Thermodynamics Concept Inventory (TCI).** [found]
https://www.physport.org/assessments/assessment.cfm?A=TCI
**Thermal and Transport Concept Inventory — Thermodynamics (TTCI-T):**
https://www.physport.org/assessments/assessment.cfm?A=TTCIT
Which-to-use guidance:
https://www.physport.org/recommendations/Entry.cfm?ID=124933

**Development of Engineering Thermodynamics Concept Inventory instruments.** [found]
Penn State record: https://pure.psu.edu/en/publications/development-of-engineering-thermodynamics-concept-inventory-instr-2/
IEEE: https://ieeexplore.ieee.org/document/963691
**Developed here.** Use the institutional connection.

**Resource Letter RBAI-1: Research-based Assessment Instruments in Physics and
Astronomy, arXiv:1605.02703.** [found] Comprehensive index of validated instruments.

---

## Student modeling / knowledge tracing

- Bayesian Knowledge Tracing overview: https://www.emergentmind.com/topics/bayesian-knowledge-tracing
- Piech et al., Deep Knowledge Tracing (2015) — the RNN/LSTM paradigm shift. [found]
- "Deep Learning vs. Bayesian Knowledge Tracing: Student Models for Interventions,"
  *JEDM* 2018: https://eric.ed.gov/?id=EJ1195512 [found]
- BKT-LSTM, arXiv:2012.12218 [found]
- "Leveraging LLMs for Bayesian and Deep Knowledge Tracing in the Logic-Muse ITS,"
  Springer 2025 [found]

## Spaced repetition

- **FSRS** — open-source, fits a model to actual review history. Benchmarks on 500M+ Anki
  reviews: ~20–30% fewer reviews than SM-2 for equal retention; ~4% mean absolute error
  on recall probability vs. ~14% for SM-2. Anki default since 23.10 (Nov 2023); v6 (2025)
  adds a per-user forgetting-decay parameter.
  https://help.remnote.com/en/articles/9124137-the-fsrs-spaced-repetition-algorithm

---

## Computational tools (property data)

- **CoolProp** — https://sourceforge.net/projects/coolprop/ — thermophysical property
  backend, Python bindings.
- **Cantera** — https://cantera.org/ — thermo, kinetics, transport. Can generate
  saturated steam tables in customary units. **Different reference state than
  CoolProp/NIST — see key finding #2.**
- **ThermoState** — https://github.com/Thermo-State/ThermoState — CoolProp GUI for power
  and refrigeration cycles. Useful prior art for how to present state calculations to
  students.
- **AwesomeThermodynamics** — https://github.com/iurisegtovich/AwesomeThermodynamics —
  curated resource list.
- IAPWS-IF97 + CoolProp portable steam table app:
  https://e-journals.irapublishing.com/index.php/IRAJTMA/article/view/351

---

## Integration and compliance

- **Canvas LTI 1.3 / LTI Advantage** — Instructure developer docs:
  https://developerdocs.instructure.com/services/canvas/external-tools/lti/file.tools_intro
  Grading/AGS: https://developerdocs.instructure.com/services/canvas/external-tools/lti/file.assignment_tools
  Advantage = Deep Linking + Assignment & Grade Services + Names and Roles Provisioning.
  Requires an admin-issued developer key.
- **API vs. LTI for Canvas** (Edlink) — https://ed.link/community/api-vs-lti-integration-for-canvas/
  Useful plain-language comparison for deciding our integration path.
- FERPA + AI vendors — the "school official" exception, and the requirement that vendors
  not train on student inputs. See `admin/irb.md` for our specific obligations.

---

## To find

Gaps in this bibliography someone should fill:

- [ ] Anything on **voluntary usage decay** in optional educational tools (the Khanmigo
      engagement problem, generalized).
- [ ] Misconception literature specific to **engineering thermodynamics** (heat vs.
      temperature, entropy-as-disorder, work as a state function).
- [ ] **Productive failure** literature (Kapur) — the theoretical basis for delaying
      hints rather than refusing them.
- [ ] **Self-regulated learning** measures — if we claim students learn to learn better,
      we need an instrument.
- [ ] Prior work on **AI tutors and academic integrity** — what happens to homework
      grades as a signal when a tutor exists.
