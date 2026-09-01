# Productive Failure

**Type:** concept
**One line:** Struggling unsuccessfully with a problem *before* instruction produces better
conceptual understanding and transfer — **g = 0.36** — provided the struggle is followed by
instruction that contrasts the student's solutions against the canonical one.
**Why we care:** It is the theoretical basis for making a tutor wait, and the evidence is
specific enough to design against. It also contains the sharpest argument *against* what we are
proposing.

> **Fully rewritten 2026-08-31 from the primary literature.** This node previously named "two
> core design components: contrast-and-compare **and collaboration**." That framing was
> **substantially wrong** and has been replaced. Corrections marked ⚠.

## The meta-analysis, verified

**Sinha & Kapur (2021), *Review of Educational Research* 91(5):761–798.**
**53 studies / 166 comparisons** drawn from 45 articles (1,212 screened).

> *"a significant effect (Hedge's g) of **0.36 [95% CI 0.20, 0.51]** in favor of PS-I (compared
> to I-PS) for conceptual knowledge and transfer, and a nonsignificant effect of
> **−0.03 [−0.20, 0.15] for procedural knowledge**."*

⚠ **Four corrections to how this node used to cite it:**

1. It is **Hedge's g**, not Cohen's d.
2. **The "12,000+ participants" figure is not in the meta-analysis.** No total N is stated
   anywhere in it. That number comes from the Kapur & Roll book chapter — cite it there or drop
   it.
3. **"Up to g = 0.58" is not a composite.** It is the top of a range of seven subgroup point
   estimates, and *that particular row is marked non-significant*. Do not repeat the derived
   gloss that PF is "three times the effect a good teacher has in a year" — it is uncited and
   rides on a null subgroup.
4. ⚠ **Data-quality defect worth flagging in the capstone.** Tables 3–5 contain rows where the
   point estimate falls **outside its own confidence interval** (e.g. undergraduates
   `0.28 [−0.46, 0.24]`). This is in the published PDF, not a transcription artifact.
   **Treat every subgroup CI in this paper as unusable**; only point estimates and significance
   markers are trustworthy.

Heterogeneity Q(165) = 295.91, p < .0001; I² = 42.01%. Egger's test n.s.; p-curve right-skewed,
estimated power 94%, bias-corrected true effect **g = 0.87**.

**⚠ Do not quote 0.87 as "the" effect.** Egger's test was *not* significant (intercept = 0.63,
p = .219) and **no studies were imputed in trim-and-fill** — the standard small-study-bias
correction found nothing to correct. The 0.87 comes from a **separate p-curve estimator**, which
infers a true effect from the shape of the significant-p distribution and is known to run high
under heterogeneity. **The defensible number is g = 0.36 [0.20, 0.51].**

## ⚠ Correction: seven design criteria, not two — and collaboration isn't one of the essential ones

The seven fidelity criteria, with their subgroup effects:

| Criterion | High | Low | Sig |
|---|---|---|---|
| **Instruction building on student solutions** | **0.56** | **0.20** | **p = .02** |
| Social surround, instruction phase (dialogue vs monologue) | 0.55 | 0.24 | p = .05 |
| **Group work as participation structure** | 0.49 | 0.19 | p = .04 |
| **Evidence of multiple solution generation** | **0.47** | **0.16** | **p = .05** |
| Affective draw of the problem | 0.44 | 0.19 | n.s. |
| Problems affording multiple solutions | 0.37 | −0.11 | n.s. |
| Social surround, problem-solving phase | 0.58 | 0.36 | n.s. |

**Overall fidelity is a significant predictor: β = 0.0065, p < .001** — about 0.65 g across the
full range. By stepwise ranking, **instruction building on student solutions is #1** and
**evidence of multiple solution generation is the genuine #2**.

## ⭐⭐ The finding that most constrains our design: fidelity *reverses* in short sessions

Fidelity and session length are confounded — longer interventions score higher. Overall PF
fidelity averages **74.45% (SD 22.64)** for interventions spanning a few days versus **42.01%
(SD 26.13)** for those spanning a few hours (Welch t(154.22) = 8.504, p < .001). So the authors
ran meta-regressions with the interaction terms. Three results, all about short sessions:

| Interaction | Effect | Reading |
|---|---|---|
| Overall fidelity × few-hours span | **β = −0.0116, p = .0546** | ⚠ **More design features makes short sessions *worse*** |
| Affective draw × few-hours span | **β = +0.7322, p = .0732** | ⭐ The problem being *interesting* matters most when time is short |
| Group work × few-hours span | **β = +0.7395, p = .0023** *(for group work absent)* | ⭐ **Individual** work wins in short sessions |

The authors' own words: *"cramming too many design features within a short amount of time may
not be optimal."*

**A tutoring session is a "few hours" intervention at best, and usually far less.** The literal
implication for us: **do not try to implement all seven fidelity criteria in one sitting.** Pick
the two that survive the interaction — a problem with genuine **affective draw**, worked
**individually** — and then spend the fidelity budget on the instruction phase (building on what
the student actually produced), which is the #1 criterion overall.

This also reframes the group-work moderator. Group work is a real positive main effect
(0.49 vs 0.19, p = .04), but it is (a) confounded with fidelity and study type and (b) *reversed*
at our session length. **A 1:1 tutor is not disadvantaged by being 1:1.**

## By domain, and by our student population

Effect sizes by target concept (point estimates only — the CI column in Table 5 is corrupted the
same way; see the warning above):

| Domain | Hedge's g |
|---|---|
| Mathematics | 0.48 |
| Chemistry | 0.48 |
| **Physics** | **0.39** |
| Environmental science | 0.56 |
| Biology | 0.32 |
| Medicine | 0.24 |
| ⚠ **Domain-general skills** | **−0.17** — the only significant subgroup difference in the table, and it is negative |

**Physics at 0.39 is the closest proxy we have for engineering thermodynamics**, and it sits just
above the pooled estimate. No thermodynamics study is in the sample.

By outcome type: **transfer 0.40, conceptual 0.33, clubbed 0.31**, no significant differences.
PF is *not* specifically a transfer intervention in this data, despite that being its usual claim.

**⚠ And a caveat about our exact population.** Effect sizes rise monotonically with grade level
(2nd–5th graders are *negative*), but *"age range… had (marginally) significant subgroup
differences for **all** student subcategories (**except for undergraduates**)."* Undergraduates
are the one group whose subgroup difference did not reach significance. Higher PF fidelity
predicts higher effects for undergraduates only marginally (β = 0.0080, **p = .0934**), versus
robustly for 6th–10th graders (β = 0.0190, p < .0001). **The undergraduate evidence is the
weakest link in the chain we are relying on** — worth stating plainly in any proposal.

Two more moderators worth knowing: **quasi-experimental studies show 0.46 versus 0.25 for
experimental** ones — tighter control, smaller effect, the usual direction — and interventions
run in **Asia scored significantly higher** than in Europe or North America.

The old "contrast-and-compare + collaboration" pairing came from Mazziotti et al. (2019) — a
paper whose own experiment supported **neither** (collaboration effect F(1,224) = 1.16, p = .28).

## ⭐ Collaboration is not required — build the solo tutor

This was our biggest open question. It is settled.

| Study | Level | Generation structure | Effect |
|---|---|---|---|
| **Kapur 2014, Study 1** | Grade 9 | **Individual, no help** | **conceptual d = 2.00**, transfer d = 1.52 |
| **Kapur 2014, Study 2** | Grade 9 | **Individual, no help** | **conceptual d = 2.25**, transfer d = 1.29 |
| **Sinha & Kapur 2021 (*L&I*)** | **University** | **Individual, computer-mediated (Jupyter)** | transfer **d = 0.56 [0.03, 1.08]** |
| Chowrira 2019 | University | Groups of 2–4 | d = 0.32 |
| Mazziotti 2019 | Grade 5 | **Dyads vs individual, directly contrasted** | **collaboration effect null** |

**Kapur 2014 ran generation individually and unguided, and produced the largest effects in the
entire literature.** In his words: *"Students worked individually without any help as indeed one
would in an examination setting"* — and he frames this as the point, *"an important
demonstration of the effectiveness of unguided problem solving prior to instruction."*

**Why the significant group-work moderator doesn't overturn this:** it is confounded with
overall fidelity. Classroom (quasi-experimental) studies use groups and average **76.78%**
fidelity; lab experiments use individuals and average **32.36%**. And a meta-regression finds
that **for short interventions, individual work predicts better outcomes** (β = 0.7395,
p = .0023) — which is exactly our session length.

*Citation warning:* Kapur & Roll cite Mazziotti 2019 for "PF is effective in both
configurations." The claim is defensible; that citation is not. **Cite Kapur 2014.**

## ⭐ The hard constraint: generation cannot be replaced by showing wrong answers

Kapur 2014 **Study 2** tested exactly the shortcut a 1:1 tutor is tempted to take. A
**vicarious failure** condition replaced generation with an hour studying and evaluating six
peer-generated failed solutions, rendered as well-designed worked examples.

- **PF > VF: conceptual d = 1.35, transfer d = 1.23**
- **VF > DI on conceptual only (d = 0.80) — no transfer advantage at all**
- Solutions **generated** correlated r = .82 / .88 with outcomes. **Evaluations performed
  correlated with nothing.**

> *"students must themselves generate and explore solutions and **not simply be presented with
> peers' solutions**."*

**Rule: suboptimal representations may scaffold generation or feed consolidation, but must
never substitute for the student's own generation.** A tutor that opens with "here are three
common mistakes" has built the vicarious-failure condition and forfeited the transfer effect.

| Move | Timing | Verdict |
|---|---|---|
| Student generates unaided | Attempt 1, ~20 min | **Required** |
| Tutor nudges toward specific suboptimal representations | Attempt 2, on demand, one at a time | **Do this** |
| Tutor replays typical wrong solutions | Consolidation | Fine (may be pre-authored) |
| Tutor presents others' failed solutions *instead of* generating | Replaces attempt 1 | **Never** |

## ⭐ The finding that most changes our design

From the *L&I* university replication:

> *"across both attempts, only **one** student in the Productive Failure condition generated a
> one-dimensional histogram (one of the three suboptimal scaffolds explicitly offered to the
> Failure-driven condition students)… students in the Productive Failure condition were **not
> likely to naturally come up with suboptimal representations**."*

**Students left to struggle unaided do not spontaneously produce the productive wrong answers.**
Unscaffolded PF was **worst on transfer** (0.39 vs 0.60) and left students **over-confident**.

So the tutor's job is not to wait quietly. It is to **actively steer students into specific,
pre-authored suboptimal representations** — released **moderately-wrong → extremely-wrong →
nearly-right**, on demand, one at a time, with the student required to declare the previous one
unhelpful to unlock the next. That ordering is deliberate: it stops students settling early and
defeats hint-abuse.

The authors close by naming our system as the next step: *"Such personalization, which can
iteratively and naturally gauge students' understanding (e.g., by holding casual
conversations)… is likely to improve students' metacognition."*

## Consolidation is strictly required — and Kapur 2008 is miscited for it

**Kapur 2016** defines failure without subsequent instruction as **unproductive failure**:
*"there is an efficacy of unguided problem solving, **but only if some form of consolidation and
instruction follows**."*

⚠ **Kapur (2008) is routinely cited as evidence for the two-phase design. It has no
consolidation or instruction phase at all** — the word "consolidation" appears zero times in
48 pages. Its design is ill-structured group problem solving → post-tests. **Cite Kapur 2016 for
the requirement, Kapur & Bielaczyc 2012 for the teacher moves, Kapur 2012 for the contrast
list.** Cite Kapur 2008 only for what it shows: unguided ill-structured problem solving has
latent preparatory value *even when the solutions produced are worse* (F = 7.200, p = .009).

**The teacher-move sequence** (Kapur & Bielaczyc 2012): students share their solutions →
**compare and contrast the affordances and constraints of the student-generated solutions
against each other** → present the canonical solution → *"drew comparisons and contrasts between
the canonical and student-generated"* solutions → practice problems.

During generation the teacher's role is explicitly **non-cognitive**: *"not to provide any
cognitive or content-related support but mainly to manage the classroom and provide affective
support"* — assuring students *"that it was okay not to be able to solve the complex problems as
long as they tried various ways."*

**⭐ The single most copyable artifact in this literature** is Kapur 2012's **pairwise contrast
list** for teaching variance — each contrast mapped to the deep feature it teaches (central
tendency vs qualitative → same mean, different variance; signed vs absolute deviations → why
signs must not cancel; sum vs average → why dividing by n enables cross-sample comparison; and
so on). **Build the thermodynamics equivalent for our target concept.** That list *is* the
consolidation design.

Practical relief: Mazziotti used **canned** typical wrong solutions from prior cohorts rather
than live student work, *"to keep the instruction constant."* We can pre-author a bank.

## ⚠ The strongest argument against our design

**Scaffolded PS-I has failed on average: Hedge's g = −0.08 [−0.20, 0.04], N = 60 comparisons.**
Undergraduate subset: **g = −0.08 [−0.34, 0.28]**.

"Scaffolded PS-I" means support added *during* the problem-solving phase — accuracy feedback,
cognitive hints toward correct steps, question prompts, self-explanation prompts, and
**Khan-Academy / Carnegie-Learning / ASSISTments-style hint sequences**, which the source names
explicitly.

**That is the thing we are proposing to build.** The converging explanation is that guidance
during generation improves *solutions* without improving *learning*:

- Kapur 2011: guided generation produced correct solutions where PF students produced none —
  and PF beat both guided generation and direct instruction on the post-test, while *"the
  differences between guided-generation and direct instruction were not significant."*
- Loibl & Rummel 2013 replicated it.
- Chowrira's mechanism: *"Having a solution may encourage students to accept it 'at face value',
  without dissecting its deep structure."*

**The known exception is what defines our design space.** PF matches scaffolded PS-I when
support is **principle-based** (definitions, conditions of applicability, relevant equations)
or **metacognitive** — never *"clarifications and hints regarding correct solution steps,
accuracy feedback."*

Two field-tested scripts:

- **Metacognitive (Chowrira, university):** *"what information do you have in the problem?"* →
  *"what other kind of information would you need to continue?"* → *"where might you find
  this?"* — *"prompts to focus students' attention **without providing additional
  information**."*
- **Failure-driven on demand (*L&I*):** three suboptimal representations, pull not push.

⚠ **And a warning about our likely outcome measure:** success-driven (canonical-directed)
scaffolding **beat** failure-driven scaffolding on the isomorphic post-test, **d = −0.50**.
Guidance wins when the test resembles training. **If the course is assessed on near-isomorphic
problem sets, PF may not show up in grades at all.**

## The university anchor, and its caveats

**Chowrira et al. (2019), *npj Science of Learning* 4:1.** N = 574 first-year UBC Cell Biology
students (PF 295, AL 279), two topics, **designed and implemented by the course instructors —
"DIY," directly analogous to our position.**

- PF: ~25 min small-group exploration with *"minimal or no introduction,"* responses **not
  marked for correctness** → ~5 min feedback using student responses as clicker options →
  ~20 min instructor walkthrough building on student mistakes.
- Control: **active learning**, not lecture — *"better instruction than passively listening."*
- **Midterm 2: b = 4.78 [2.19, 7.36], p < 0.001, effect size 0.32 [0.15, 0.49]**
- **Final exam overall: b = 0.78, p = 0.668 — null**

⚠ **Design caveats:** quasi-experiment with self-selected sections; the PF section was
**already higher before the manipulation** (d = 0.44 on Midterm 1 and on final non-study items);
**Cronbach's α = 0.574 and 0.555** on the outcome measures; **one instructor taught PF**, so
instructor effects are confounded with condition.

## Equity — the evidence runs *toward* us

Chowrira's ternary ability split:

| Ability | Midterm 2 | Final exam |
|---|---|---|
| **Low** | **b = 8.28 [3.68, 12.89], p < 0.001** | b = 6.83, p = 0.060 |
| Medium | b = 3.26, p = 0.193 | n.s. |
| High | b = 3.37, p = 0.105 | n.s. |

**Low-prior-knowledge students gained more than twice as much, and were the only group with
durable gains.** No subgroup was harmed. Kapur & Bielaczyc likewise found PF **never worse than
direct instruction on any measure in any school**, including below-average-ability schools.

⚠ Hedge it: post-hoc split of a quasi-experiment with α ≈ 0.56; the authors call the subgroup
splits *"more suggestive than conclusive."*

**The at-risk profile is not low ability — it is performance-orientation.** Students who
*"primarily seek to demonstrate ability… may view challenging task situations as a threat and
withdraw effort."* **That is measurable up front with a goal-orientation instrument**, and it is
a far better screen than prior grades.

Other genuine losses: **grades 2–5 (g = −0.09, p < .01)**; **domain-general skills
(g = −0.17, p = .05)**; non-STEM (Nachtigall, both studies null — *"effectiveness may only
emerge for learning in structured domains"*; thermodynamics qualifies); repeated failure
demoralizes; and over-generation can backfire.

**The affective ceiling is real and both university teams hit it.** Chowrira's students *"gave
up out of sheer frustration"* until moderate support was added. Kapur & Bielaczyc removed
extension problems in a lower-frustration-threshold school and reallocated the time to **extra
consolidation**. **Lower prior knowledge → shorter struggle and more consolidation, never a
reversion to direct instruction.**

## The struggle budget

| Study | Level | Generation | Consolidation |
|---|---|---|---|
| **Sinha & Kapur (*L&I*)** | **University** | **20 min unscaffolded + 20 min on-demand hints** | **20 min** (5 concept / **10 contrast** / 5 canonical) |
| **Chowrira 2019** | **University** | **~25 min** | ~5 min feedback + ~20 min walkthrough |
| Kapur 2014 | Grade 9 | 60 min | 60 min |

**The two university studies converge: ~20–25 min unscaffolded generation, then hints, then
~20–25 min consolidation — one class period.**

⚠ **Nobody in this literature ever measured optimal struggle duration.** Every number is a
timetable, not an optimization. The meta-analysis offers no phase-level guidance.

**Escalate on stalled solution generation, not the clock.** Solution count is the mechanism and
it is measurable: r = .65–.88 with conceptual understanding and transfer; solution diversity
partial η² = .80, *"about 9 times stronger than the pretest."* PF students produce ~6 distinct
solutions vs ~3 for direct instruction. **Count solutions the student *produced* — not solutions
they saw.**

## ⚠ Two standing risks

1. **Undergraduates are the weakest-supported adult band.** Grades 6–10 g = 0.50 (p = .05);
   postgraduate g = 1.03 (p = .05, only 5 comparisons); **undergraduates g = 0.28, not
   significant.** And of 166 comparisons: **zero engineering, zero thermodynamics.** Physics
   topics are "average speed, density, collision, electricity, mechanics."
2. **Element interactivity.** Ashman et al. (2020), flagged in the meta-analysis's own
   limitations: *"advantages of PS-I over I-PS may diminish with increasing complexity."*
   **Thermodynamics is high element-interactivity.** State this extrapolation explicitly rather
   than letting a reviewer find it.

Also worth stating honestly: **"PF doesn't hurt procedural knowledge" is weaker than it sounds.**
The nulls come from measures at ceiling — Kapur 2014's procedural means were 9.24/10 vs 9.47/10,
and he flags it himself. Say **"no evidence of harm," not "demonstrated equivalence."**

## What this all adds up to for us

**Design spec the evidence supports:** ~20–25 min individual generation on a problem with
invariant surface features and variant deep structure → tutor supplies **pre-authored
suboptimal representations** on demand, one at a time, moderate → extreme → near-miss → hints
restricted to **principle-based and metacognitive** content, never step-level → **mandatory
~20–25 min consolidation built on an explicit pairwise contrast list** ending in the canonical
solution. Escalate on stalled solution count. Cap consecutive failures. Screen for
performance-orientation.

**And frame the contribution honestly:** scaffolded PS-I usually fails, the failure-driven
design is the known exception, and the *L&I* authors explicitly name adaptive conversational
scaffolding as the next step. **That gap is our capstone's contribution — it should be presented
as an open question we are addressing, not as settled ground.**

## Open questions

- [ ] **Verify Darabi et al. 2018 at source** (g = 0.43 [0.19, 0.68] reaches us only
      second-hand). Needs library proxy. Note only 12 experimental studies met inclusion, and
      all three of its moderators were non-significant — read that as underpowered, not as
      "PF works everywhere."
- [ ] Get Kapur 2012's journal version for exact statistics and the full contrast list.
- [ ] **Build the thermodynamics pairwise contrast list.** Highest-value single artifact.
- [ ] Which thermodynamics problems afford multiple solution representations? That is criterion
      #1 and it constrains problem selection.

## Connects to

- [Socratic tutoring](socratic-tutoring.md) — why the ladder must terminate in contrast
- [Bastani 2025](../evidence/bastani-2025-harm.md) — the crutch effect this explains
- [engagement decay](engagement-decay.md) — the force pulling against the struggle budget
- [equity](../practice/equity.md) — the low-ability finding
- [Betty's Brain](../systems/bettys-brain.md) — failure as the designed centrepiece
- [VanLehn 2011](vanlehn-2011.md) — the substep anomaly this may explain

## Sources

- [Sinha & Kapur (2021), "When Problem Solving Followed by Instruction Works," *RER* 91(5), 761–798](https://www.research-collection.ethz.ch/handle/20.500.11850/490417) `[read — full text, 39 pp., 2026-08-31]` — the meta-analysis. **Sage blocks scripted download; ETH Zürich hosts the CC-BY copy** (DOI 10.3929/ethz-b-000490417). Fetch it through the DSpace REST API — recipe in [the wiki README](../README.md#getting-a-paper-that-looks-paywalled).
- **Sinha & Kapur (2021), "Robust effects of explicit failure-driven scaffolding," *Learning and Instruction* 75:101488** `[read]` — **the university, individual, computer-mediated replication; source of the g = −0.08 scaffolded-PS-I null**
- [Chowrira, Smith, Dubois & Roll (2019), "DIY productive failure," *npj Science of Learning* 4:1](https://www.nature.com/articles/s41539-019-0040-6) `[read]`
- Kapur (2014), *Cognitive Science* 38(5):1008–1022 `[read]` — **individual generation; the vicarious-failure comparison**
- Kapur (2016), *Educational Psychologist* 51(2):289–299 `[read]` — unproductive failure; the 2×2
- Kapur & Bielaczyc (2012), *JLS* 21(1):45–83 `[read]` — teacher-move sequence
- Kapur (2008), *Cognition and Instruction* 26(3):379–424 `[read]` — ⚠ **has no consolidation phase; commonly miscited**
- Mazziotti, Rummel, Deiglmayr & Loibl (2019), *npj Science of Learning* 4:2 `[read]` — the direct collaboration test, null
- Nachtigall, Serova & Rummel (2020), *Instructional Science* 48:651–697 `[read]` — non-STEM nulls
- Sinha & Kapur (2019), "When Productive Failure Fails," CogSci `[read]` — the boundary-conditions list
- Darabi, Arrington & Sayilir (2018), *ETR&D* 66(5) `[abstract only]` — **unverified at source**
- Loibl, Roll & Rummel (2017), *Educational Psychology Review* `[inaccessible]` — triangulated via quotations
