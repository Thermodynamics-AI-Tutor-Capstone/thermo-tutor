# Paper holdings — retroactive audit of every cited source

Generated 2026-09-03. Scope: every markdown link with an `http(s)` URL in
`knowledge/**/*.md` and `docs/02-bibliography.md`. Acquisition only — no markdown file was modified.

All PDFs live in `course-materials/papers/` (git-ignored). Every file was verified with
`head -c 5 file.pdf | grep -q '%PDF'` — `file(1)` is unreliable here because it trusts the extension,
and login walls / Cloudflare challenges return HTTP 200 with HTML. Each PDF has a sibling `.txt`
from `pdftotext`.

---

## 1. Acquired

99 distinct artefacts, covering 113 cited link instances.
`Prov.` = **new** (fetched in this audit), `pre-existing` (one of the 7 already held), `added out-of-band`
(appeared in the directory from another process while this audit ran).

| File (`.pdf` + `.txt`) | Title | Tag | Citing node(s) | Prov. |
|---|---|---|---|---|
| `agent-rot-2026-long-horizon-degradation` | "How Fast Do Agents Rot? An Empirical Study of Long-Horizon Degradation in LLM Agents," arXiv:2609.01660 | `read` | `practice/agent-architecture` | added out-of-band |
| `alimin-2026-chatpid-graphrag` | Alimin & Schweidtmann, ChatP&ID, arXiv:2603.22528 | `read` | `domain/diagram-reading` | **new** |
| `alkhatlan-2018-its-historical-survey` | Alkhatlan & Kalita (2018), "Intelligent Tutoring Systems: A Comprehensive Historical Survey with Recen… | `read` | `concepts/vanlehn-2011` | **new** |
| `amoozadeh-2024-student-ai-interaction-cs1` | Amoozadeh, Nam, Prol, Alfageeh, Prather, Hilton, Srinivasa Ragavan & Alipour (2024), "Student-AI Inter… | `read` | `practice/assessment-integrity`, `systems/cs50-duck` | **new** |
| `automata-2026-agent-trace-failure-prediction` | "Automata from Agent Traces: Failure and Next-Step Prediction," arXiv:2608.23670 | `read` | `practice/agent-observability` | added out-of-band |
| `bassner-2025-tum-dissociation` | Bassner, Lenk-Ostendorf, Beinstingel, Wasner & Krusche (2025), "Less stress, better scores, same learn… | `abstract-only` | `evidence/tum-dissociation-2025` | pre-existing |
| `bastani-2025-genai-without-guardrails` | Bastani et al., "Generative AI without guardrails can harm learning: Evidence from high school mathema… | `read` | `concepts/engagement-decay`, `concepts/guardrails`, `evidence/bastani-2025-harm` | **new** |
| `benedek-2025-ai-overreliance-knowledge` | "Impact of AI Tools on Learning Outcomes: Decreasing Knowledge and Over-Reliance," arXiv:2510.16019 | `skimmed` | `evidence/corvinus-2025-overreliance` | **new** |
| `bhattacharyya-2026-specialised-kt-outperform-llms` | Bhattacharyya et al., "Specialised KT Models Outperform LLMs," arXiv:2603.02830 | `read` | `concepts/knowledge-tracing` | **new** |
| `bilgin-2025-genai-chemical-engineering-education` | Bilgin, Chen & Velegol (2025), "Generative AI in Chemical Engineering Education," ASEE Annual Conference | `read` | `evidence/student-ai-perceptions-2025`, `practice/content-generation` | **new** |
| `biotutor-eth-2026` | "A Lecture-Specific AI-Based Tutor for Higher Education: Pedagogical Design and Empirical Evaluation,"… | `abstract-only` | `systems/biotutor-eth` | pre-existing |
| `biswas-2016-bettys-brain-design-to-practice` | Biswas, Segedy & Bunchongchit, "From Design to Implementation to Practice a Learning by Teaching Syste… | `read` | `systems/bettys-brain` | **new** |
| `bloom-1984-two-sigma-problem` | Bloom (1984), "The 2 Sigma Problem," Educational Researcher 13(6), 4–16 | `found` | `concepts/vanlehn-2011` | **new** |
| `bouke-2026-gasp-rag-hallucination` | Detecting Hallucinations in RAG through Grounding-Aware Sensitivity by Perturbation (GASP), arXiv:2607… | `found/read` | `concepts/grounding-and-verification` | **new** |
| `brown-2025-gpthermo-wpi` | Brown, H. Z. & Ebadi, R. (2025). "GPThermo: An In-House Generative Artificial Intelligence Tutor for T… | `read` | `PAPER`, `systems/gpthermo-wpi` | **new** |
| `brundage-2024-thermo-concept-survey` | Brundage & Singh, "Survey of Thermodynamic Processes and First and Second Laws," PRPER 19, 020112 / ar… | `read` | `evaluation/concept-inventories` | **new** |
| `chowrira-2019-diy-productive-failure` | Chowrira, Smith, Dubois & Roll (2019), "DIY productive failure," npj Science of Learning 4:1 | `read` | `concepts/productive-failure` | **new** |
| `christopher-2025-ai-intro-thermodynamics` | Christopher, Bongioanni & Scharff (2025), "Applications of Artificial Intelligence in an Introductory … | `read` | `evidence/student-ai-perceptions-2025` | **new** |
| `cooper-2026-principles-genai-chem-education` | Cooper, M. M. (2026), "A Preliminary Set of Principles to Support Learning in the Context of Generativ… | `read` | `practice/assessment-integrity` | **new** |
| `dange-2026-aiplato-physics-homework` | Dange, Lopez, Shah & Deslauriers (2026), "aiPlato: A Novel AI Tutoring and Stepwise Feedback System fo… | `read` | `systems/aiplato-uta` | **new** |
| `doignon-falmagne-knowledge-spaces-learning-spaces` | Doignon, J.-P. & Falmagne, J.-C., "Knowledge spaces and learning spaces," arXiv:1511.06757 / eScholarship | `read` | `systems/aleks` | **new** |
| `doroudi-2017-bkt-identifiability` | Doroudi & Brunskill, "The Misidentified Identifiability Problem of Bayesian Knowledge Tracing," EDM 2017 | `read` | `concepts/knowledge-tracing` | **new** |
| `duzkar-2026-thermoqa` | Düzkar, "ThermoQA: A Three-Tier Benchmark for Evaluating Thermodynamic Reasoning in Large Language Mod… | `read` | `domain/thermoqa` | **new** |
| `edm-2026-hybrid-human-ai-tutoring` | Improving Hybrid Human-AI Tutoring by Differentiating Human Tutor Roles Based on Student Needs, arXiv:… | `found` | `practice/equity` | pre-existing |
| `elhaimeur-2026-multiagent-tutoring-latency-cost` | Elhaimeur & Chrisochoides, "Latency and Cost of Multi-Agent Intelligent Tutoring at Scale," arXiv:2604… | `read` | `practice/cost-economics` | **new** |
| `falmagne-aleks-knowledge-assessment` | The Assessment of Knowledge, in Theory and in Practice — Falmagne | `found` | `systems/aleks` | **new** |
| `feng-2023-assistments-two-years` | Feng et al. (2023), "Implementing and Evaluating ASSISTments… over Two Years," AIED 2023 | `read` | `systems/assistments` | **new** |
| `forbus-1999-cyclepad-articulate-virtual-lab` | Forbus, Whalley, Everett, Ureel, Brokowski, Baher & Kuehne (1999). "CyclePad: An articulate virtual la… | `read` | `systems/cyclepad-cycletalk` | **new** |
| `furst-2026-stan-thermo-assistant` | Furst & Venkateshwaran, "Stan: An LLM-based thermodynamics course assistant," arXiv:2603.04657 | `read` | `systems/stan-udel` | **new** |
| `geissler-2025-canonical-to-complex-thermodynamics` | Geißler, Bien, Schöppler & Hertel, "From Canonical to Complex: Benchmarking LLM Capabilities in Underg… | `read` | `domain/diagram-reading`, `domain/utqa` | **new** |
| `ghosh-2024-chatgpt-equitable-education` | Ghosh, S. (2024), "ChatGPT as a Tool for Equitable Education in Engineering Classes," ASEE | `read` | `practice/equity` | **new** |
| `graesser-2005-autotutor-mixed-initiative` | Graesser, Chipman, Haynes & Olney, "AutoTutor: An Intelligent Tutoring System With Mixed-Initiative Di… | `read` | `systems/autotutor` | **new** |
| `graesser-2014-autotutor-and-family-review` | Graesser et al., "AutoTutor and Family: A Review of 17 Years of Natural Language Tutoring," IJAIED | `skimmed` | `systems/autotutor` | **new** |
| `gray-2026-llm-grading-timing` | "Adoption of Large Language Model for Improving Grading Timing in an Engineering Course," ASEE 2026 | `read` | `evaluation/llm-as-judge` | **new** |
| `harness-variance-2026-coding-agents` | "Same Model, Different Harness: Different Coding-Agent Results," arXiv:2608.26218 | `read` | `practice/agent-architecture` | added out-of-band |
| `hashmi-2026-socratic-physics-discourse-taxonomy` | Hashmi & Rebello, "A bottom-up taxonomy of student discourse with a Socratic AI physics tutor," arXiv:… | `read` | `concepts/socratic-tutoring` | **new** |
| `horizon-gap-2026-agent-components` | "The Horizon Gap: Planning, Memory, Execution, Training, and Evaluation for Long-Horizon LLM Agents," … | `read` | `practice/agent-architecture`, `practice/agent-observability` | added out-of-band |
| `kazemitabaar-2024-codeaid` | Kazemitabaar et al., "CodeAid: Evaluating a Classroom Deployment of an LLM-based Programming Assistant… | `skimmed` | `systems/codeaid-toronto` | **new** |
| `keith-2026-ai-chatbots-petroleum-tas` | "Improving Academic Student Success: Using AI Chatbots as Virtual Teaching Assistants," ASEE 2026 | `read` | `concepts/grounding-and-verification` | **new** |
| `kenthapadi-2024-grounding-evaluation-llms` | "Grounding and Evaluation for LLMs: Practical Challenges and Lessons Learned," arXiv:2407.12858 | `found/skimmed` | `concepts/grounding-and-verification` | **new** |
| `kestin-2025-harvard-rct` | Kestin, Miller, Klales, Milbourne & Ponti, "AI tutoring outperforms in-class active learning: an RCT i… | `read` | `evidence/kestin-2025-rct` | **new** |
| `koedinger-2012-kli-framework` | Koedinger, Corbett & Perfetti — the KLI framework | `found` | `concepts/knowledge-components`, `systems/cognitive-tutor` | added out-of-band |
| `kortemeyer-2024-ethel-virtual-ta` | Kortemeyer, G., "Ethel: A Virtual Teaching Assistant," arXiv:2407.19452 | `read` | `concepts/rag-in-education`, `evaluation/llm-as-judge`, `systems/ethel-eth` | **new** |
| `kortemeyer-2024-grading-handwritten-thermo-exam` | Kortemeyer, Nohl & Onishchuk, "Grading Assistance for a Handwritten Thermodynamics Exam," arXiv:2406.1… | `read` | `domain/diagram-reading`, `systems/ethel-eth` | **new** |
| `kou-2026-mechvqa` | MechVQA, arXiv:2605.30794 | `read` | `domain/diagram-reading` | **new** |
| `kulik-fletcher-2016-its-effectiveness` | Kulik & Fletcher (2016), "Effectiveness of Intelligent Tutoring Systems: A Meta-Analytic Review," Revi… | `found/read` | `concepts/vanlehn-2011`, `systems/autotutor` | pre-existing |
| `kumar-2006-cycletalk-tutorial-dialogue` | Kumar, Rosé, Aleven, Iglesias & Robinson (2006). "Evaluating the Effectiveness of Tutorial Dialogue In… | `read` | `systems/cyclepad-cycletalk` | **new** |
| `kweon-2025-llm-virtual-teaching-assistant` | Kweon, Nam, Lim, Hong & Choi, "A Large-Scale Real-World Evaluation of an LLM-Based Virtual Teaching As… | `read` | `concepts/engagement-decay`, `concepts/rag-in-education`, `evidence/kaist-vta-2025`, `practice/cost-economics` +1 | **new** |
| `learnlm-2024-improving-gemini-for-learning` | LearnLM: Improving Gemini for Learning, arXiv:2412.16429 | `read` | `systems/learnlm` | **new** |
| `learnlm-2025-deepmind-report` | LearnLM Team (Google) & Eedi, "AI tutoring can safely and effectively support students: An exploratory… | `found/read` | `systems/learnlm` | **new** |
| `learnlm-2025-gemini-arena-for-learning` | LearnLM Team, Google, "Evaluating Gemini in an Arena for Learning," arXiv:2505.24477 | `read` | `systems/learnlm` | **new** |
| `li-2026-tutor-not-solver-petechat` | Li, Tan, Zakharov, Qiu & Acton, "Tutor, Not Solver: Designing a Guardrailed AI Assistant for Learning … | `read` | `concepts/guardrails`, `systems/petechat-purdue` | **new** |
| `lian-2025-machine-assistant-rag` | "Machine Assistant with Reliable Knowledge: Enhancing Student Learning via RAG-based Retrieval," arXiv… | `found/read` | `concepts/rag-in-education` | **new** |
| `liu-2024-teaching-cs50-with-ai` | Liu, Zenke, Liu, Holmes, Thornton & Malan, "Teaching CS50 with AI" (SIGCSE 2024) | `read` | `concepts/engagement-decay`, `systems/cs50-duck` | **new** |
| `liu-2025-improving-ai-in-cs50` | Liu, Zhao, Xu, Perez, Zhukovets & Malan, "Improving AI in CS50: Leveraging Human Feedback for Better L… | `read` | `systems/cs50-duck` | **new** |
| `liu-2025-teachable-agents-engagement` | Liu et al., "Engagement patterns of middle school students with AI teachable agents in mathematics lea… | `read` | `systems/bettys-brain` | **new** |
| `live-trace-2026-agent-observability` | "Parsing the Stream: A Live Trace Model for Long-Horizon Agents and Their Observers," arXiv:2609.01466 | `read` | `practice/agent-observability` | added out-of-band |
| `loubet-2025-llm-thermodynamic-problems` | Loubet et al., "Using Large Language Models for Solving Thermodynamic Problems," arXiv:2502.05195 / Co… | `skimmed` | `domain/thermo-problem-benchmark` | **new** |
| `loubet-2025-superstudent-thermodynamics` | Loubet et al., "Superstudent intelligence in thermodynamics," arXiv:2506.09822 | `read` | `domain/superstudent-thermodynamics`, `domain/thermo-problem-benchmark` | **new** |
| `luo-2026-aria-multimodal-rag` | Luo, Roy Sarkar & Goswami, "ARIA: Adaptive Retrieval Intelligence Assistant — A Multimodal RAG Framewo… | `read` | `concepts/rag-in-education` | **new** |
| `ma-2014-its-meta-analysis` | Ma et al., "Intelligent Tutoring Systems and Learning Outcomes: A Meta-Analysis," J. Educational Psych… | `found` | `systems/autotutor` | **new** |
| `macina-2025-mathtutorbench` | Macina, Daheim, Hakimi, Kapur, Gurevych & Sachan, "MathTutorBench," arXiv:2502.18940 | `read` | `evaluation/llm-as-judge`, `evaluation/mathtutorbench` | **new** |
| `madsen-2016-resource-letter-rbai1` | Madsen, McKagan & Sayre, Resource Letter RBAI-1, arXiv:1605.02703 | `read` | `evaluation/concept-inventories` | **new** |
| `manggala-2025-steam-table-app-iapws-coolprop` | Development of a Portable Steam Table Application Integrating IAPWS-IF97 and CoolProp | `found` | `domain/property-data-tools` | **new** |
| `mao-2018-deep-learning-vs-bkt` | Mao, Lin & Chi, "Deep Learning vs. Bayesian Knowledge Tracing," JEDM 10(2) 2018 | `read` | `concepts/knowledge-tracing` | **new** |
| `maurya-2024-unifying-ai-tutor-evaluation` | Maurya et al., "Unifying AI Tutor Evaluation: An Evaluation Taxonomy for Pedagogical Ability Assessmen… | `read` | `evaluation/mathtutorbench` | **new** |
| `melumad-2025-llm-vs-websearch-depth-of-learning` | "Experimental evidence of the effects of large language models versus web search on depth of learning,… | `read` | `evidence/llm-synthesis-shallow-learning` | **new** |
| `minn-2020-bkt-lstm` | Minn, "BKT-LSTM," arXiv:2012.12218 | `read` | `concepts/knowledge-tracing` | **new** |
| `naeem-2025-aitutor-evalkit` | AITutor-EvalKit, arXiv:2512.03688 | `read` | `evaluation/mathtutorbench` | **new** |
| `naeem-2025-neuralnexus-bea-shared-task` | Naeem, Ahmad, Ahsan & Iqbal, "NeuralNexus at BEA 2025 Shared Task," arXiv:2506.10627 | `read` | `evaluation/mathtutorbench` | **new** |
| `niousha-2026-missing-evaluation-axis` | Niousha, Boatright Smith, Akram, Brusilovsky, Hellas, Leinonen, DeNero & Norouzi (2026), "The Missing … | `read` | `evaluation/behavioral-evaluation`, `evaluation/llm-as-judge`, `evaluation/mathtutorbench` | **new** |
| `nye-2016-conversations-with-autotutor` | "Conversations with AutoTutor Help Students Learn," IJAIED | `skimmed` | `systems/autotutor` | **new** |
| `oreopoulos-2026-khanmigo-two-year-experiment` | Oreopoulos, P. & Low, N. (2026). "One Click Away: AI Tutoring with Khanmigo in a Two-Year School Exper… | `read/skimmed` | `concepts/engagement-decay`, `evidence/khanmigo-engagement-2026`, `practice/equity`, `systems/khanmigo` | **new** |
| `piech-2015-deep-knowledge-tracing` | Piech et al., "Deep Knowledge Tracing," NeurIPS 2015, arXiv:1506.05908 | `read` | `concepts/knowledge-tracing` | **new** |
| `polverini-2025-mllm-physics-visual-tasks` | Polverini & Gregorcic, "Multimodal LLMs and physics visual tasks," arXiv:2506.19662 | `read` | `domain/diagram-reading` | **new** |
| `premature-commitment-2026-agent-diagnosis` | "When Agents Commit Too Soon: Diagnosing Premature Commitment in LLM Agents," arXiv:2606.22936 | `read` | `practice/agent-architecture` | added out-of-band |
| `protocol-validity-2026-agent-benchmarks` | "Do Agent Benchmarks Measure Capability? Protocol Validity in the Age of Agentic AI," arXiv:2607.22368 | `read` | `practice/agent-observability` | added out-of-band |
| `ready-2026-enterprise-agent-deployment` | "READY or Not: Reliable Enterprise Agent Deployment," arXiv:2609.02095 | `read` | `practice/agent-observability` | added out-of-band |
| `roschelle-2016-online-math-homework` | Roschelle, Feng, Murphy & Mason (2016), "Online Mathematics Homework Increases Student Achievement," A… | `read` | `systems/assistments` | **new** |
| `safe-agents-2026-specification-verification-survey` | "Toward Safe LLM Agents: A Survey of Specification, Verification, and Enforcement," arXiv:2608.14590 | `skimmed` | `practice/agent-architecture` | added out-of-band |
| `scaffolding-collapse-2026-socratic-tutors` | "Mitigating Scaffolding Collapse in Socratic Tutors via Representation Alignment," arXiv:2607.19371 | `read` | `concepts/guardrails` | added out-of-band |
| `sinha-kapur-2021-productive-failure-meta-analysis` | Sinha & Kapur (2021), "When Problem Solving Followed by Instruction Works," RER 91(5), 761–798 | `read` | `concepts/productive-failure` | **new** |
| `smith-2026-modernizing-course-content-llm` | "A Methodological Framework for Modernizing Engineering Course Content with Large Language Models," AS… | `read` | `practice/content-generation` | **new** |
| `su-2026-sketchjudge` | SketchJudge, arXiv:2601.06944 | `read` | `domain/diagram-reading` | **new** |
| `taneja-2024-jill-watson-chatgpt` | Taneja, Maiti, Kakar, Guruprasad, Rao & Goel, "Jill Watson: A Virtual Teaching Assistant powered by Ch… | `read` | `systems/jill-watson` | **new** |
| `tourigny-2026-agentic-mcq-generation` | Tourigny, Acosta Simancas, Onen, Nightingale & MacDonald (2026), "A Rigorous Evaluation of Agentic Lar… | `read` | `practice/content-generation` | **new** |
| `vandesande-2013-bkt-properties` | van de Sande, "Properties of the Bayesian Knowledge Tracing Model," JEDM 5(2) 2013 | `read` | `concepts/knowledge-tracing` | **new** |
| `vanlehn-2005-andes-five-years-evaluations` | VanLehn et al., "Five Years of Evaluations," AIED 2005, pp. 678–685 | `read` | `systems/andes` | **new** |
| `vanlehn-2005-andes-physics-tutoring-system` | VanLehn et al., "The Andes Physics Tutoring System: Lessons Learned," IJAIED 15(3), 147–204 (2005) | `read` | `systems/andes` | **new** |
| `vanlehn-2011-relative-effectiveness` | VanLehn (2011), "The Relative Effectiveness of Human Tutoring, Intelligent Tutoring Systems, and Other… | `read` | `concepts/blooms-two-sigma`, `concepts/knowledge-components`, `concepts/vanlehn-2011` | pre-existing |
| `wang-2024-tutor-copilot` | Wang, Ribeiro, Robinson, Loeb & Demszky, "Tutor CoPilot: A Human-AI Approach for Scaling Real-Time Exp… | `read` | `practice/equity`, `systems/tutor-copilot` | **new** |
| `wasiq-2026-engvqa-vlm-engineers` | Do VLMs Reason Like Engineers? (EngVQA), arXiv:2606.10833 | `read` | `domain/diagram-reading` | **new** |
| `weitekamp-2025-tutorgym` | Weitekamp, Siddiqui & MacLellan, "TutorGym: A Testbed for Evaluating AI Agents as Tutors and Students,… | `read` | `evaluation/mathtutorbench`, `evaluation/tutorgym` | **new** |
| `withhold-answer-2026-supervisor-tutor` | "Teaching a Large Language Model Tutor to Withhold the Answer: A Supervisor Architecture," arXiv:2608.… | `read` | `concepts/guardrails` | added out-of-band |
| `xie-2026-rag-enhanced-llm-ai-tutor` | "Leveraging RAG-Enhanced LLMs for Engineering Education: Design and Evaluation," ASEE 2026 | `read` | `systems/rag-tutor-southeast` | **new** |
| `xu-2026-fairtutor` | Xu, Q., "FairTutor: Equity-Aware Pedagogical LLM Routing for Budget-Constrained AI Tutoring," arXiv:26… | `found/read` | `practice/cost-economics`, `practice/equity` | **new** |
| `yang-2025-gpt5-chart-reading` | Yang & Chen, "GPT-5 Corrected GPT-4V's Chart Reading Errors, Not Prompting," arXiv:2510.06782 | `read` | `domain/diagram-reading` | **new** |
| `yoshida-2026-nodes-early-edges-late` | Yoshida et al., "Nodes Are Early, Edges Are Late," arXiv:2603.02865 | `read` | `domain/diagram-reading` | **new** |
| `zhang-2025-matscibench` | MatSciBench, arXiv:2510.12171 | `read` | `domain/diagram-reading` | **new** |

### Caveat on one artefact

- `bloom-1984-two-sigma-problem.pdf` is the genuine JSTOR scan of *Educational Researcher* 13(6),
  4–16, but it is **image-only** — `pdftotext` yields 1.5 KB (the JSTOR linked-citations page)
  rather than the article body. It needs OCR before it can be quoted from. Every other `.txt` in
  the directory is a real text layer (smallest is 22 KB).

### Held but not traceable to a URL-linked citation

These PDFs are in the directory but no `http(s)` link in the knowledge base resolves to them —
either they are cited without a URL, or they were deposited by another process during this run.

- `agent-memory-2026-longitudinal-evaluation.pdf`
- `calibration-2026-tool-calling-diagnostic.pdf`
- `dual-layer-memory-2026-write-routing.pdf`
- `educlaw-bench-2026-pedagogical-agents.pdf`
- `personalisation-human-robot-collab-review.pdf`
- `rose-2005-npsg-human-tutor.pdf`
- `shinn-2023-reflexion.pdf`
- `socratic-guides-2026-alignment.pdf`
- `wei-2022-chain-of-thought.pdf`
- `yao-2023-react.pdf`

---

## 2. Failed / unfetchable

| Title | URL | Tag | Blocker observed |
|---|---|---|---|
| PhysPort — Thermodynamics Concept Inventory (TCI) instrument page | [https://www.physport.org/assessments/assessment.cfm?A=TCI](https://www.physport.org/assessments/assessment.cfm?A=TCI) | `[read]` | Instrument page, not a paper. The instrument PDF itself sits behind PhysPort educator verification. |
| PhysPort — TTCI-T instrument page | [https://www.physport.org/assessments/assessment.cfm?A=TTCIT](https://www.physport.org/assessments/assessment.cfm?A=TTCIT) | `[read/skimmed]` | Same: instrument page, PDF gated behind educator verification. |
| Biswas, Leelawong, Schwartz & Vye (2005), "Learning by Teaching: A New Agent Paradigm for Educational Software," Applied AI 19(3–4) | [https://www.tandfonline.com/doi/full/10.1080/08839510590910200](https://www.tandfonline.com/doi/full/10.1080/08839510590910200) | `[read]` | Taylor & Francis 403 on `/doi/pdf` and `/doi/epdf` (bronze OA, publisher-only). The one repository mirror, `isis.vanderbilt.edu`, answers "Request Rejected" (WAF). |
| Anderson, Corbett, Koedinger & Pelletier, "Cognitive Tutors: Lessons Learned," JLS 4(2) | [http://act-r.psy.cmu.edu/papers/Lessons_Learned.html](http://act-r.psy.cmu.edu/papers/Lessons_Learned.html) | `[read]` | Not blocked — but the source *is* an HTML page (114 KB, fetches fine); no PDF artefact exists at that host, so nothing to store under the papers rule. |
| Penn State Pure record for the Midkiff/Litzinger Thermodynamics Concept Inventory paper | [https://pure.psu.edu/en/publications/development-of-engineering-the…](https://pure.psu.edu/en/publications/development-of-engineering-thermodynamics-concept-inventory-instr-2/) | `[skimmed]` | Pure record page carries no fulltext bitstream; the underlying IEEE FIE 2001 paper is closed. |
| Pardos, Tang, Anastasopoulos, Sheel & Zhang (2023), "OATutor: An Open-source Adaptive Tutoring System…," CHI 2023 | [https://dl.acm.org/doi/10.1145/3544548.3581574](https://dl.acm.org/doi/10.1145/3544548.3581574) | `[skimmed]` | ACM DL 403 on `/doi/pdf` even with Referer, despite CC-BY gold OA. OpenAlex and Unpaywall list no repository mirror. |
| Porto et al. (2025), "A Systematic Literature Review of AI-Driven Intelligent Tutoring Systems in Engineering Education," IEEE Access | [https://doi.org/10.1109/access.2025.3626473](https://doi.org/10.1109/access.2025.3626473) | `[untagged]` | IEEE Xplore returns HTTP 502 / challenge to scripts. Gold OA but DOAJ lists no mirror — ieeexplore is the only host. |
| Midkiff, Litzinger & Evans (2001), "Development of Engineering Thermodynamics Concept Inventory instruments," IEEE FIE | [https://ieeexplore.ieee.org/document/963691](https://ieeexplore.ieee.org/document/963691) | `[found]` | IEEE Xplore blocked, and the paper is genuinely closed (Unpaywall `is_oa=false`). No repository copy exists. |
| "Assessment in CS50 with AI: Leveraging Generative AI for Personalized Student Evaluation" (SIGCSE TS 2025) | [https://doi.org/10.1145/3641555.3705061](https://doi.org/10.1145/3641555.3705061) | `[found]` | ACM DL paywall — genuinely closed (Unpaywall `is_oa=false`). Not among the PDFs listed on cs.harvard.edu/malan/publications. |
| D'Mello & Graesser, "AutoTutor detects and responds to learners' affective and cognitive states" | [https://www.academia.edu/568630/AutoTutor_detects_and_responds_to_l…](https://www.academia.edu/568630/AutoTutor_detects_and_responds_to_learners_affective_and_cognitive_states) | `[found]` | academia.edu login wall. No OA mirror found via OpenAlex / Semantic Scholar / Memphis IIS. |
| Goel & Polepeddi (2018), "Jill Watson: A Virtual Teaching Assistant for Online Education" | [https://dilab.gatech.edu/publications/](https://dilab.gatech.edu/publications/) | `[found]` | The DILab publications index is a JS app with zero PDF links; the 2018 chapter is closed (Routledge). **Mitigated:** the 2024 successor, arXiv:2405.11070, is held as `taneja-2024-jill-watson-chatgpt.pdf`. |

---

## 3. Cited web sources that are not papers

78 further cited URLs are news articles, vendor blogs, institutional pages, product
documentation, GitHub repositories, HuggingFace datasets or podcast episodes. There is no PDF
artefact to hold for these, so the "download every cited paper" rule does not apply to them.

Breakdown by host (top 12): `github.com` ×11, `psu.edu` ×4, `qrg.northwestern.edu` ×4, `insidehighered.com` ×3, `huggingface.co` ×2, `doaj.org` ×2, `en.wikipedia.org` ×2, `aleks.com` ×2, `developerdocs.instructure.com` ×2, `ai.psu.edu` ×2, `cmu.edu` ×2, `its.umich.edu` ×2.

---

## 4. Counts

| | Count |
|---|---|
| Unique cited URLs across `knowledge/**` + `docs/02-bibliography.md` | **202** |
| — resolving to a paper/report artefact | **124** |
| — non-paper web sources (news, blogs, repos, docs, datasets) | 78 |
| Paper-type URLs now held as a verified PDF | **113** |
| Paper-type URLs still blocked | **11** |
| Distinct PDFs in `course-materials/papers/` | **109** |
| — of which fetched in this audit | 82 |

Coverage of paper-type citations: **113/124** = 91%.

Verification tags across all cited URLs: `[read]` 104, `[skimmed]` 46, `[found]` 44, `[untagged]` 11, `[abstract-only]` 2.

---

## 5. Acquisition recipes that worked (for next time)

- **arXiv** — `https://arxiv.org/pdf/<id>` direct, no UA tricks needed. 57 papers came from here.
  Bulk metadata for filenames: `https://export.arxiv.org/api/query?id_list=<comma-separated>` —
  note **https**, the plain-http endpoint returns nothing in this sandbox.
- **ASEE** — `peer.asee.org/<id>.pdf` serves the file; `peer.asee.org/<id>` gives a Cloudflare
  challenge. 9 ASEE papers acquired this way.
- **ERIC** — `eric.ed.gov` search is blocked, but `files.eric.ed.gov/fulltext/<ID>.pdf` is wide open,
  and `https://api.ies.ed.gov/eric/?search=title%3A%22…%22&format=json` finds the ID. This is how
  Graesser 2014, Nye 2016 and Roschelle 2016 were recovered after the publisher 403'd.
- **Springer** — `link.springer.com` 403s, but **`rd.springer.com/content/pdf/<doi>.pdf`** with a
  `Referer` header works. Recovered Betty's Brain (IJAIED 2016).
- **ETH DSpace** — `/server/api/pid/find?id=hdl:<handle>` **with `-L`** (it 302s), then
  `/core/items/<uuid>/bundles` → ORIGINAL → `/bitstreams` → `_links.content.href`.
- **Nature / npj / Sci Rep** — append `.pdf` to the article URL.
- **OA discovery** — OpenAlex (`api.openalex.org/works/doi:<DOI>`) and Unpaywall
  (`api.unpaywall.org/v2/<DOI>?email=…`) for `best_oa_location` and the full `locations` array;
  Semantic Scholar (`api.semanticscholar.org/graph/v1/paper/DOI:<DOI>?fields=openAccessPdf`) as a
  cross-check. All three answer scripts fine.
- **OJS journals** — landing page `…/article/view/<sub>/<gal>` → PDF at `…/article/download/<sub>/<gal>`.

Confirmed hard-blocked in this environment: IEEE Xplore, Elsevier, Springer `link.` host, Sage,
Taylor & Francis, ACM DL, figshare/KiltHub `ndownloader` (202 then 403), academia.edu,
`isis.vanderbilt.edu` (WAF), `digitalcommons.library.umaine.edu`.

