# Andes

**Type:** system
**One line:** A step-based intelligent tutoring system for university physics, evaluated for
five consecutive years at the US Naval Academy — the closest historical analogue to what we're
building, and the most instructive failure catalogue in this knowledge base.
**Why we care:** Its effect-size decomposition tells us what step-based tutoring actually buys,
its authoring cost tells us what it costs, and its abandoned Bayesian student model is a direct
warning about our own plan.

> **Rewritten 2026-08-31 from both 2005 papers in full.** Three corrections marked ⚠, one of
> which reverses a claim this node made.

## The evidence, year by year

Hour exams — in-class, ~4 open-response problems, students show all work:

| | 1999 | 2000 | 2001 | 2002 | 2003 | **Overall** |
|---|---|---|---|---|---|---|
| Andes n | 173 | 140 | 129 | 93 | 93 | **455** |
| Control n | 162 | 135 | 44 | 53 | 44 | **276** |
| p | .036 | <.0001 | .003 | .005 | .0005 | **<.0001** |
| Effect size | 0.21 | 0.92 | 0.52 | 0.44 | 0.60 | **0.61** |

⚠ **Two things to know before quoting these.** The effect size is
`(Andes − Control) / Control SD` — **Glass's Δ, not Cohen's d**, so it is not directly
comparable to the *g* values elsewhere in this wiki. And **the widely-quoted 0.92 for 2000 does
not reproduce from the paper's own table**: (70.0 − 57.1)/19.0 = **0.68**. The 0.92 requires the
*Andes* SD as denominator. The headline 0.61 checks out exactly.

**The control is hard**, not "nothing": same course, textbook, exams; homework collected and
graded, marked early in the semester specifically to enforce drawing coordinate systems and
vectors, with comments like *"Draw FBD"* and *"Axes"*; some sections gave weekly quizzes;
worked solutions handed out. This is step-based ITS versus **conscientiously graded paper
homework**.

Design caveats the authors state themselves: *"Students were not assigned randomly to
condition… Students were not given an appropriate pre-test."* And ours: the control group
collapses from 162 to **44** by 2001 and stays there, while the instructors were the paper's
authors and taught the Andes sections.

## ⭐⭐ The subscore table — the most important number in this knowledge base

Hour-exam rubric: Drawings 30%, Variable definitions 20%, Equations 40%, Answers 10%.

| Subscore | 2000 | 2002a | 2002b | 2003 | **Average** |
|---|---|---|---|---|---|
| **Drawings** | 1.82 | 0.49 | 0.83 | 1.72 | **1.21** |
| **Variable definitions** | 0.88 | 0.42 | 0.36 | 1.11 | **0.69** |
| Equations | 0.20 | 0.12 | 0.30 | −0.17 | **0.11** |
| **Answers** | −0.10 | −0.09 | 0.06 | −0.20 | **−0.08** |

*(Equations and Answers were non-significant in every year.)*

**Five years of step-based tutoring moved drawings and variable definitions, and moved nothing
at all on getting the right answer.**

**Step-based tutoring buys the process, not the product.** The implication is direct and
uncomfortable: **if our thermodynamics tutor's outcome measure is "did the student get the right
answer," Andes predicts we will measure zero.** We would have to grade the *derivation* to see
the effect — which means **the assessment instrument has to be designed before the tutor**, and
it has to be step-level.

This also reframes the [instrument choice](../evaluation/concept-inventories.md): STPFaSL's
**Representation** subscale is a process measure, and process is where the effect lives.

Corroborating: the 2003 **final exam** — 50 multiple-choice items, answers only — gave an
overall effect of just **0.25** (p = .028), against 0.61 on the derivation-graded hour exams.

## ⚠ Correction: the Bayesian network was removed, and was never the source of the effect

This node previously said "Bayesian networks for decision-making." That is **wrong for the
system that produced the results.** The Bayesian student model existed only in **Andes1**, was
deliberately torn out, and **the 0.61 came from Andes2 — a system with no Bayesian network at
all.**

> *"The bottom line was that the Bayesian student modeling technique was not the source of
> Andes1's power. **It was indeed a highly accurate assessment of student mastery**, but the
> rest of the tutoring system didn't really have much use for such an assessment."*

> *"the Bayesian student model that was so prominent in Andes1 is no longer useful, so it has
> **fallen into disrepair**."*

**The reason is structural and it lands squarely on our design.** USNA instructors assigned
specific problems; Andes could not choose the next problem and could not decide whether a
student advanced. So it computed an accurate mastery estimate and **had nothing to do with
it.**

> **An accurate student model is worthless unless the system is empowered to act on it.**

Before we build [knowledge tracing](../concepts/knowledge-tracing.md), we must answer: *what
decision does the mastery number actually change?* If the course assigns the problem set and we
cannot select problems or gate progression, we would be rebuilding Andes1's dead end.
→ [knowledge tracing](../concepts/knowledge-tracing.md)

**Plan recognition failed too, and the test is worth copying.** Andes1 inferred the student's
plan and hinted the next step in it. They printed 40 randomly sampled help episodes and gave
them to three physics instructors. **The instructors agreed with each other in 21 of 40
episodes. Andes agreed with that consensus in 3 of 21.** Diagnosis: students asking for help
usually have no coherent plan to recognize. Andes2 replaced it with a depth-first walk of the
solution graph — *"When the student's steps are randomly ordered, it is better to just ignore
them… We prefer step selections that are occasionally pedantic to ones that are occasionally
confusing."*

## What "step-based" means operationally

**Four windows:** problem text + drawing canvas (upper left), Variables table (upper right),
numbered Equations lines with a running score (lower right), hint dialogue (lower left).

**The loop:** click a palette tool → drag to draw → **fill out a modal dialogue box** → the
object commits and immediately turns **green or red** → define scalar variables → type equations
into numbered lines, each turning green or red on entry → click `x=?` and Andes solves *the
student's own equation system*.

**The dialogue boxes are the pedagogy, not chrome.** Defining a *velocity* forces a choice
between instantaneous and average. Defining an *individual force* forces naming **two** objects
— the object acted on, and the object the force is due to. Defining a *net* force names only
one, and the two dialogues are drawn differently on purpose.

**Three hard constraints**, one of which is a lovely lesson: to define any vector-derived scalar
you **must draw the vector**. They tried a menu shortcut in 1999–2000; students used it and made
sign and angle errors; exhortation failed. *"So we removed the menu option, endured the
student's complaints, and noticed a decrease in errors."*

**Feedback is three-layered:** immediate green/red on every entry; **unsolicited pop-ups only
for slips** (blank field, undefined variable, missing units) — *"for errors where some learning
is possible, Andes gives help only when asked"*; and solicited What's Wrong / Next Step help.

**Hints are 3-deep: pointing → teaching → bottom-out.** While a hint displays, **the other three
windows grey out**, explicitly to defeat the eye-tracking finding that students don't read hints.

**The unit of work: ~30 gradeable steps per homework problem**, with branches for independent
solution routes that share sub-steps. That is the granularity we would have to author for
thermodynamics.

## ⭐ The authoring cost — the honest number

There is no hours-per-problem figure in either paper. What there is, is worse:

> *"When the Andes project began, we naively thought that once we had developed enough authoring
> tools, the instructors could augment the knowledge base on a part-time basis… Andes currently
> has **550 rules**. Maintaining such a large knowledge base is like maintaining any other large
> software system… Thus, our work process involves a **full-time knowledge engineer**."*

**356 problems, 550 rules, one full-time knowledge engineer indefinitely, plus four physics
professors part-time, over roughly nine years.**

And completeness is non-negotiable: the author supplies a formal problem statement and **Andes
must solve it in every valid way** — *"If Andes failed to generate a valid solution… the
student's entry would be colored red, with unfortunate pedagogical results."* One missed
solution path means the tutor tells a correct student they are wrong. Every knowledge-base edit
regenerates all 356 solution graphs, diffed against the previous set.

**This is the hidden cost of step-based ITS, and the reason chatbots won on convenience.**

## ⚠ Andes has no thermodynamics — but its sibling project does

The knowledge base covers kinematics, dynamics, vectors, work-energy, momentum-impulse,
circuits, electromagnetism, optics, waves, fluids. **No thermodynamics module exists.** We
cannot lift Andes content.

**But the same ONR initiative produced the actual thermodynamics precedent**, which this
knowledge base had entirely missed:

> *"Two projects resulted, an extensive implementation of Ken Forbus' existing **CyclePad**
> software in the **thermodynamics curriculum at the Academy**, and a more ambitious project to
> build a new physics tutor…"*

→ **[CyclePad and CycleTalk](cyclepad-cycletalk.md)** — read that node next.

And Andes' authors assert transfer to our domain explicitly: *"any topic where problems are
solved by producing a system of equations and solving them is amenable to an Andes style
treatment. This includes many topics in engineering and science."*

## What they say they got wrong

A remarkably candid list:

- **Bayesian student modeling** — accurate, useless, removed
- **Plan-recognition hinting** — 3/21 agreement with expert consensus, removed
- **Syntactic error diagnosis** — *"probably did more harm than good,"* removed. And the reason
  matters: *"if students get even a few cases of bad advice, they will stop asking for advice
  entirely, preferring to guess repeatedly instead."*
- **The authoring premise** — instructors could not maintain the knowledge base part-time
- **UI training** — tutorials, manuals, help systems, an animated agent, pop-up hypertext: all
  failed. **Only short videos worked.**
- **Instructors were the adoption bottleneck, not students** — *"they soon ran into user
  interface details that stymied them, and rejected Andes as 'too hard for students to use.'"*

**Their prescribed build order, which is a gift to a two-semester capstone:**

1. **Phase 1** — flag feedback + integrated math solver + many problems + training videos.
   **Nothing else.** Ship into a real course.
2. **Phase 2** — add What's Wrong Help, **authored from Phase 1 log files**: sort logs for
   frequent incorrect equations, have graders tag each with its error and a hint sequence, write
   handlers from that data, regression-test against the logs.
3. **Phase 3** — add Next Step Help, **authored from human tutoring transcripts**. Their concrete
   proposal: put a Help button in the tutor connecting to a **live human tutor** working
   call-center style, then mine those transcripts. *"The human tutoring would also provide a
   valuable service to students."*

**That 2005 proposal is the hybrid human-AI architecture people are publishing in 2026** — with
human tutoring as a *data-generation mechanism for authoring* rather than a service tier.
Strongest single design idea in this batch.

**Their stated #1 lesson:** *"It is absolutely critical that the instructors be active
participants in the design process at every step of the way."*

## Student acceptance — unflattering, and they published it

| | 2001 | 2002 | 2003 |
|---|---|---|---|
| Would use Andes if not required (12 wks) | 32.7% | 46.0% | 37.8% |
| **Average favourable / unfavourable** | **39.9 / 46.7** | **51.4 / 39.6** | **41.9 / 56.0** |

*"about 40% to 50% of the students seemed to like Andes and about 40% to 55% seemed to dislike
it."* **Engineers liked it least** — 30% would use it voluntarily.

**But** asked to compare against WebAssign/Blackboard specifically, **69.2% said Andes was more
effective, 14% less.** Students don't want *any* electronic homework helper; conditional on
being forced to use one, they prefer the step-based one.

**A step-based tutor that measurably works can still be actively disliked by a majority of its
users.** Plan the adoption story accordingly. → [engagement decay](../concepts/engagement-decay.md)

## Availability today

- **Source is live: [github.com/bvds/andes](https://github.com/bvds/andes)**, LGPL-3.0, last push
  2018. Common Lisp + C++ solver + Mathematica; SBCL/Apache/MySQL. The full knowledge base is
  readable, including `errors.cl` (176 KB — the error-handler library).
- 🚩 **The 356 problems are NOT in the repo.** `documentation/install.md`: *"The original Andes
  problem definitions are under copyright and not publicly available. For access, send your ssh
  public key to help@andestutor.org"* — and **andestutor.org no longer resolves.** The artifact
  that cost a decade of instructor and knowledge-engineer time is, as far as we can determine,
  **unobtainable through any public channel.** That is the durable lesson about step-based ITS
  content.
- ⭐ **Worth reading before we design our own logging:** the repo contains a working
  consent-gated, anonymized, researcher-accessible logging implementation — a `STUDENT_STATE`
  consent workflow, a read-only `open` account exposing only `OPEN_STUDENT_STATE` and
  `OPEN_PROBLEM_ATTEMPT`, and `x:`/`md5:` username prefixes so identity never reaches the
  server. → [IRB](../../admin/irb.md)

## Open questions

- [ ] **VanLehn (2015), "Reflections on Andes' Goal-free User Interface," *IJAIED* 25(3)** — a
      ten-year retrospective by the PI specifically on the unconstrained-UI decision. OpenAlex
      says OA; Springer redirects to auth. **Try from a campus IP. Probably the highest-value
      unread document for us.**
- [ ] The two papers **disagree on aptitude–treatment interaction** — *Lessons Learned* finds it
      small and uniform across majors; *Five Years* finds the 2003 final-exam effect only for
      "Others." Same project, different instruments. Flag both if citing either.
- [ ] Clone the repo and read `errors.cl` — a hand-built library of physics error handlers is the
      closest thing to a worked misconception catalogue in existence.

## Connects to

- [CyclePad & CycleTalk](cyclepad-cycletalk.md) — **the thermodynamics sibling project**
- [VanLehn 2011](../concepts/vanlehn-2011.md) — the meta-analysis Andes fed
- [knowledge tracing](../concepts/knowledge-tracing.md) — the "act on the model" warning
- [knowledge components](../concepts/knowledge-components.md) — ~30 steps per problem
- [concept inventories](../evaluation/concept-inventories.md) — why the instrument must be process-level
- [our skill graph](../../research/domain/skill-graph-draft.md)

## Sources

- [VanLehn et al., "The Andes Physics Tutoring System: Lessons Learned," *IJAIED* 15(3), 147–204 (2005)](https://oli.cmu.edu/wp-content/uploads/2012/05/VanLehn_2005_Andes_Physics_Tutoring_System.pdf) `[read]` — 47 pp. **Closed at the publisher; this CMU mirror is the only free copy located. Save it.**
- [VanLehn et al., "Five Years of Evaluations," AIED 2005, pp. 678–685](https://oli.cmu.edu/wp-content/uploads/2012/05/VanLehn_2005_Andes_Five_Years_of_Evaluations.pdf) `[read]`
- Schulze et al., "Andes: An Intelligent Tutor for Classical Physics," *JEP* 6(1), 2000 `[inaccessible]` — Cloudflare-blocked on every route including Wayback. Describes Andes1 (the Bayesian version) and is superseded by the above.
- [github.com/bvds/andes](https://github.com/bvds/andes) `[read — repo inspected]` — LGPL-3.0; knowledge base present, **problems absent**
- VanLehn (2015), "Reflections on Andes' Goal-free User Interface," *IJAIED* 25(3) `[found]` — **priority**
