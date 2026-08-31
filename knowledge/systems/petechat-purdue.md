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
