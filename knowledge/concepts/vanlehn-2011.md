# VanLehn 2011 — the effect sizes that anchor the field, and the mechanism underneath them

**Type:** concept / review
**One line:** The review that dismantled Bloom's 2 sigma, showed step-based ITS within a
rounding error of human tutors — and then explained *why*, in a paragraph almost nobody quotes.
**Why we care:** It sets the bar our project has to clear; it names *interaction granularity*
rather than feedback intelligence as the variable that predicts learning; and its causal
explanation — **students only learn from solutions they finish themselves** — is the single most
useful sentence in this knowledge base for deciding what our tutor is allowed to do.

> **Verification: `[read — full text, 25 pp., 2026-09-03]`.** Local copy:
> `course-materials/papers/vanlehn-2011-relative-effectiveness.pdf` (+ `.txt`). Obtained via
> Taylor & Francis after the ASU and Wayback routes failed. **This node was previously built
> entirely on secondhand sources and carried three errors; they are marked ⚠ below.**

Kurt VanLehn, *"The Relative Effectiveness of Human Tutoring, Intelligent Tutoring Systems,
and Other Tutoring Systems,"* **Educational Psychologist 46(4), 197–221, 2011.**
[DOI 10.1080/00461520.2011.611369](https://doi.org/10.1080/00461520.2011.611369). Experiments
published 1975–2010, STEM content only, random assignment only, one-on-one only. ~1,400 citations.

---

## ⭐⭐⭐ The mechanism, which is the most important content in the paper

Everyone cites 0.79 and 0.76. Almost nobody cites the explanation VanLehn gives for them, and
it is the part that should govern our design.

The active ingredient is not feedback, not hints, not the student model. It is **finishing a
correct solution having done most of the reasoning yourself**:

> **"When students solve a multistep problem correctly doing most of the reasoning themselves,
> then they are applying hundreds of knowledge components. Each time they apply a knowledge
> component, they do so in a new context and thus generalize it. They access it in memory and
> thus strengthen it. If they fail initially to retrieve an appropriate knowledge component,
> then they usually construct or reconstruct it… In short, when students self-generate a correct
> solution, they generalize, strengthen, construct, and debug all the knowledge components
> required by the solution. Unfortunately, when they quit early, they miss hundreds of
> opportunities to learn."**

**Four verbs: generalize, strengthen, construct, debug.** Every one of them is an act the
student performs. None of them is something a tutor can do *to* a student.

And the reason answer-based systems lose is not that their feedback is bad. It is that
**they let students stop**:

> "Answer-based tutoring systems offer such weak scaffolding and feedback that
> **students are usually allowed to give up after several failed attempts.**"

Whereas the systems on the plateau all share one property — they get the student to the end:

> "Human tutors almost always get students to finish a problem correctly… Many ITS have such
> strong scaffolding and support for self-repairs that students often complete problems
> correctly, and **some ITS even require students to correctly solve the current problem before
> moving on to the next.**"

**Scaffolding and feedback are instrumental, not terminal.** VanLehn is explicit that their
main effect may be *indirect*: "they may have an equally strong indirect effect by making it
more likely that students finish problems correctly having done most of the reasoning
themselves."

### This is not VanLehn's idea, and it was tested before he wrote it

> "This explanation, that all self-generated correct solutions are equally effective, was first
> proposed by **Anderson et al. (1995)**, albeit only for step-based tutoring systems."

Anderson's team tested it by varying things that *should* have mattered — most notably
**immediate vs. delayed feedback** — and found that "when students in all experimental groups
were required to complete all the problems correctly, the experimental manipulations did not
affect their learning gains. On the other hand, the manipulations did affect **efficiency**,
namely, the time to complete all the problems correctly."

**Read that as a design law: pedagogical cleverness buys speed, not learning. Completion buys
learning.** → [Cognitive Tutor](../systems/cognitive-tutor.md)

### ⭐ What this single mechanism explains across our own base

It is the same construct arriving under five different names in five unrelated literatures:

| Where we met it | What it was called | What it actually is |
|---|---|---|
| [TUM RCT](../evidence/tum-dissociation-2025.md) | germane cognitive load fell | the student stopped doing the reasoning |
| [Bastani PNAS](../evidence/bastani-2025-harm.md) | +48% assisted, −17% unassisted | the solution was never self-generated |
| [LLM synthesis](../evidence/llm-synthesis-shallow-learning.md) | "shallower knowledge," sources didn't help | being told ≠ constructing |
| [Productive failure](productive-failure.md) | generation before instruction | forcing construction before the answer exists |
| [aiPlato](../systems/aiplato-uta.md) | "Evaluate My Work," 152 uses / 61 students | students demanding to finish it themselves |

**Design consequence, stated plainly: our tutor's job is to make sure the student reaches a
correct solution having done the reasoning, and to make quitting hard.** Not to explain well.
An excellent explanation that lets the student stop is a worse intervention than a mediocre
prompt that gets them to the end. → [guardrails](guardrails.md),
[grounding and verification](grounding-and-verification.md)

⚠ **The corollary is uncomfortable.** "Reveal the answer" is not a mild pedagogical failure in
this model — it is the *entire* failure, because it removes hundreds of knowledge-component
applications at once. That is why
[the same reversal keeps showing up in the metrics](../evaluation/behavioral-evaluation.md).

---

## Table 1, in full, with the counts — because the counts are the story

This is the whole result of the review. `No.` is the number of comparisons; `% Reliable` is the
share significant at p < .05.

| Comparison | No. | d | % Reliable |
|---|---:|---:|---:|
| Answer-based vs. no tutoring | **165** | **0.31** | 40%† |
| **Step-based vs. no tutoring** | 28 | **0.76** | 68% |
| Substep-based vs. no tutoring | 26 | 0.40 | 54% |
| **Human vs. no tutoring** | 10 | **0.79** | 80% |
| Step-based vs. answer-based | **2** | 0.40 | 50% |
| Substep-based vs. answer-based | 6 | 0.32 | 33% |
| Human vs. answer-based | **1** | −0.04 | 0% |
| Substep-based vs. step-based | 11 | 0.16 | 0% |
| Human vs. step-based | 10 | 0.21 | 30% |
| ⚠ **Human vs. substep-based** | 5 | **−0.12** | 0% |

† Not VanLehn's own analysis. **The 0.31 is imported wholesale from C. Kulik & Kulik (1991)**,
and the 40% is VanLehn's own admitted approximation: Kulik & Kulik reported 40% reliable across
*all* categories and "did not break this down per category."

⚠ **Three corrections to what this node used to say:**

1. **"Human tutoring beat substep-based systems by d = 0.12" — sign error.** The value is
   **−0.12**: substep-based systems slightly *outperformed* human tutors. Not reliably (0% of
   5 comparisons), but the sign matters, and the old text had it backwards.
2. **"10 comparisons drawn from 28 evaluation studies" — a garble of the table.** *Ten* is the
   number of possible **pairwise comparison types** among five instruction types. *28* is the
   number of step-vs-no-tutoring comparisons in one row. VanLehn's informal search "yielded 87
   comparisons"; the formal search added 8 more.
3. **The evidence base is thinner than any single number suggests, and thinnest exactly where
   we lean hardest.** See the next section.

### ⚠⚠ The claim we depend on rests on two experiments with one tutor

We have been using "step beats answer-based" as a load-bearing design argument. Here is the
whole of the direct evidence for it (Table A4):

> **Suraweera & Mitrovic (2002), Exp. 1: d = 0.17 (not reliable). Exp. 2: d = 0.63 (reliable).**
> Both are **KERMIT, a database-design tutor**, versus a version of itself that gave final-answer
> feedback only.

**Two experiments, one system, one domain, one lab, and one of the two is null.** The
head-to-head human-vs-answer-based row is worse: **a single 1982 comparison, d = −0.04.**

The 0.76-vs-0.31 gap that the field quotes is a comparison of **two separate sets of studies
against different no-tutoring baselines twenty years apart** — the 0.31 side being 165 CAI
studies from a 1991 review that VanLehn did not re-analyse. It is suggestive, and it is
consistent with the direct contrast, but **it is not a controlled granularity manipulation**,
and we should stop citing it as though it were one.

⭐ **This does not weaken the design recommendation. It relocates it.** The argument for
step-level interaction should now rest on **the completion mechanism above**, which is
theoretically motivated and independently supported, rather than on a granularity contrast
with k = 2.

---

## The interaction plateau

VanLehn set out to test the **interaction granularity hypothesis** — that effectiveness rises
monotonically as the tutor interacts around smaller pieces of reasoning:

> human tutoring > substep-based > step-based > answer-based > no tutoring

**It failed.** What he found instead:

> "When the granularity decreases from answer based to step based, the effectiveness increases
> from 0.31 to around 0.75. However, **further decreases in granularity yield negligible
> increases in effect size.** That is, there seems to be an **interaction plateau**."

> human tutoring **=** substep-based **=** step-based **>** answer-based

The three illustrative studies all show the same shape, and they are worth knowing individually
because each is a within-experiment test rather than a cross-study average:

- **Evens & Michael (2006)**, medical students, baroreceptor reflex: human tutors, CIRCSIM-tutor
  (substep) and CIRCSIM (step) **tied with each other**, all above reading. "This pattern is
  inconsistent with the interaction granularity hypothesis."
- **VanLehn et al. (2007)**, conceptual physics, five conditions: human tutoring, two substep
  dialogue systems (Why2-Atlas, [Why2-AutoTutor](../systems/autotutor.md)), a step-based text
  tutor, and read-only. **The four tutoring conditions were not reliably different from each
  other** and all beat reading by ≈ d = 1.0. Five further experiments replicated it.
- **Reif & Scott (1999)**, physics homework: human d = 1.31, step-based d = 1.01 vs. no tutoring
  — but **VanLehn threw out his own no-tutoring comparison** because the tutored conditions had
  been taught a problem-solving method the controls never saw. Only the human-vs-step contrast
  survived into the review. *(A model of how to handle a content confound, and a reminder that
  headline gains often hide one.)*

⚠ **One anomaly VanLehn cannot explain, and it should bother us.** In the last two Why2
experiments the read-only control used an **experimenter-written text instead of a commercial
textbook**, and those students "had equally high learning gains as students in the other
conditions." His footnote: *"It is not clear why they learned so well."* **A well-written text,
written for the actual student population, matched human tutoring.** Before we build a tutor we
should know what our course's baseline text is doing.

**Design implication, unchanged but now better founded:** a **step-level inner loop is
non-negotiable**; **finer than step buys nothing measurable** (substep vs. step: d = 0.16, 0 of
11 reliable); **answer-only is the tier to avoid.**
→ [Andes](../systems/andes.md), [knowledge components](knowledge-components.md)

---

## ⚠⚠ What the review says about itself

This is the section that never survives into secondary citations, and it changes how hard the
numbers can be leaned on.

> **"Because the formal search was truncated and the informal search is not replicable, and only
> one coder (the author) was used in applying the inclusion/exclusion criteria, this review does
> not meet current standards for meta-analyses."**

VanLehn says this in his own methods section. Three separate weaknesses — non-replicable search,
truncated formal search, single coder who is also the author of several included studies. His
defence is expertise: "it is likely that nearly all the relevant studies have been located…
in part because the author has worked for more than three decades in the tutoring research
community."

⚠ **And the effect-size selection rule inflates every number in Table 1:**

> "Many experiments use multiple assessments of learning… **This review reports the assessment
> with the largest effect size.**"

**Max-over-outcomes.** Read that against
the proximal–distal collapse table below — a rule that picks the
largest of several measures will systematically pick the one closest to the intervention.
**0.76 and 0.79 are upper bounds, not central estimates.**

⭐ **A third caveat with teeth for us: the "raising the baseline" arithmetic.** To combine
comparisons, VanLehn simply *adds* effect sizes — "given the crude approximation afforded by
adding effect sizes." His four estimates of human tutoring versus no tutoring, by that method:

| Route | Estimate |
|---|---|
| Direct | **0.79** |
| via answer-based | −0.04 + 0.31 = **0.27** |
| via step-based | 0.21 + 0.76 = **0.97** |
| via substep-based | −0.12 + 0.40 = **0.29** |

**0.27 to 0.97.** The famous 0.79 is one of four mutually inconsistent estimates, and it is the
one from the direct route with the fewest comparisons behind it (n = 10).

**⚠ Carnegie Learning was excluded entirely** — the Cognitive Tutor studies changed textbook and
classroom activities as well as software, so they failed the content-control criterion. VanLehn
reports What Works Clearinghouse's numbers for them anyway, and they are sobering: **0.38,
−0.18, −0.16, 0.04, −0.07.** → [Cognitive Tutor](../systems/cognitive-tutor.md)

---

## ⭐ Bloom's 2 sigma: what actually produced it

Our [Bloom node](blooms-two-sigma.md) had this as an open question — whether mastery learning
rather than one-to-one tutoring was doing the work. **VanLehn answers it directly, with the
number.**

Of the six studies Bloom summarised, only Anania (1981) Exp. 3 was one-on-one and thus eligible.
Its effect size was **1.95**. Then:

- The tutors were not super-tutors. They were **"undergraduate education majors"** who
  **"met the experimenter each day for one week before the instruction began."**
- The experiments had a **third condition: mastery learning in an ordinary classroom.** It
  scored **~1.0 SD** above the plain classroom control.
- **The mastery threshold was 90% in the tutoring condition and 80% in the classroom
  mastery-learning condition** (Anania, 1981, pp. 44–45). The classroom control had no threshold
  at all — students advanced regardless of score.

> **"That is, the tutors were holding their students to a higher standard of mastery than the
> classroom teachers. This alone could account for the advantage of tutoring (2.0 effect size)
> over mastery learning (1.0 effect size)."**

> **"So the Bloom (1984) article is, as Bloom intended it to be, a demonstration of the power of
> mastery learning rather than a demonstration of the effectiveness of human tutoring."**

**The second 2-sigma study is an artefact of one small control group.** Evens & Michael's first
baroreceptor experiment gave d = 1.95; repeated with more subjects it gave **0.52**. Tutee gains
were about the same both times — what moved was the *control*: the first control (**N = 9**) had
a mean gain of **0.33**, the replication's (N = 28) **1.54**, and a third comparable control
(N = 33) **2.0**. VanLehn: "may have been unusually low, perhaps due to a sampling artifact."

> **"The next highest effect size was 0.82."**

Two studies at 1.95, then a cliff to 0.82. That is the entire empirical basis of the founding
claim of this field.

⚠ *Note for our own use: the pre-extracted summary this node was built from attributed the
N = 9 control to Anania. It belongs to Evens & Michael. Anania's artefact is the mastery
threshold; Evens & Michael's is the tiny control group. **Two different studies, two different
artefacts.***

⭐ **The constructive reading is the one worth carrying:** mastery learning — an
80–90% threshold that must be cleared before advancing — produced **~1.0 SD in a classroom, with
no tutor at all.** That is larger than step-based ITS against no tutoring, and it is a policy,
not a technology. → [spaced repetition](spaced-repetition.md),
[knowledge tracing](knowledge-tracing.md)

---

## ⭐⭐ Eight explanations for human tutoring, and six of them are dead

Before the meta-analysis, VanLehn works through the standing hypotheses for *why* human tutors
should be better. This is the most under-cited part of the paper and it is directly an argument
about **what not to build**.

| # | Hypothesis | Verdict |
|---|---|---|
| 1 | **Detailed diagnostic assessment** — tutors model misconceptions and adapt | **Dead.** Tutors "rarely know about their tutees' misconceptions, false beliefs, and buggy skills," rarely ask questions that would diagnose them, and **do not become more effective when handed that information** |
| 2 | **Individualized task selection** | **Dead, and backwards.** Human tutors follow a "curriculum script" — simple to difficult. Computer tutors already individualize *better*, "so on this argument, computer tutors should be more effective than human tutors" |
| 3 | **Sophisticated tutorial strategies** (Socratic irony, reciprocal teaching, inquiry) | **Dead.** Across 18 cited studies of tutors at many expertise levels, "such sophisticated strategies are **rarely used**" |
| 4 | **Learner control of dialogue** | **Dead.** Shah et al. found **146 student initiatives in 28 hours** of tutoring, 37% of them just "…right?" — about **one non-trivial student question every 18 minutes**, in high-stakes medical training |
| 5 | **Broader domain knowledge** | **Dead.** Tutors seldom deploy it on procedural content, and when they do offer deeper explanations, **suppressing them "did not affect the learning gains of tutees"** (Chi et al. 2001) |
| 6 | **Motivation** | **Unclear.** Praise is "associated with reduced learning gains in some cases"; text-mediated tutoring learns as well as face-to-face, so no "warm body" effect; some tutors give **false positive feedback** to protect self-efficacy |
| 7 | ⭐ **Feedback** — catch the error while the reasoning is fresh | **Survives** |
| 8 | ⭐ **Scaffolding** — prompt the next bit of reasoning rather than tell | **Survives** |
| 9 | **ICAP** (interactive ≥ constructive > active > passive) | Complementary, not competing — but "such coding has not yet been done for either human or computer tutoring" |

> "Of the other eight hypotheses… **only the last two seem completely free of contravening
> evidence.**"

### Why hypotheses 1 and 2 dying matters more to us than anything else in the paper

**The two dead hypotheses are the two things an LLM tutor is most tempted to build.**
Misconception diagnosis and adaptive task selection are the glamorous parts — and the evidence
says human experts do neither, and are not helped when you hand the diagnosis to them.

This is the same finding as [Andes removing its Bayesian network](../systems/andes.md) before
the results were produced, and it is what [TutorGym](../evaluation/tutorgym.md) measures from the
other end: **no model beats chance at labelling an incorrect student action.** We had filed those
as separate results. They are one result, and VanLehn stated it in 2011.

⚠ **Hypothesis 3 is worth reading twice before we write a Socratic system prompt.** Expert human
tutors, the people the Socratic ideal is modelled on, *do not do it.* → [Socratic
tutoring](socratic-tutoring.md), where students are documented routing around it anyway.

---

## ⭐ Expert tutors are not measurably better than novices

Table A10 is seven rows long and it undercuts a premise the whole field runs on.

| Comparison | Result |
|---|---|
| Fossati (2008), expert vs. novice | d = 0.04 |
| Chae et al. (2005), expert vs. novice | not significant |
| H. Johnson & Johnson (1992), Socratic vs. didactic, same people | d = 0.11 |
| Rosé et al. (2001), Socratic vs. didactic, same person | d = 1.00, **not reliable** |
| Evens & Michael (2006), expert vs. novice | d = 3.01, **reliable** |
| Chi et al. (2001), untrained vs. prompt-only constrained | not significant |
| di Eugenio et al. (2006) | significant, but the expert **taught different content** |

> "Only **two** of these comparisons showed a reliable difference in learning gains. Moreover,
> the **Cohen et al. (1982) meta-analysis found no relationship between tutor's experience and
> their effectiveness**… Clark et al. (1976) found that giving subject-matter experts training
> and experience as tutors did not make them more effective."

**What does differ is behaviour, not outcome:**

> **"Almost all these studies found that novice tutors tended to lecture more, and expert tutors
> tended to be much more interactive."**

⭐ **And one line buried in the di Eugenio footnote deserves to be a headline:** *"The novice
tutors, by the way, were no more effective than several Step-based Tutors."*

**Read together: expertise changes how a tutor behaves without changing what students learn, and
the plateau explains why — once you are interactive enough to get students to finish, more
interactivity buys nothing.** VanLehn's own summary: "once tutoring has achieved a certain
interactive granularity (roughly, step-based tutoring), decreases in interaction granularity
apparently provide diminishing and sometimes even negligible returns."

⚠ **The caveat he adds, and it is fair:** the "experts" in these studies may not be expert in
the deliberate-practice sense — "it is likely that few tutors video record and analyze their
performances." He argues both humans and ITS have large unrealised headroom, and cites Min Chi's
reinforcement-learning retuning of a substep tutor's pedagogical policy as **d = 0.84 over the
original system** — an ITS improving on itself by that much, without changing granularity.
**That is the largest single design-improvement effect size in the paper, and it came from
tuning the policy, not the interface.** → [a pedagogical policy outside the prompt](../PAPER.md)

---

## The scope limitation nobody quotes

> **"It is important to note that none of the field studies in this review completely replaced
> all classroom instruction with tutoring. Instead, they replaced or partially replaced just one
> activity (usually homework)."**

> "A classroom has many instructional activities that can have significant impacts on learning
> gains, so **upgrading just one activity does not guarantee large overall course learning
> gains.**"

And in the take-home section:

> "**None of the studies reported here even attempted to replace a classroom teacher with ITS**
> even though it is not uncommon for a human tutor to replace a classroom teacher… ITS should be
> used to replace homework, seatwork, and perhaps other activities but not to replace a whole
> classroom experience."

**0.76 is a homework-replacement effect size.** Every number in this review is the effect of
upgrading one activity inside an otherwise unchanged course. That is exactly the intervention
shape our project has, which is good — but it also caps what we can honestly promise.

⭐ **His actual recommendation reads like a description of our project:**

> "Step-based tutoring systems should be used (typically for homework) in **frequently offered or
> large enrollment STEM courses.**"

The economics argument is his too: development costs "do not depend on the number of tutees."
→ [cost economics](../practice/cost-economics.md)

**The best single-system number in the review is Andes:** four year-long evaluations at the US
Naval Academy, **d = 0.61** against students doing the same homework on paper (Table A1).
→ [Andes](../systems/andes.md)

---

## ⭐ A study in this review is our own project's ancestor

Table A8, human tutoring vs. step-based tutoring, contains this row:

> **d = −0.07 — "(Rose, Aleven, Carey, & Robinson, 2005) HT and SBT coached students designing
> Carnot engines. Data from one human tutor were excluded."**

**Carnot engines.** That is the [CycleTalk / CyclePad](../systems/cyclepad-cycletalk.md) line at
CMU and the Naval Academy, and it is in VanLehn's meta-analysis as a **null** — a step-based
tutor and a human tutor produced indistinguishable learning on thermodynamic cycle design, with
the sign marginally favouring the software.

**The closest thing to our course in the entire review is a null result against a human tutor.**
Whether that is encouraging or discouraging depends on which side of the comparison you were
hoping to be on. → [Rosé et al. 2005](../systems/cyclepad-cycletalk.md)

---

## The proximal–distal collapse

*(Kept from the previous version; the source for the Kulik & Fletcher, Ma and Steenbergen-Hu
figures is **Alkhatlan & Kalita's 2018 survey**, read in full — ⚠ still secondhand for those
three meta-analyses.)*

**Ma et al. 2014** — 107 effect sizes from 73 studies, the largest of the four:

| ITS compared against | d |
|---|---|
| Non-ITS computer-based instruction | **0.57** |
| Teacher-led / large-group instruction | **0.42** |
| Textbooks or workbooks | **0.35** |
| Small-group human instruction | **0.05** |
| ⭐ **Individualized human tutoring** | **−0.11** |

**ITSs beat every form of mass instruction and tie with a human tutor** — consistent with
VanLehn's 0.76 vs. 0.79.

**Kulik & Fletcher 2016** — 50 studies; 92% favoured the ITS; **median effect 0.66** across 39
of them. ⚠ **But the effect on *standardized tests* was 0.13.** A fivefold collapse between the
researchers' own measures and an external one.

| Study | Proximal measure | Distal measure |
|---|---|---|
| Kulik & Fletcher 2016 | **0.66** own measures | **0.13** standardized tests |
| [Tutor CoPilot](../systems/tutor-copilot.md) | **+4 p.p.** exit tickets | **null** end-of-year MAP |
| [CycleTalk](../systems/cyclepad-cycletalk.md) | **+0.35 SD** concept test | **null** both design exercises |
| [Andes](../systems/andes.md) | **+1.21** drawings, +0.69 variables | **−0.08** answers |
| [Bastani](../evidence/bastani-2025-harm.md) | **+48%** while assisted | **−17%** unassisted exam |

⚠ **And VanLehn's own numbers belong in this frame.** "This review reports the assessment with
the largest effect size" is a *proximal-selection rule applied to the whole literature*.
**Whatever we measure close to the tutor will look good.** Our evaluation has to lead with a
distal, unassisted, ideally externally-validated outcome, and we should expect it to be roughly
a fifth of whatever the in-app numbers say.
→ [concept inventories](../evaluation/concept-inventories.md),
[behavioral evaluation](../evaluation/behavioral-evaluation.md)

**Steenbergen-Hu & Cooper 2013** (K-12 maths, 26 reports) adds two moderators: **no significant
effect for short-duration use**, with effects appearing only at a **full school year or longer**
— and effects **larger for general students than for low achievers.**

---

## Why this is uncomfortable for our project

**A chat interface is not obviously step-based.**

A student who types "I'm stuck on 4b," reads three paragraphs, and types "oh ok thanks" has
externalized almost nothing. That is answer-based tutoring — the d ≈ 0.31 tier — with better
prose. Worse, by the completion mechanism, it is the *quitting* case: the solution arrived, the
student generated none of it, and the hundreds of knowledge-component applications never
happened.

[Andes](../systems/andes.md) got its results by making students enter vectors, coordinate
systems, variable definitions, and equations, with feedback after each. That is a *structured
problem-solving surface*, not a chat window.

**The design implication should be argued about explicitly by the team:** the most-evidenced
design in the history of this field is not a chatbot. If we build a chat interface because it is
what LLMs make easy, we are choosing the weaker interaction granularity for implementation
convenience.

A defensible synthesis: a **structured solving surface** where the student enters steps, with
conversational help alongside — the LLM providing what Andes could not (understanding a confused
question in natural language), the interface providing what chat cannot (mandatory
externalization, and a definition of "finished").

**And one thing we can take straight from Anania:** the mastery threshold. **90% to advance
produced 1.0 SD in an ordinary classroom.** It costs nothing to implement and it is the only
component of the 2-sigma result that survived scrutiny.

## Open questions

- [ ] **Has anyone re-run this analysis including LLM-era systems?** Fifteen years on, with a
      dozen RCTs now published, the plateau is testable again — and no LLM tutor in our base has
      been classified by granularity.
- [ ] **What is our "step" in a thermodynamics problem?** State identification, property lookup,
      which-law selection, algebraic manipulation, unit handling? The completion mechanism says
      the answer determines what "finishing" means.
      → [knowledge components](knowledge-components.md),
      [our skill graph](../../research/domain/skill-graph-draft.md)
- [ ] **Can an LLM tutor make quitting hard without making cheating easy?** VanLehn's mechanism
      says require completion; [Bastani](../evidence/bastani-2025-harm.md) says a student with an
      LLM will complete by copying. **That tension is the central design problem of this project**
      and nothing in the 2011 literature addresses it.
- [ ] Kulik & Fletcher 2016 and Ma et al. 2014 are still secondhand via Alkhatlan & Kalita.
- [ ] Suraweera & Mitrovic (2002) — the only direct step-vs-answer manipulation in the review.
      Worth acquiring given how much weight we put on that contrast.

## Connects to

- [Bloom's 2 sigma](blooms-two-sigma.md) — the claim this corrects, and the mastery-threshold answer
- [Andes](../systems/andes.md) — the exemplar step-based physics system, d = 0.61 over four years
- [Cognitive Tutor](../systems/cognitive-tutor.md) — Anderson et al. 1995, who proposed the completion mechanism first
- [CyclePad / CycleTalk](../systems/cyclepad-cycletalk.md) — Rosé et al. 2005 is in this review at d = −0.07
- [Productive failure](productive-failure.md) — the same mechanism from the generation side
- [TUM dissociation](../evidence/tum-dissociation-2025.md) — germane load is completion, measured
- [Knowledge components](knowledge-components.md) — what gets generalized, strengthened, constructed, debugged
- [Socratic tutoring](socratic-tutoring.md) — hypothesis 3, which expert tutors do not use
- [TutorGym](../evaluation/tutorgym.md) — hypothesis 1's modern restatement
- [Kestin 2025](../evidence/kestin-2025-rct.md) — the modern result that has to be read against these baselines

## Sources

- [VanLehn (2011), "The Relative Effectiveness of Human Tutoring, Intelligent Tutoring Systems, and Other Tutoring Systems," *Educational Psychologist* 46(4), 197–221](https://doi.org/10.1080/00461520.2011.611369) `[read — full text, 25 pp., 2026-09-03]` — **the primary.** Local: `course-materials/papers/vanlehn-2011-relative-effectiveness.pdf`
- [Alkhatlan & Kalita (2018), "Intelligent Tutoring Systems: A Comprehensive Historical Survey with Recent Developments," arXiv:1812.09628](https://arxiv.org/pdf/1812.09628) `[read — full text, 31 pp., 2026-09-01]` — ⚠ now only the source for **Ma et al. 2014** and **Steenbergen-Hu & Cooper 2013**; VanLehn and Kulik & Fletcher are held as primaries
- [Bloom (1984), "The 2 Sigma Problem," *Educational Researcher* 13(6), 4–16](https://doi.org/10.3102/0013189X013006004) `[found]` — dissected here via Anania (1981) and Burke (1983)
</content>
</invoke>
