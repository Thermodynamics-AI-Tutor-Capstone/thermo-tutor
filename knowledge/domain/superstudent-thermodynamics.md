# Superstudent Intelligence in Thermodynamics

**Type:** study
**One line:** OpenAI's o3, zero-shot, outscored all 90 students on a real German
engineering thermodynamics exam — including its diagram questions.
**Why we care:** It settles the capability question in our domain and forces the project's
framing. It also quietly undercuts the "diagram wall" story, because this exam had diagrams
and o3 handled them.

> **Verification: `[read]` — full text, 2026-08-31.** This node previously said o3 "solved
> every problem correctly." **The paper's own body says otherwise** — see the correction
> below. The abstract overstates the detailed account.

## The study

Rébecca Loubet, Pascal Zittlau, Marco Hoffmann, Luisa Vollmer, Sophie Fellenz, Heike Leitte,
Fabian Jirasek, Johannes Lenhard, **Hans Hasse** — Laboratory of Engineering Thermodynamics
and collaborating groups, **RPTU Kaiserslautern**, Germany. arXiv:2506.09822, June 2025.

**Same group** that produced the 22-problem benchmark in
[Loubet et al.](thermo-problem-benchmark.md). This is the follow-up.

- The exam from their **first course in engineering thermodynamics**, spring 2025
- **90 students** took it
- o3 was given the *same* exam, days after the students, and graded *the same way*
- **Zero-shot**, no prompt engineering, **three independent runs** (which barely differed —
  a contrast with their earlier study, where runs varied)
- Conducted in **German**; they note language has little effect on thermodynamics performance
- The exam **included graphical input and questions requiring graphical output**

The prompt, in their English translation:

> *"You are an expert in thermodynamics. Solve the exam given below. There are three
> problems 1-3. In each of them, start by answering the first question a). If you are asked
> for plots, draw them."*

## The result

- **o3 outscored all 90 students.** Its score was in the range of the best Hasse has seen in
  **more than 10,000 similar exams since 1985**
- **Student failure rate: 58%.** Exactly **one** student earned a grade A — o3 did better

**The correction:** o3 did *not* solve everything flawlessly. Per the body of the paper:

- Problem 1 — solved essentially without errors
- Problem 2 — same, but **points lost to "minor issues of o3 with graphical
  representations"**
- Problem 3 — **"the only major mistake o3 made,"** on a specialized topic: the caloric
  properties of a constant-density fluid

It won because the students did worse, not because it was perfect.

## Why the "10,000 exams" figure means something different than it sounds

It is not a formal dataset. Hasse, the corresponding author, **has taught this course for
several decades to more than 10,000 students** at different universities. The comparison is
against his own teaching history — which is a stronger claim about consistency of standards
than about statistical sampling.

## What the exam actually rewards — and why it matters

Their grading scheme is unusual and important for interpreting the result:

> *"points are earned for analyzing the problem, formulating the applicable equations, and
> combining them. The correct numerical solution gives points, but only comparatively few,
> so that grade A can be earned, in principle, without doing any numerical calculations."*

So o3 won on **reasoning structure**, not arithmetic. That makes the result *more*
impressive on the dimension that matters for engineering judgment — and it means the exam
**does not test** the property-lookup and numerical reliability where
[ThermoQA](thermoqa.md) found frontier models weakest (R-134a at 44–63%). The two results
are measuring different things and are fully compatible.

The authors also stress that this exam resists pattern-matching: *"the problems in the
thermodynamics exam are always new and carefully crafted, so they cannot be solved by
relying on pattern learning but only by knowledgeably and creatively applying the principles
of thermodynamics."*

## What this does to our project's framing

**The naive version of our project is obsolete on arrival.** "Build something that can solve
thermodynamics problems" is done, by a general model, zero-shot, better than any student in
that course's history.

What survives — and it is most of what our brief actually asked for:

- **Teaching is not solving.** [MathTutorBench](../evaluation/mathtutorbench.md) found
  subject expertise and pedagogical skill trade off; [TutorGym](../evaluation/tutorgym.md)
  found no model beat chance at recognizing an *incorrect* student step. A model that aces
  the exam still cannot reliably tell whether your work is wrong.
- **Reliability, not peak capability.** See [the synthesis](llm-thermodynamics-capability.md).
- **Knowing the student is the hard part.** No exam score tells you what *this* student
  misunderstands. → [knowledge tracing](../concepts/knowledge-tracing.md)
- **Assessment is already broken, independent of us.** If a free model outperforms every
  student on the exam, take-home assessment in thermodynamics has a problem now. That is
  [question C5](../../docs/03-open-questions.md), and it is worth bringing to the instructor
  sponsor as a shared problem rather than one we created.

**The honest framing for our introduction:** not "an AI that knows thermodynamics" — that's
a free commodity — but *a system that uses a model which already knows thermodynamics to
make a human learn it.* Different problem, unsolved, not obviously easier.

## Open questions

- [ ] The exam and full solutions are in the Supplementary Information. **Get them** — a
      real, hard, diagram-inclusive thermo exam with a marking scheme is directly useful as
      an evaluation instrument.
- [ ] Did they check o3's *reasoning*, or only final answers and marks? A model right for
      wrong reasons is a bad tutor. (The marking scheme awards points for formulating and
      combining equations, which suggests reasoning was assessed — worth confirming.)
- [ ] Has anyone repeated this with a newer model, or on an English-language exam?
- [ ] What do the authors propose for engineering education? (Section 3 discusses it; worth
      a careful read before we write our own framing.)

## Connects to

- [LLM capability in thermodynamics](llm-thermodynamics-capability.md) — the synthesis
- [Loubet et al.](thermo-problem-benchmark.md) — same group, the earlier benchmark
- [ThermoQA](thermoqa.md) / [UTQA](utqa.md) — the reliability counterpoint
- [diagram reading](diagram-reading.md) — **this study complicates the diagram-wall story**
- [MathTutorBench](../evaluation/mathtutorbench.md) — expertise ≠ pedagogy
- [open questions C5](../../docs/03-open-questions.md) — what this does to assessment

## Sources

- [Loubet et al., "Superstudent intelligence in thermodynamics," arXiv:2506.09822](https://arxiv.org/abs/2506.09822) `[read]` — full text
