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

## Connects to

- [knowledge tracing](../concepts/knowledge-tracing.md) — invented here
- [knowledge components](../concepts/knowledge-components.md) — invented here
- [Andes](andes.md) — the parallel step-based lineage
- [VanLehn 2011](../concepts/vanlehn-2011.md) — where these systems land empirically
- [ALEKS](aleks.md) — the competing formalism for the same problem

## Sources

- [Kenneth Koedinger — Wikipedia](https://en.wikipedia.org/wiki/Kenneth_Koedinger) `[skimmed]`
- [The Simon Initiative — History](https://www.cmu.edu/simon/what-is-simon/history.html) `[skimmed]`
- [Cognitive Tutors: Lessons Learned (ACT-R)](http://act-r.psy.cmu.edu/papers/Lessons_Learned.html) `[found]`
- [LearnLab background readings](https://learnlab.org/index.php/background-readings) `[found]`
- [CMU Today, "CMU Researchers Develop Innovative Cognitive Learning Models"](https://www.cmu.edu/cmtoday/education_innovation/cognitive-learning-innovative-practice/) `[skimmed]`
