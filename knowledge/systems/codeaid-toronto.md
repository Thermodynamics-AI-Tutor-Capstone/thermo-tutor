# CodeAid — University of Toronto

**Type:** system
**One line:** An LLM programming assistant deployed to 700 students for a semester that
answers with **pseudo-code and line-by-line explanations instead of code** — a
domain-specific mechanism for helping without giving the answer.
**Why we care:** It is the clearest example of solving the "help without solving" problem
*structurally*, through output format, rather than by asking the model nicely.

## What it is

Majeed Kazemitabaar and colleagues, **University of Toronto**, in a large introductory
**C and Systems Programming** course. **CHI 2024** (arXiv:2401.11314).

- **700 students, 12-week semester**
- Evaluation: thematic analysis of **8,000 usages**, weekly surveys, **22 student
  interviews**, and **8 programming-educator interviews**
- Built with an iterative design process involving continuous instructor feedback

## The design idea worth stealing

CodeAid *"delivers helpful, technically correct responses without revealing code
solutions."* Its four interaction modes:

- Answer general programming questions
- Ask questions about code the student provides
- **Generate pseudo-code with line-by-line explanations** — never runnable code
- **Annotate the student's incorrect code with fix suggestions** — pointing at the error
  without rewriting it

**This is a structural guardrail, not a prompted one.** The output *format* makes giving away
the answer difficult, rather than instructing the model to resist. Compare
[CS50's Duck](cs50-duck.md), which relies on a system prompt and consequently
**leaks code in 48% of conversations**.

**The thermodynamics analogue is worth thinking about.** What is the pseudo-code equivalent
in our domain? Candidates:

- The **solution strategy without the numbers** — "choose the control volume around the
  turbine, apply the steady-flow energy balance, you'll need h₁ and h₂ₛ" — with the student
  doing every lookup and computation
- A **state table with cells left blank** for the student to fill
- The **assumption list** for the problem, correct and explicit, with the solving left open
  → [our biggest teaching target](../domain/thermo-problem-benchmark.md)

That last one is interesting precisely because assumption identification is what
[every model gets wrong](../domain/llm-thermodynamics-capability.md) and what students most
need. Giving a *verified* assumption list is help that cannot be copied into an answer.

## Reported limitation

Per [CS50's](cs50-duck.md) discussion of it: CodeAid achieves **79% technical correctness**
but *"struggles with complex debugging tasks and maintaining consistent pedagogical
approaches across queries."*

Consistency across queries is the recurring theme —
[MathTutorBench](../evaluation/mathtutorbench.md) found general models degrade pedagogically
as dialogues lengthen, and CS50 measured its own drift at scale. **Pedagogical consistency,
not peak pedagogical quality, is the engineering problem.**

## Open questions

- [ ] **Read the CHI paper in full.** The 8,000-usage thematic analysis and the 22 student
      interviews are the closest published analogue to our own
      [planned interview study](../../research/student-interviews/protocol-draft.md), and
      their instruments may be adaptable.
- [ ] Did students find pseudo-code satisfying, or did they route around it to ChatGPT?
- [ ] Is CodeAid open source?
- [ ] What did the 8 educator interviews say? Directly relevant to
      [faculty adoption](../practice/faculty-adoption.md).

## Connects to

- [CS50 Duck](cs50-duck.md) — the prompt-based alternative, and its measured leakage
- [guardrails](../concepts/guardrails.md) — structural vs. instructed constraints
- [Socratic tutoring](../concepts/socratic-tutoring.md) — a third option beyond ask/refuse
- [property data tools](../domain/property-data-tools.md) — where a thermo analogue would live

## Sources

- [Kazemitabaar et al., "CodeAid: Evaluating a Classroom Deployment of an LLM-based Programming Assistant that Balances Student and Educator Needs," CHI 2024, arXiv:2401.11314](https://arxiv.org/html/2401.11314) `[skimmed]` — **priority read**
- [Austin Henley's summary](https://austinhenley.com/blog/codeaid.html) `[found]`
