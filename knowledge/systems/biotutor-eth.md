# bioTutor — ETH Zurich

**Type:** system
**One line:** ETH's second course-specific tutor — **open-source, with the full system prompt
published** — deployed for **23 weeks** to a 407-student cohort with **10,465 interactions**, and
built on a **generate-your-own-answer-first** interaction pattern that is the closest thing in
this base to productive failure shipped as a UI.
**Why we care:** It is the longest single-course deployment here, **the source and the prompt are
both public**, and its interaction design — *state your question, state your answer, then get
feedback* — is [the primitive four other studies independently pointed at](aiplato-uta.md),
implemented and run for a year.

> **Verification: `[read — full text, 18 pp., 2026-09-03]`.** Local copy:
> `course-materials/papers/biotutor-eth-2026.pdf` (+ `.txt`). ⚠ **This node was `[abstract only]`
> and overstated the deployment in one important way — see the ⚠⚠ correction below.**

Tobler, S. & Köhler, K. (2026). *"A Lecture-Specific AI-Based Tutor for Higher Education:
Pedagogical Design and Empirical Evaluation."* **Educ. Sci.** 16(5), 812.
[DOI 10.3390/educsci16050812](https://doi.org/10.3390/educsci16050812). **Institute for Biomedical
Engineering, ETH Zurich.** Gold OA. Funded by the **ETH Innovedum Fund** (4453); ethics
**23 ETHICS-277**.

⭐ **Source code: [github.com/samueltobler/bioTutor](https://github.com/samueltobler/bioTutor/)** —
this node's top open question is now answered.

⭐ **The full instruction prompt is in Appendix A and reproduced below.** Almost nobody publishes
theirs.

---

## ⭐⭐⭐ The interaction design, which is the reason to care about this system

Most "Socratic tutor" claims are a line in a system prompt. **bioTutor enforces the sequence in
the user interface:**

1. **The student formulates their own question.** Not a menu, not a problem the system chose —
   *"students' own open questions form the starting point of the interaction."*
2. **If the question is clear and course-relevant, the student must supply their own answer
   first.**
3. **Only then** does the tutor give *"concise feedback"*, refuse to reveal the answer, and ask a
   follow-up question grounded in the lecture materials.
4. Explanations come **after** the follow-up dialogue, not instead of it.

> *"The enforced requirement that students formulate their own questions, propose answers, and
> then engage in a follow-up Socratic dialogue distinguishes the bioTutor from chatbots like
> ChatGPT which typically provide direct answers without motivating students to first reflect on
> their understanding."*

**This is [aiPlato's "Evaluate My Work"](aiplato-uta.md) made mandatory rather than optional, and
it is [productive failure](../concepts/productive-failure.md) as an interface constraint.** The
authors cite the lineage explicitly — Schwarz & Bransford (1998), and
[Sinha & Kapur (2021)](../concepts/productive-failure.md): *"working on (own) problems instead of
first receiving instruction significantly enhances learning, **even if the correct solution is not
found**."*

⭐ **It is also [VanLehn's completion mechanism](../concepts/vanlehn-2011.md) turned into a
turn-taking rule.** The student cannot receive the reasoning without first attempting it.

⚠⚠ **But nobody checked that the tutor actually behaved this way:**

> *"The chatbot was tested before deployment to examine whether it showed the expected behavior.
> Yet, **the consistency of this interaction pattern was not systematically quantified across all
> recorded conversations.**"*

**10,465 interactions were logged and none were audited for compliance with the design.** That is
precisely the gap [CS50 measured at 22% code leakage across 10 million messages](cs50-duck.md).
**The conversations exist and are analysable. This is a free, high-value replication for us —
and it is exactly the audit our own tutor will need.** → [guardrails](../concepts/guardrails.md)

### ⭐ The prompt, verbatim (Appendix A)

> *As a friendly Socratic biology teacher, evaluate the student's input based on factual
> correctness, providing concise and relevant feedback. Encourage students expressing uncertainty
> while refraining from revealing the answer. **Do not directly tell the answer, even if students
> ask you to provide it.** Rather motivate them to think again critically. Craft follow-up
> questions to deepen understanding, **using information from provided files without introducing
> terms not present in them.** Use natural conversational language and do not add references and
> do not cite files.*
>
> *Steps: 1. Evaluate the student's input for factual accuracy. 2. Provide concise, encouraging
> feedback and shortly elaborate on the concept. 3. Create a follow-up question based on
> information in the provided files. 4. Avoid using terms not found in the files or referencing
> file names in your response.*
>
> *Output Format: **Limit responses to 100 words.** Use natural conversational language and no
> emojis. **Use the same language as the user.***

Three things worth noting:

1. ⭐ **"Limit responses to 100 words."** A hard length cap, and it is the one design choice that
   answers [LearnLM being called "patronizing" and UIC students wanting succinctness](learnlm.md).
2. ⭐ **"Using information from provided files without introducing terms not present in them"** —
   a *vocabulary* constraint, not just a content one. It is the cheapest available approximation of
   course-level appropriateness, which is [the failure Tutor CoPilot reported](tutor-copilot.md)
   as suggestions being *"too smart."*
3. ⚠ **"Do not add references and do not cite files."** They deliberately **suppress provenance**,
   which is the opposite of every architecture in [§V](../PAPER.md). No rationale is given. Given
   that [showing sources buys accuracy but not depth](../evidence/llm-synthesis-shallow-learning.md),
   this is arguably defensible and it is certainly untested.

---

## ⚠⚠ Correction: 407 is the enrolment, not the user count

**This node previously read as though 407 students used the tutor. They did not.**

| | |
|---|---:|
| Enrolled in the lecture | **407** |
| Completed end-of-semester feedback | 316 |
| ⭐ **Self-reported using the chatbot** | **94 (29.7% of respondents)** |
| **Completed the acceptance questionnaire — the N behind every result below** | **73** |

> *"Since data were recorded anonymously, **it was not possible to determine how many individual
> users actually used the chatbot.**"*

**Every satisfaction number in this paper rests on 73 self-selected respondents.** The authors are
scrupulous about this — they call 30% *"the proportion of feedback respondents who self-reported
chatbot use"* and say it *"should not be interpreted as a verified usage rate for the full
cohort."* **The summaries are not.**

⭐ **Read the 30% against the promotion effort, because that is the real finding.** The tool got
**a five-minute slot in one non-compulsory lecture**, a link in the LMS, and a written guide.
*"Students were not further reminded of the existence of the tool, and no extrinsic motivation for
its use was provided (e.g., no integration into lectures, grade bonuses, or specific exercises)."*

**Thirty percent uptake for five minutes of promotion and zero integration is, in this literature,
a good number** — [KAIST's 14-week deployment lost 50%](../evidence/kaist-vta-2025.md) and
[CS50 reached 97% with the tool wired into the course](cs50-duck.md). **The variable is
integration, and this is a clean low-integration data point.**
→ [engagement decay](../concepts/engagement-decay.md)

## ⭐ The best engagement curve in this knowledge base

| Phase | Weeks |
|---|---|
| In-person semester | 13 |
| Learning + exam-preparation phase | 7 |
| After the exam, tool still live | 3 |

**10,465 student-formulated interactions across 1,026 conversations. Median 6 interactions per
conversation** (mean 10.2 ± 11.6) — so the median student went six turns deep, which is a real
dialogue rather than a lookup. Roughly **11 conversations per self-reported user** *(descriptive
only; the anonymous logs cannot be linked to respondents)*.

Shape of the curve:

- **Flat through the semester** at a median of **4 conversations per day**
- ⭐ **Two spikes, both at the formative "learning objective checks"** — mid- and end-of-semester
- **A large, sustained rise before the February summative exam**
- ⭐ **Still used in March**, after the lecture had ended and *"students were aware that the
  materials underlying the chatbot's knowledge foundation were not specific to any other course"*

**Assessment events drive usage.** That is the same signal as
[aiPlato's within-assignment attrition](aiplato-uta.md) and
[Khanmigo's engagement collapse](khanmigo.md) read from the other side: **the tutor is used when
there is something to be assessed on.** If our deployment is not attached to an assessment
calendar, the curve above says the plateau will be low and flat.

## ⚠ What it measures — and what that is worth

They built **edTAM**, an education-adapted extension of the Technology Acceptance Model (TAM2;
Venkatesh & Davis 2000), with usefulness and ease-of-use from **UMUX-Lite** plus three added
constructs — learning relevance, output quality, result demonstrability.

⚠⚠ **It is six items on a 5-point Likert scale, and three of the constructs are measured by a
single item each.** The authors say so:

> *"As these constructs were each assessed with a single item, they should be interpreted as
> **exploratory indicators rather than robust construct measurements**."*

No correction for multiple testing was applied, *"as the analysis was exploratory and
descriptive."*

**Results (n = 73):**

| | |
|---|---:|
| Combined usability + usefulness | **median 4.5 / 5** |
| Found it straightforward to use | **> 85%** |
| Capabilities met their requirements | **> 75%** |
| ⭐ **Follow-up questions helped deepen understanding** | **77%** |
| Answers helped clarify open questions | **~70%** |
| ⚠ **Said the time invested did not pay off** | **23%** |
| ⭐ **Would want a similar tool in other lectures** | **> 80%** |

⭐ **The last row is the one that matters, and the authors' reading of it is right:** these are
students at a technical university with free ChatGPT and Gemini in the next tab, and **over 80% of
users still want a course-specific tutor in their other lectures.** That is a preference for
*course grounding*, expressed against a strictly better general model.

### ⭐⭐ The three student quotes, which are worth more than the percentages

> **In favour:** *"I find it very useful that it asks follow-up questions, as this allows one to
> test one's knowledge."*

> **Against, the comfort trap:** *"for some questions I find this [asking of explanations]
> somewhat unnecessary and would prefer to simply receive an answer."*

> ⭐⭐ **Against, and this one is a real design defect:** *"the follow-up questions are not useful
> when one cannot answer one's own question and the chatbot asks for the solution."*

**That third quote names the failure mode of the generate-first primitive, and nothing else in
this knowledge base does.** If the student genuinely does not know, "what do *you* think?" is a
dead end — the interaction stalls at exactly the moment help is needed most. It is the
[assistance dilemma](../concepts/vanlehn-2011.md) reported from the student's side.

**Design consequence: a generate-first tutor needs a detected floor.** After *n* failed
elicitations, or on an explicit *"I don't know,"* it must switch modes — to a worked analogue, a
prerequisite check, or a partial reveal. **bioTutor has no such escape hatch, and its own users
found the hole.** → [Socratic tutoring](../concepts/socratic-tutoring.md),
[productive failure](../concepts/productive-failure.md)

⚠ **And [TUM showed why high acceptance is not reassurance](../evidence/tum-dissociation-2025.md):
students rated unrestricted ChatGPT as easier and more helpful than the scaffolded tutor that
actually preserved their motivation.** A median of 4.5 is compatible with a tool that teaches
nothing.

## ⚠⚠ No learning outcome, and the reason given is an ethical one

> *"The study does not provide evidence on whether the bioTutor influenced learning outcomes,
> since a quasi-experimental setting that would have allowed comparison between different student
> groups was not feasible in the present course context… **Excluding some students from a
> potential learning opportunity for exam preparation might have created inequality, which we
> deliberately aimed to avoid.**"*

**This is the second paper in this batch to decline to randomise on equity grounds** — the
[EDM 2026 hybrid study](hybrid-human-ai-tutoring.md) says the same thing about withholding
proactive tutoring from struggling students.

⭐ **That is a pattern worth naming, because it is the reason this literature has so few control
groups, and because it has a known answer.** [aiPlato's IRB shape](aiplato-uta.md) is the model:
**nobody was excluded from using the platform — consent governed the data, not the access.** A
within-subject crossover ([as Kestin ran](../evidence/kestin-2025-rct.md)) gives every student
both conditions and still yields a causal estimate. **The ethical objection is real and it is
answerable by design, and we should say so in our own protocol.** → [IRB](../../admin/irb.md)

⚠ Also unmeasured: no demographic data at all, so nothing on prior knowledge, background or
language proficiency.

## The architecture — deliberately, almost provocatively simple

| Layer | Choice |
|---|---|
| App framework | **RShiny**, hostable locally or on shinyapps.io |
| LLM + retrieval | ⚠ **OpenAI Assistants API**, with lecture materials uploaded as the knowledge base |
| Datastore | ⚠ **Google Sheets**, via API |
| Identity | **None.** Random session UID + timestamps. No login; access by shared link |
| Dashboard | A second RShiny app, password-protected, multi-course, reading the same sheet |

**They chose simplicity over sophistication on purpose** — *"we aimed to create a technically
simple solution to ensure transferability to other courses without significant adaptation
efforts."*

⚠ **Three consequences worth being clear-eyed about:**

1. **Retrieval is OpenAI's, not theirs.** There is no chunking strategy, no reranker, no hybrid
   search — compare [Iris's pipeline](../evidence/tum-dissociation-2025.md). And **an off-the-shelf
   OpenAI Assistant is exactly the baseline [Jill Watson beat 76.7% to 31.3%, with 16.5% harmful
   answers](jill-watson.md).** bioTutor has no verification layer of any kind.
   → [grounding and verification](../concepts/grounding-and-verification.md)
2. **Google Sheets is the database.** They flag *"a slower API and rate limits, which may take
   effects when working with large student cohorts simultaneously"* — and separately note server
   outages and long waits under load as a possible reason for the 23% "not worth the time."
   ⭐ **[Latency is an effect-size variable](../concepts/vanlehn-2011.md): one minute of lag took
   an ITS from d = 0.31 to d = 0.01.**
3. **The Assistants API is being retired.** They name the migration to the Responses API as
   outstanding maintenance work. → [agent architecture](../practice/agent-architecture.md)

## ⭐ The instructor dashboard — a five-way convergence, and nobody has validated it

The dashboard computes usage statistics automatically and, **on a manually-triggered button**,
runs a batch of Chat Completions analyses producing:

- **weekly summaries** of all interactions
- a list of the **most frequently asked questions**
- ⭐ a **question-type analysis** — e.g. whether students asked about *definitions* or about
  *mechanisms* (following Tawfik et al. 2020)

| System | Instructor-facing feature |
|---|---|
| [Stan](stan-udel.md) | Question mining and confusion detection from lecture transcripts — *its only real contribution* |
| [PeteChat](petechat-purdue.md) | Content upload, provenance, tone config, alignment metrics |
| [Ethel](ethel-eth.md) | Planned instructor self-serve upload platform |
| [aiPlato](aiplato-uta.md) | Usage logs and analytics at assignment and problem level |
| **bioTutor** | **Weekly AI summaries, top questions, question-type classification** |

**Five systems, independently, plus
[a systematic review naming dual-user support as the standing gap](../practice/institutional-landscape.md).**

⚠⚠ **And now the sharpening the full text provides: not one of them has been evaluated.** The
authors are explicit twice over:

> *"Whether and how lecturers used these insights to adapt their teaching **remains to be
> investigated**."*

> *"The lecturer dashboard should be understood as **a prototype for aggregated instructional
> insight rather than as a fully validated learning analytics tool**. Although the dashboard
> provides AI-generated summaries… **the accuracy, usefulness, and pedagogical reliability of
> these summaries were not systematically evaluated.**"*

**So the convergence is five teams building the same feature and zero teams checking that it
works.** ⚠ *And these are LLM-generated summaries of student conversations — precisely the task
[LLM-as-judge work says models are unreliable at](../evaluation/llm-as-judge.md).*

⭐⭐ **That is an opening, not a discouragement.** *"Do instructors act on the dashboard, and are
its summaries accurate?"* is a small, cheap, publishable study that needs **no student-facing risk
and no new system** — the authors even specify the method: *"expert ratings or comparisons with
human-coded conversation analyses."* **It may be the single most tractable contribution available
to this project.**

## ⭐ Their practical implications, which read as a deployment checklist

1. **Introduce it in person, early, and explain the didactic design** — *"someone looking for a
   tool providing quick answers… will not achieve their goal with the bioTutor and thus, might be
   disappointed."* The 23% dissatisfaction is partly an expectations mismatch.
2. **Ship a written guide** students can consult later.
3. **Provide a list of conversation-starter questions** to ease the first interaction. ⭐ Non-obvious
   and cheap: a tutor that opens with *"ask me anything"* puts the hardest step first.
4. ⚠⚠ **Budget for content preparation, which was their main bottleneck.** *"One of the main
   challenges in designing the content-specific bioTutor was the preparation of input material
   that comprehensively matched the lecture content."* Specifically: **complicated figures in
   slide sets require written descriptions**, and **lecture transcripts require human revision**
   before use as grounding material. → [content generation](../practice/content-generation.md),
   [diagram reading](../domain/diagram-reading.md) — *in thermodynamics the figures are T–s and
   P–v diagrams, so this cost is higher for us, not lower.*

## What we should take

1. ⭐⭐ **Read the repo and the prompt before writing anything.** A deployed, year-tested,
   open-source course tutor with its instruction prompt published is worth an afternoon.
2. ⭐ **Adopt the generate-first turn structure — and build the escape hatch bioTutor lacks.**
   Their own students found the hole; fixing it is a contribution.
3. ⭐ **Steal the 100-word cap and the vocabulary constraint.** Both are one line of prompt and
   both target measured failure modes.
4. **Build the instructor dashboard — and then evaluate it.** Five systems have built one; nobody
   has validated one.
5. **Do not repeat their evaluation.** Run a TAM instrument if you like, but as a *secondary*
   measure beside a [distal, unassisted outcome](../evaluation/concept-inventories.md).
6. ⚠ **Do not accept "randomising would be unfair" as a reason to skip a control group.**
   [aiPlato's consent-governs-data-not-access design](aiplato-uta.md) and
   [Kestin's crossover](../evidence/kestin-2025-rct.md) both solve it.

## Open questions

- [x] ~~Where is the source?~~ **[github.com/samueltobler/bioTutor](https://github.com/samueltobler/bioTutor/)**
      — not yet cloned or read.
- [x] ~~What does "didactically structured interaction design" concretely mean?~~ **A UI-enforced
      sequence: student's own question → student's own answer → feedback that withholds the
      solution → follow-up question → explanation last.** Prompt in Appendix A.
- [x] ~~Is this from the same ETH group as [Ethel](ethel-eth.md)?~~ **No.** bioTutor is Tobler &
      Köhler at the **Institute for Biomedical Engineering**, funded by the ETH Innovedum Fund;
      Ethel is the **Rectorate + AI Center**. **Two independent efforts inside one university**,
      which is itself a finding about how institutions actually adopt these.
- [ ] ⭐ **Did the tutor actually follow its own design?** 10,465 logged interactions, never
      audited for compliance. The data *"can be made available upon reasonable request."*
      **Ask for it.** This is the cheapest real study on this page.
- [ ] ⭐ **Are the dashboard's AI-generated summaries accurate?** Unevaluated, by their own
      account, and the authors name the method to evaluate it.
- [ ] What happens at the floor? The student quote about being asked for a solution they do not
      have is the unhandled case, and it is where a **prerequisite check or a worked analogue**
      would go.
- [ ] Does the no-citation choice matter? They suppress provenance deliberately and never test it.
- [ ] Does the generate-first pattern survive a numerical domain? Biology questions are
      answerable in prose; a thermodynamics student's "own answer" may be a half-finished
      derivation. → [knowledge components](../concepts/knowledge-components.md)

## Connects to

- [aiPlato](aiplato-uta.md) — "evaluate my work" as an optional button; bioTutor makes it mandatory
- [Productive failure](../concepts/productive-failure.md) — the theory bioTutor implements as a UI rule
- [The ITS meta-analyses](../concepts/vanlehn-2011.md) — completion, the assistance dilemma, and latency as an effect-size variable
- [TUM dissociation](../evidence/tum-dissociation-2025.md) — why acceptance is not evidence, and the far more elaborate RAG pipeline
- [Ethel](ethel-eth.md) — ETH's other, unrelated tutor
- [Jill Watson](jill-watson.md) — what an unverified OpenAI Assistant scores on course questions
- [CS50 Duck](cs50-duck.md) — the compliance audit bioTutor did not run
- [Stan](stan-udel.md), [PeteChat](petechat-purdue.md) — the dashboard convergence
- [Engagement decay](../concepts/engagement-decay.md) — 23 weeks, and assessments drive the curve
- [LLM-as-judge](../evaluation/llm-as-judge.md) — the dashboard's summaries are exactly this task
- [Institutional landscape](../practice/institutional-landscape.md)

## Sources

- [Tobler & Köhler (2026), "A Lecture-Specific AI-Based Tutor for Higher Education: Pedagogical Design and Empirical Evaluation," *Educ. Sci.* 16(5), 812](https://doi.org/10.3390/educsci16050812) `[read — full text, 18 pp., 2026-09-03]` · gold OA. Local: `course-materials/papers/biotutor-eth-2026.pdf`. Earlier attempts hit MDPI's bot block; [the DOAJ record](https://doaj.org/article/6d7b154181de4bc1b74983fb1dbb4a85) carried the abstract.
- [bioTutor source code, GitHub](https://github.com/samueltobler/bioTutor/) `[found]` — ⭐ chatbot and lecturer dashboard, RShiny. **Not yet read.**
- Interaction logs and survey responses — *"not publicly available but can be made available upon reasonable request."* `[found]` — ⭐ **worth requesting**
</content>
