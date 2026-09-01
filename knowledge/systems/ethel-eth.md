# Ethel — ETH Zurich

**Type:** system
**One line:** A university-sponsored virtual teaching assistant built by ETH Zurich's Rectorate
and AI Center, notable because it was **built and costed for thermodynamics**, and because its
authors publish their failures.
**Why we care:** It is the closest thing to an institutional peer for our project — same domain,
same "sponsored by the university, not a startup" posture — and it puts a real number on what
running one costs.

> **Verification: `[read]` — full text (3 pp.), 2026-09-01.**

Kortemeyer, G. — *"Ethel: A Virtual Teaching Assistant,"* arXiv:2407.19452, ETH Zurich Rectorate
and AI Center, submitted to *American Journal of Physics*.

## What it is

Three components, not one chatbot:

1. **A course chatbot** over course PDFs via **RAG** — LangChain plus OpenAI ada embeddings,
   which the author says is *"about 400 lines of code."* No fine-tuning: *"Instead of complex
   tuning, these materials are stored in a reference database."*
2. **Homework feedback**, with the problem text and the sample solution injected into the prompt.
3. **Exam grading**, with the rubric or sample solution injected.

**GPT-4 via Azure**, chosen because Switzerland is multilingual and the course script is German.
The author notes plainly that open-weight models would serve a monolingual English deployment, and
that the reason for the cloud is not capability but operations: *"running any LLM… round-the-clock
and at-scale currently requires commercial cloud-based platforms; while university high-performance
computer clusters might have the necessary GPU-power, they are usually designed for batch
operation."* **Data privacy is handled by the university's agreement with Azure AI Services** —
the same institutional-contract route [PSU takes with AI Studio](../practice/psu-ai-landscape.md).

The retrieval works on vague reference: a student asking about *"that example of the table with
the lights"* was correctly resolved against a **300-page German lecture script**, and the system
held its place when the student tried to derail it onto the Doppler shift.

## ⭐ The number nobody else publishes

> **$7.50 per student per course per semester** (Azure AI Services, actual operating cost).

Set against [Tutor CoPilot's $20/tutor/year](tutor-copilot.md) and the
[ODU multi-agent figure of $2.63–$4.79/student/semester](../practice/cost-economics.md), the
picture is consistent across three very different architectures: **a course-scale AI tutor costs
single-digit-to-low-double-digit dollars per student per term.** Ethel is the high end because it
does grading and feedback, not just chat.
→ [cost and economics](../practice/cost-economics.md)

## ⚠ The grading findings — on our exact material

Ethel's assessment component was evaluated on a **high-stakes thermodynamics exam, 252 students**
(the detail is in [Kortemeyer, Nohl & Onishchuk](../domain/diagram-reading.md), arXiv:2406.17859).
Four results, all of which constrain us:

**1. Prompt granularity decides whether grading works.** *"Using a fine-grained rubric for entire
problems often resulted in bookkeeping mistakes and grading failures. In contrast, dividing
problems into several parts and using a comprehensive sample solution proved more reliable"* —
though that variant *"occasionally missed nuanced details and specific rubric weightings."*
**Decompose the problem, supply a worked solution; do not hand the model a whole rubric and a
whole problem.** This is the same shape as the general finding that models fail at *binding* and
bookkeeping rather than at physics.

**2. Diagrams again.** *"Grading graphical solutions, like process diagrams, was substantially
less reliable than grading mathematical derivations,"* with errors traced to *"extraneous visual
elements in freehand drawings."* T–s and P–v diagrams are where both **tutoring** and **grading**
break down. → [diagram reading](../domain/diagram-reading.md)

**3. ⚠⚠ The precision/recall asymmetry is the disqualifying one.** The system showed *"high
precision in identifying passing exam solutions but had **low recall, missing about half of the
other passing solutions**."* In plain terms: **when it says a solution passes, believe it; when it
says a solution fails, it is wrong about half the time.** That rules out autonomous grading
entirely, and it is exactly the right shape for a **triage** tool — auto-confirm the confident
passes, route everything else to a human.

**4. Handwriting recognition, not reasoning, was the bottleneck** — *"the primary challenge was
handwriting recognition"* — and it remains their largest open problem. Worth remembering before we
assume a vision model solves student work: the failure was in transcription, upstream of any
tutoring.

## What they plan next, which doubles as a roadmap

- An **instructor self-serve platform** so faculty upload their own documents and get a
  course-specific bot without developer involvement — the same instructor-facing control
  [PeteChat](petechat-purdue.md) arrived at independently.
- **Connectivity with campus systems**, specifically lecture recordings, to reuse
  already-generated subtitles as retrieval material. → [LMS integration](../practice/lms-integration.md)
- **Direct links to referenced material segments** so students can trace a claim to its source.
  → [grounding and verification](../concepts/grounding-and-verification.md)
- Continued exploration of **open-weight and on-premises** options to cut the Azure dependency.

## ⚠ What this is not

**There is no learning-outcome evaluation.** This is a system-description paper: architecture,
cost, and grading accuracy. No student learning was measured, no control condition exists, and the
chatbot component is evidenced by a single illustrative dialogue. On the
[Stan six-level scale](stan-udel.md) the chatbot is a **grounded Q&A assistant** — Level 2 — not a
tutor. Its genuinely novel contribution is the **assessment** side.

## Open questions

- [ ] Has ETH published usage or learning data for Ethel since July 2024? Worth a check.
- [ ] Is the $7.50 figure inclusive of the grading workload, or chat only? The paper says
      "operating Ethel," which reads as all-in, but it is one sentence.
- [ ] Kortemeyer is also behind ["could an AI agent pass an introductory physics
      course?"](../domain/superstudent-thermodynamics.md) — is there a single ETH research
      programme here we should be tracking as a whole?

## Connects to

- [Kortemeyer's thermodynamics grading study](../domain/diagram-reading.md) — the 252-student exam
- [Cost and economics](../practice/cost-economics.md) — the $7.50 datapoint
- [PeteChat](petechat-purdue.md) — the other university-built, RAG-grounded, instructor-controlled tutor
- [Stan](stan-udel.md) — the level scale this sits on
- [RAG in education](../concepts/rag-in-education.md)
- [PSU AI landscape](../practice/psu-ai-landscape.md) — the institutional-contract privacy route

## Sources

- [Kortemeyer, G., "Ethel: A Virtual Teaching Assistant," arXiv:2407.19452](https://arxiv.org/pdf/2407.19452) `[read — full text, 3 pp., 2026-09-01]`
- [Kortemeyer, Nohl & Onishchuk, "Grading Assistance for a Handwritten Thermodynamics Exam," arXiv:2406.17859](https://arxiv.org/abs/2406.17859) `[read]` — covered in [diagram reading](../domain/diagram-reading.md)
