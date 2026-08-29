# Superstudent Intelligence in Thermodynamics

**Type:** study
**One line:** OpenAI's o3, zero-shot, solved every problem on a real university
thermodynamics exam correctly — better than every human student, scoring in the range of the
best results across 10,000+ administrations since 1985.
**Why we care:** It settles the capability question in our domain and forces the project's
framing: we are not building something that can solve thermodynamics problems. That exists.

## The study

Tested **o3 in zero-shot mode** on a university thermodynamics exam designed to require
"knowledgeably and creatively combining principles of thermodynamics" rather than pattern
matching.

Result: **solved all problems correctly, better than all students who took the exam.** Its
score fell in the range of the best scores observed across **more than 10,000 similar exams
since 1985.**

Context the authors supply: thermodynamics exams of this kind have high failure rates and
rare A grades, and top scores have historically been treated as markers of exceptional
intellectual ability.

Their conclusion: this is *"a turning point"* warranting discussion of consequences for
engineering practice and engineering education.

## What this does to our project's framing

**The naive version of our project is obsolete on arrival.** "Build something that can solve
thermodynamics problems for students" — done, by a general-purpose model, zero-shot, better
than any student in forty years of that exam.

What survives, and it's most of what our brief actually asked for:

- **Teaching is not solving.** [MathTutorBench](../evaluation/mathtutorbench.md) found
  subject expertise and pedagogical skill *trade off*. A model that can solve everything has
  no idea how to make a student able to.
- **Reliability, not peak capability, is what tutoring needs.** o3 aced an exam;
  [ThermoQA](thermoqa.md) shows every frontier model at 44–63% on R-134a. Both true. See
  [the synthesis](llm-thermodynamics-capability.md).
- **Knowing the student is the hard part.** No exam performance tells you what *this*
  student misunderstands. → [knowledge tracing](../concepts/knowledge-tracing.md)
- **The assessment problem is now the instructor's problem.** If a free model outperforms
  every student on the exam, take-home assessment in thermodynamics is broken. That's
  [question C5](../../docs/03-open-questions.md), and it just got much sharper — this is a
  finding worth bringing to the instructor sponsor directly.

## The honest version of what we're building

Not "an AI that knows thermodynamics." That's a solved commodity available free.

**A system that uses a model that already knows thermodynamics to make a human learn it —
which is a different problem, is not solved, and is not obviously easier.**

That reframing should be in the capstone's introduction. It's more defensible than the usual
pitch, and it's true.

## Open questions

- [ ] **Read the full paper.** Which exam, which institution, how were the 10,000 exams
      compared, and was o3 given diagrams? (If the exam included diagram work, this
      contradicts [UTQA](utqa.md) and is very important. If not, they're consistent.)
- [ ] Was it one exam or several?
- [ ] Did the authors check the *reasoning*, or only final answers? A model can be right for
      wrong reasons, which matters enormously for a tutor.
- [ ] What do the authors propose for engineering education?

> **Verification: `[skimmed]` via abstract only.** The PDF didn't text-extract. The claims
> here are strong and consequential — **verify before citing.**

## Connects to

- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis
- [ThermoQA](thermoqa.md) / [UTQA](utqa.md) — the reliability counterpoint
- [MathTutorBench](../evaluation/mathtutorbench.md) — expertise ≠ pedagogy
- [open questions C5](../../docs/03-open-questions.md) — what this does to assessment

## Sources

- [Superstudent intelligence in thermodynamics, arXiv:2506.09822](https://arxiv.org/abs/2506.09822) `[skimmed]` — 30 pages, PDF cached locally
