# Cognitive Tutor (CMU / Carnegie Learning)

**Type:** system
**One line:** ACT-R-based intelligent tutors from Carnegie Mellon — the lineage that gave
the field model tracing, knowledge tracing, and the knowledge-component framework.
**Why we care:** Most of the vocabulary we use for student modeling comes from here, and
the RAND result is one of the largest measured effects in educational technology.

## Lineage

John Anderson's **ACT-R** cognitive architecture → the LISP Tutor → the Practical Algebra
Tutor (Anderson and **Kenneth Koedinger**) → Carnegie Learning's commercial Cognitive
Tutor → the **Pittsburgh Science of Learning Center / LearnLab** → CMU's **Open Learning
Initiative (OLI)** and the **Simon Initiative**.

This is a fifty-year continuous research program, and it is the intellectual source of:

- **Model tracing** — inferring which production rule a student applied from what they did
- **[Knowledge tracing](../concepts/knowledge-tracing.md)** — Bayesian estimation of
  per-skill mastery from a response history. Everything from BKT to DKT descends from this.
- **[Knowledge components](../concepts/knowledge-components.md)** — the unit of
  "one thing a student can know," and the KLI framework
- **The doer effect** — that *doing* practice problems produces far more learning than
  reading or watching, established causally across multiple domains and learner contexts
  ("Learning is Not a Spectator Sport")

## Evidence

A **RAND Corporation** trial of Cognitive Tutor Algebra found high school students in the
curriculum learned **almost a full additional year of algebra** during the trial.

## The doer effect, and why it should worry us

The doer-effect finding is the most under-discussed result in this entire knowledge base
relative to its importance for our design.

If doing generates learning and reading doesn't, then **a tutor whose primary output is
explanatory prose is optimized for the wrong thing.** A chat interface naturally produces
reading. Every paragraph the tutor writes is a paragraph the student is not spending
attempting.

This connects directly to [Bastani's harm result](../evidence/bastani-2025-harm.md): the
unguarded-AI group did better during practice and worse afterward. They were watching, not
doing.

**Design implication:** measure the ratio of student *attempts* to tutor *words*. If our
tutor talks more than the student works, the mechanism the evidence supports isn't
running.

## Open questions

- [ ] Exact effect sizes from the RAND study and its replications
- [ ] What's the current state of OLI, and is its content reusable?
- [ ] Are there OLI or LearnLab engineering/thermodynamics courses?
- [ ] Is DataShop (the PSLC learning-data repository) usable for us? It's the largest
      open store of tutoring interaction data and could inform our
      [grain question](../../docs/03-open-questions.md)

## ⭐ The eight principles, from the primary

Anderson, Corbett, Koedinger & Pelletier, *"Cognitive Tutors: Lessons Learned"* (CMU, read in
full 2026-09-01). Extracted from ACT* theory and used to build every tutor in this line:

1. **Represent student competence as a production set** — an explicit model of the target skill,
   used both to set curriculum objectives and to interpret student actions.
2. **Communicate the goal structure underlying the problem solving** — via *reification*: make the
   implicit decomposition visible in the interface. Their example is a proof graph in geometry.
3. **Provide instruction in the problem-solving context** — not before it.
4. **Promote an abstract understanding of the problem-solving knowledge.**
5. **Minimise working memory load.**
6. **Provide immediate feedback on errors.**
7. **Adjust the grain size of instruction with learning.**
8. **Facilitate successive approximations to the target skill** — *"when students are initially
   trying to perform a skill, they cannot perform all the steps,"* so the tutor fills in the
   missing ones and withdraws as competence grows.

**Principle 2 is the one a chat interface silently drops.** A conversation does not reify anything;
it renders the goal structure as prose and then scrolls it away. A
[T–s diagram with marked states](../domain/diagram-reading.md), or a visible list of the
sub-questions in a cycle analysis, is the thermodynamics equivalent of their proof graph — and it
is [exactly what the sub-question decomposition loop provides](../concepts/grounding-and-verification.md).

## ⚠⚠ Three empirical findings that cut against how AI tutors are built today

**1. The tutors worked better when they did *not* pretend to be human.**

> *"The tutors appear to work better if they present themselves to students as **non human tools
> to assist learning rather than as emulations of human tutors**."*

Nearly every current LLM tutor does the opposite — a name, a persona, a conversational manner. And
the largest single complaint about [LearnLM in Google's own arena](learnlm.md) was
**conversational style: "patronizing" (36.3%)**. **Two findings thirty years apart pointing the
same way: the persona is a liability, not a feature.** Worth testing rather than assuming.

**2. Short, directed error messages beat elaborate ones.**

> *"the best tutorial interaction style was one in which the tutor provides **immediate feedback,
> consisting of short and directed error messages**."*

Set against LLM tutors' natural register — long, warm, thorough — and against
[UIC students' complaint](../evidence/student-ai-perceptions-2025.md) that competitors were
preferred for being *more succinct*. **Terseness is a measured feature.**

**3. ⭐ Pairing students at one machine destroyed the effect.**

> *"Because we did not have enough machines, sometimes pairs of students worked on the machines.
> In this case, **most of the tutor benefit was eliminated**."*

An accident of hardware supply produced the cleanest available evidence that **the benefit is
individual**, not collaborative — and it aligns with
[productive failure's finding that individual work wins in short sessions](../concepts/productive-failure.md).
**A 1:1 tutor should be genuinely 1:1.**

## The effect sizes, from the primary

- **LISP tutor:** students took **30% less time** *and* scored **one standard deviation higher** on
  the final test than a control using a standard LISP environment.
- **Geometry tutor:** a 14-point gain, *"more than one standard deviation in the population or more
  than one letter grade."*
- **Best case overall:** *"students could achieve at least the same level of proficiency as
  conventional instruction in **one-third of the time**."*

⚠ Note the framing: their strongest claim is about **time**, not ceiling. Same proficiency,
faster. That is a more defensible and more sellable promise than a learning-gain headline, and it
is the one [Kestin also reports](../evidence/kestin-2025-rct.md) (49 min vs 60).

## Connects to

- [knowledge tracing](../concepts/knowledge-tracing.md) — invented here
- [knowledge components](../concepts/knowledge-components.md) — invented here
- [Andes](andes.md) — the parallel step-based lineage
- [VanLehn 2011](../concepts/vanlehn-2011.md) — where these systems land empirically
- [ALEKS](aleks.md) — the competing formalism for the same problem

## Sources

- [Kenneth Koedinger — Wikipedia](https://en.wikipedia.org/wiki/Kenneth_Koedinger) `[skimmed]`
- [The Simon Initiative — History](https://www.cmu.edu/simon/what-is-simon/history.html) `[skimmed]`
- [Anderson, Corbett, Koedinger & Pelletier, "Cognitive Tutors: Lessons Learned"](http://act-r.psy.cmu.edu/papers/Lessons_Learned.html) `[read — full text, ~17,000 words, 2026-09-01]`
- [LearnLab background readings](https://learnlab.org/index.php/background-readings) `[found]`
- [CMU Today, "CMU Researchers Develop Innovative Cognitive Learning Models"](https://www.cmu.edu/cmtoday/education_innovation/cognitive-learning-innovative-practice/) `[skimmed]`
