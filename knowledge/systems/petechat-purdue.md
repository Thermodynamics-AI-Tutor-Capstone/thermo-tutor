# PeteChat — Purdue

**Type:** system
**One line:** A course-specific, guardrailed AI tutor built by fine-tuning open-source
LLMs on course data, deployed in Purdue's ECE 20875 in Spring 2025.
**Why we care:** The closest **methodological** sibling to our project — a student-facing,
single-course tutor with published design rationale and an explicit "tutor, not solver"
stance.

> **Verification: `[read]` — full text, 2026-08-31.** Important correction: this is a
> **design case, not an experimental study.** The evidence base is four expert interview
> sessions and a 284-message baseline corpus. It has **no student outcome data**. This node
> previously implied a large-scale deployment evaluation; it isn't one.

## What it is

Belle Li, Lily Tan, Wei Zakharov, Qiang Qiu, Colby Ben Acton — Purdue University
(Learning Design & Technology, Libraries, Engineering Education, ECE). arXiv:2606.09845.

A **course-aligned AI tutor** built on a **locally hosted Llama-3 family model**,
fine-tuned on Purdue content with **LoRA/QLoRA** on Purdue's **Gilbreth GPU cluster**, plus
RAG over course materials.

Architecture: a **mixture-of-experts-inspired router** dispatches each query to one of four
modes — **exam generation, MCP tools, multimodal support, or RAG Q&A**. The RAG pipeline runs
query rewriting → multimodal retrieval → shared-vector embedding → generation with tutor
guardrails.

Framed as **design-based research (DBR)** across four development phases, explicitly
prioritizing "situated design reasoning" over outcome measurement.

Institutionally: funded by Purdue's **Innovation Hub Funding Program: Teaching & Learning in
an AI-Rich Environment**, with the Center for Instructional Excellence, Purdue Libraries, and
RCAC. That funding-and-partners pattern is a useful template for the
[PSU AI Center of Excellence](../practice/psu-ai-landscape.md) route.

## The eight design principles — the actual deliverable

These are concrete, transferable, and the reason to read this paper:

1. **Tutor, not solver.** Default to hinting and scaffolding; avoid direct answers. Teach
   *how to think* — debug explanations, step-by-step reasoning.
2. **Align to the course.** Ground responses in instructor-provided materials **and show
   provenance**; add freshness disclaimers for logistics to protect instructors.
3. **Respect academic integrity.** Guardrails and reminders on homework; encourage students
   to read and follow instructions.
4. **Reduce TA overhead.** Automate clarity (summaries of instructions), regrade explanations
   from rubrics, handle repeat questions consistently.
5. **Design for clarity and momentum.** Open sidebar with per-assignment *"Try asking…"*
   cards; concise, visual, readable answers.
6. **Flexible control for staff.** Instructors upload/update content, set tone, review
   alignment metrics — **without code**.
7. **Trust through transparency.** Show sources, note uncertainty, offer share/confirm
   actions so students can verify with peers or TAs.
8. **Time-aware support.** Study plans and mock quizzes scoped to available time and
   upcoming exams.

**The starter-prompt mechanism (5) is quietly clever**: *"Try asking…"* cards are
**auto-generated from syllabus metadata** — assignment names, due dates, topic tags — and
instructors can override them. A usage-analytics layer tracks which prompts get picked and
feeds that back. That's a cheap, concrete answer to the
[first-session problem](../concepts/engagement-decay.md), where KAIST's disappointed
low-frequency users are lost.

## ⭐ The baseline corpus — the most useful data in the paper, and it is bleak

Before the guardrails and SRL scaffolds were added, they logged **284 messages / 31 conversations**
from **ECE 20875, Fall 2025**, across three late-semester contexts under genuine assessment
pressure: exam prep (47 student / 47 bot), homework debugging (50/50), open-ended mini-project
(45/45). Dual coding scheme, second coder on 21.1% of the corpus, **Cohen's κ = .82**.

**Student behaviour (n = 142 student messages):**

| Code | Overall | Exam prep | Homework | Mini-project |
|---|---|---|---|---|
| A3 Adaptive help-seeking | 18.3% | 6% | 28% | 20% |
| A4 Excessive / broad help-seeking | 14.1% | 9% | 10% | 24% |
| ⚠ **A8 Boundary testing / system probing** | **13.4%** | 11% | **22%** | 7% |
| A6 Self-monitoring | 13.4% | 2% | 14% | 24% |
| A1 Goal setting | 12.7% | **38%** | 0% | 0% |
| A0 Off-task | 10.6% | 11% | 10% | 11% |
| A5 Direct answer / solution seeking | 7.0% | 6% | 8% | 7% |
| ⚠ **A9 Self-evaluation / reflection** | **1.4%** | 2% | 2% | **0%** |
| ⚠⚠ **A7 Hint utilization / scaffolding** | **0.0%** | 0% | 0% | 0% |

**Read the last two rows.** Hint utilisation was **literally zero across all 284 messages**, and
self-reflection was 1.4%. The authors' own conclusion: *"even when students were using the system
under real course pressure, there was little evidence that the interaction was eliciting the
forethought, monitoring, or reflection behaviors"* the design was aiming at.

**This is the same finding as [CycleTalk's 14% help-request rate](cyclepad-cycletalk.md), twenty
years later, with a language model instead of scripted dialogues.** The scaffolding is built, it
is available, and students do not take it. Any design that assumes students will pull help is
designing for a behaviour that has never been observed.
→ [engagement decay](../concepts/engagement-decay.md)

**And boundary testing at 22% in the homework context** is the number to quote whenever someone
suggests a system prompt will hold the line. Roughly one homework message in five was a probe for
answer-giving behaviour, and the baseline system **sometimes complied** (B2 Direct Solution /
Over-Solving, 4.2%, present in all three contexts).
→ [why pedagogy in the system prompt fails](../concepts/guardrails.md)

**System response alignment (n = 142 bot messages): aligned 64.1%, misaligned 5.6%, N/A 30.3%.**
Hint-first scaffolding (B1) ran **0% in exam prep**, 40% in homework, 64% in the mini-project —
the assistant behaved most like a tutor exactly where the stakes were lowest.

⚠ **One widely-quotable claim here is testimony, not measurement.** The paper reports that TAs
*"confirmed that heavy GPT reliance is inflating homework scores (north of 95%) while exam
performance drops."* That is TA impression reported in an interview, with no gradebook analysis
behind it. It is a plausible and important pattern — and it is **exactly the study we could
actually run** — but it is not evidence yet.
→ [assessment validity](../practice/assessment-integrity.md)

## Two mechanisms worth stealing beyond the list

**Reverse prompting and judgment-of-learning (JOL) micro-checks.** PeteChat periodically
turns the question back on the student and asks them to rate their own understanding.
Explicitly framed as metacognitive support and part of the assessment-aware guardrails. This
is one of very few concrete implementations of metacognitive scaffolding we have found in a
deployed LLM tutor.

**Uncertainty expression as hallucination mitigation.** Early trials showed the model
hallucinating references and overconfidently stating incorrect facts. Their fix: prompt it to
**cite knowledge-base sources when possible and to say "I'm not sure"** or point at where to
look, rather than fabricate. They report this "reduced blatantly incorrect answers" without
eliminating them. Compare CS50's observation that
[AI's confident tone when wrong is the real problem](cs50-duck.md).

## What it does not have

- **No student outcome data.** None. It is a design case.
- Evidence base: **four expert sessions (n=4)** with TAs and UX/developer stakeholders, plus
  a directed content analysis of a **284-message pre-guardrail baseline corpus**
- No knowledge tracing, no mastery model
- Deployment scale and retention are not reported in this paper

## Revised position

PeteChat is **the best available source of design principles** for a course-aligned
guardrailed tutor, and **not** a source of evidence that such tutors work. Cite it for the
eight principles and the JOL idea; do not cite it for effectiveness.

## Open questions

- [x] ~~Which base models?~~ Llama-3 family, LoRA/QLoRA fine-tuned on Purdue content.
- [ ] What did the fine-tuning actually buy over prompting alone? Unmeasured.
- [ ] Are there follow-up papers with Spring 2025/2026 deployment data? **Search — that's
      where the outcome evidence would be.**
- [ ] Did the guardrails hold under pressure? No defection testing reported.
- [ ] Do the JOL micro-checks change behaviour, or are they ignored?

## Connects to

- [CS50 Duck](cs50-duck.md) — same "won't spoil the answer" commitment, much larger scale
- [Stan](stan-udel.md) — same course-tutor pattern, our domain
- [guardrails](../concepts/guardrails.md) — PeteChat is a guardrail design case study
- [Cogniti](cogniti-sydney.md) — the alternative: don't build a tutor, build a tutor factory

## Sources

- [Li, Tan, Zakharov, Qiu & Acton, "Tutor, Not Solver: Designing a Guardrailed AI Assistant for Learning in Higher Education: A Design Case of PeteChat," arXiv:2606.09845](https://arxiv.org/abs/2606.09845) `[read]` — full text
