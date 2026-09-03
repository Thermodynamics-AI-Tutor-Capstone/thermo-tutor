# The dissociation: performance rose, learning did not (TUM, N = 275)

**Type:** evidence
**One line:** A three-arm RCT that separates a **scaffolded** AI tutor from **unrestricted**
ChatGPT and from no AI at all — and finds that **both AI conditions raised task scores while
neither raised learning.**
**Why we care:** This is [Bastani](bastani-2025-harm.md) refined, in a university course, with the
guardrailed arm tested properly. It is the cleanest statement of the trap our project has to
avoid, and its title says it: *performance and learning dissociate.*

> **Verification: `[read — full text, 21 pp., 2026-09-03]`.** Local copy:
> `course-materials/papers/bassner-2025-tum-dissociation.pdf` (+ `.txt`). **This node was
> `[abstract only]` until now** — Elsevier 403s scripted access, but the article is CC-BY gold OA.
> ⚠ **Reading the full text made the headline weaker in two places and added a third finding we
> had missed entirely.** Marked ⚠⚠ below.

Bassner, P., Lenk-Ostendorf, B., Beinstingel, R., Wasner, T. & Krusche, S. (2026). *"Less stress,
better scores, same learning: The dissociation of performance and learning in AI-supported
programming education."* **Computers and Education: Artificial Intelligence** 10, 100537.
[DOI 10.1016/j.caeai.2025.100537](https://doi.org/10.1016/j.caeai.2025.100537).
Technical University of Munich. ⭐ **Dataset and analysis code are public:**
[Zenodo 10.5281/zenodo.16905779](https://doi.org/10.5281/zenodo.16905779) — the only study in
this knowledge base we could re-analyse ourselves.

## Design

**N = 275 analysed** (from 452 enrolled — see ⚠⚠ below), introductory programming (CS1) at TUM,
across **35 tutorial sessions with 19 tutors**. A **90-minute exercise** on concurrency —
implementing a parallel sum with threading. Three randomised arms:

| Arm | n | What students got |
|---|---:|---|
| **Iris** | 91 | A **scaffolded tutor** — four-tier calibrated hints, full solutions withheld |
| **ChatGPT** | 88 | **Unrestricted** assistance, free to hand over complete solutions |
| **Control** | 96 | No AI; web search, docs, StackOverflow |

Randomisation checks passed on gender, age and prior programming experience (all p > .05).

**Note what makes this better than most:** performance and learning are measured by *different
instruments*, so the dissociation can actually be observed rather than assumed.

## ⚠⚠ The result, with the numbers

**Performance — a very large effect:**

| Measure | ChatGPT | Iris | Control | test |
|---|---:|---:|---:|---|
| **Exercise performance** (% test cases passed) | **71.84** | **57.50** | **29.85** | F = 29.69, p < .001, η²g = .179 |
| Exercise duration (min) | 88.2 | 90.9 | 91.3 | **n.s.** (p = .142) |
| Code comprehension (0–3) | 1.36 | 1.43 | 1.18 | **n.s.** (p = .136) |

Pairwise (Tukey HSD): **ChatGPT vs. control d = 1.10**, **Iris vs. control d = 0.76**, ChatGPT vs.
Iris d = 0.38 (p = .031). **All three arms differ from each other. GPT > Iris > control.**

⭐ **Duration was identical.** Students with AI did not work longer; they got further in the same
time. The authors: *"they simply accomplished more within the same timeframe."*

**Learning — nothing:**

| | ChatGPT | Iris | Control |
|---|---:|---:|---:|
| Knowledge, T1 (0–6) | 2.33 | 2.18 | 1.92 |
| Knowledge, T2 (0–6) | 3.16 | 2.89 | 2.77 |
| **Gain** | **0.83** | **0.71** | **0.85** |

Repeated-measures ANOVA: main effect of **time p < .001** (everybody learned something), main
effect of **group p = .311**, **time × group interaction p = .773**.

> **"Both AI groups achieved substantially higher exercise scores than the control group…
> Despite these performance gains, neither AI condition produced greater pre–post knowledge gains
> or code-comprehension advantages."**

**Neither.** Not just the unguardrailed arm — **the scaffolded, hint-withholding tutor also failed
to produce a learning gain.** Same shape as
[Bastani's guardrailed arm scoring the same as controls](bastani-2025-harm.md).

⭐ **A detail the abstract hides: the control group had the numerically largest gain (0.85).**
The arm that scored 29.85% on the exercise learned as much as the arm that scored 71.84%. That is
the dissociation in one line, and it is stronger than "no significant difference."

**The score distributions are the detail worth keeping:**

- **ChatGPT users clustered at high scores**
- **Control participants clustered at low scores**
- **Iris users spread across the full range**

The scaffolded tutor did not compress everyone to the top. It let students land where their
understanding put them — which is what an assessment is supposed to do, and exactly what
[the deployed RAG+SRL tutor's "variance compression"](../systems/rag-tutor-southeast.md) did *not*
do. The authors' framing: *"ChatGPT makes everyone succeed uniformly, while Iris makes everyone
able to try meaningfully."*

## ⭐ The mechanism: germane load went *down*

| Cognitive load (5-point, higher = more) | ChatGPT | Iris | Control | vs. control |
|---|---:|---:|---:|---|
| Intrinsic (task complexity) | 3.81 | 3.59 | 3.81 | **n.s.** (p = .080) |
| ⭐ **Germane** (schema building) | **3.56** | **3.83** | **4.28** | d = **−0.77** / **−0.56**, p < .001 |
| Extraneous (wasted effort) | 3.13 | 3.31 | 3.86 | d = **−0.87** / **−0.70**, p < .001 |
| **Frustration** | 3.13 | 3.21 | **4.09** | d = **−0.87** / **−0.81**, p < .001 |
| **Intrinsic motivation** | 2.64 | **2.82** | 2.42 | Iris d = **0.55**, p < .001; **GPT p = .076** |

**Reducing germane load is the finding.** Extraneous load is wasted effort and cutting it is good.
**Germane load is the effortful schema-building that *constitutes* learning** — so a tool that
reduces it has removed the work that produces understanding. That is a mechanism, not just a
correlation, for why scores rose and learning did not.

⭐ **The ordering is exactly what the theory predicts, and it is monotone:** control 4.28 → Iris
3.83 → ChatGPT 3.56. **The more the tool gives away, the less schema-building work is left.**
Scaffolding bought back *some* germane load — but not significantly (Iris vs. ChatGPT p = .191),
and not enough to show up in knowledge.

⭐ **Intrinsic load did not move.** The task was equally hard in all three arms; what changed was
how much of the hard part the student did. That is a cleaner isolation than
[Bastani](bastani-2025-harm.md) achieved.

→ [productive failure](../concepts/productive-failure.md), whose entire premise is that the
struggle is the point; and
[VanLehn's completion mechanism](../concepts/vanlehn-2011.md), of which this is the measured form.

### ⭐⭐ Our reading: no arm actually satisfied VanLehn's precondition

*This is our inference, not the authors'.* [VanLehn's explanation](../concepts/vanlehn-2011.md)
for why tutoring works is that the student **finishes a correct solution having done most of the
reasoning**. Check each arm against that:

| Arm | Reached the end? | Did the reasoning? |
|---|---|---|
| Control (29.85%) | **No** | yes, as far as they got |
| ChatGPT (71.84%) | partly | **No** |
| Iris (57.50%) | **No** | yes |

**Nobody both finished and reasoned.** On VanLehn's account the study never created the condition
under which learning is predicted, which is a more specific explanation of the triple null than
"90 minutes is too short." **It also names what a fourth arm would have to do: hold students to
completion *and* withhold the solution** — which is mastery learning with a hint ladder, and
[nothing in this knowledge base has tested it](../concepts/blooms-two-sigma.md).

## ⭐ "The comfort trap" — and the nuance the abstract drops

> **"Scaffolded, hint-first design preserved motivational benefits, whereas AI providing
> unrestricted solutions encouraged a 'comfort trap' where students' preferences misaligned with
> pedagogical effectiveness."**

Head-to-head perception ratings (n = 179, positive d favours ChatGPT):

| Item | d | p |
|---|---:|---:|
| Helped resolve exercise issues | **0.63** | < .001 |
| Improved concept understanding | **0.49** | .001 |
| AI was easy to use | **0.45** | .003 |
| Feedback was helpful | **0.44** | .004 |
| AI understood queries | **0.38** | .011 |
| More effective than traditional methods | 0.22 | n.s. |
| General helpfulness for understanding | 0.14 | n.s. |
| ⚠ **Overall AI experience** | **−0.29 (favours Iris)** | .059 |

⚠⚠ **The comfort trap is real but narrower than we had it.** On every *instrumental* judgement —
did it help me, did it understand me, was it easy — **ChatGPT won clearly.** But on the two
*summary* judgements, students split: general helpfulness was a tie, and **"overall AI experience"
leaned towards Iris and nearly reached significance.**

**The honest statement is: students judged the answer-giving tool more useful in the moment while
rating the scaffolded tool slightly better overall.** That is a more actionable finding than
"students prefer the worse tool" — it says the pedagogy is not doomed on satisfaction grounds, it
just loses every question phrased as "did this help me right now."

⚠ **So do not use in-the-moment student satisfaction as a proxy for tutor quality.** It selects
for answer-giving. → [LearnLM being called "patronizing"](../systems/learnlm.md),
[UIC students preferring more succinct answers](student-ai-perceptions-2025.md).

⭐ **And only Iris raised intrinsic motivation** (d = 0.55 vs. control, p < .001) while ChatGPT
did not (p = .076) — despite ChatGPT scoring higher and being rated more helpful. The authors read
this through Self-Determination Theory: both tools supported *competence*, but only Iris preserved
*autonomy*. ⚠ *Note all three motivation means sit below the scale midpoint of 3.0, so this is
"less unmotivated," not "motivated."*

## ⭐⭐ Iris's architecture — the part we should copy

This was invisible from the abstract and it is the most directly reusable content in the paper.
Iris runs on **GPT-4**, embedded in TUM's **Artemis** LMS, and it is a five-layer build that maps
almost exactly onto [our convergent architecture](../PAPER.md):

- **LMS-native context, not copy-paste.** Iris reads problem statements, grading rubrics, the
  student's *current* code, prior attempts and **build logs** directly. *"Upon detecting repeated
  test failures, the agent can fetch the failing log, locate the relevant lecture snippet, and
  generate a hint."* → [LMS integration](../practice/lms-integration.md)
- **An agent, not a pipeline.** ART-style multi-step reasoning with tool calls (code analysis,
  lecture retrieval) looping until it has enough evidence.
- **Multimodal RAG over the actual course.** Slide text *and* video transcripts chunked and
  embedded; ⭐ **diagram-only slides are auto-captioned so text retrieval can reach them** — a
  concrete answer to [the diagram gap](../domain/diagram-reading.md) that costs nothing at query
  time. HyDE query expansion, **hybrid dense + keyword retrieval**, listwise cross-encoder
  reranking, top 3–5 snippets. → [RAG in education](../concepts/rag-in-education.md)
- **A cite-only directive**, with **slide numbers and video timestamps** in the output so
  instructors can verify and students can follow up.
  → [grounding and verification](../concepts/grounding-and-verification.md)
- ⭐⭐ **A four-tier hint ladder that never bottoms out in the answer** — the authors' *"Calibrated
  Assistance"*:
  1. **Subtle hints** — point at a code line or a conceptual blind spot
  2. **Guiding questions** — *"How does your loop behave on an empty list?"*
  3. **High-level conceptual feedback** — the approach, not the implementation
  4. **Generalized examples** — an analogous pattern, *"deliberately keeping the target solution
     opaque"*

⚠⚠ **That last point contradicts a standing recommendation in our own paper.** [§V.4 says the hint
ladder "must terminate in an explicit contrast against the canonical solution."](../PAPER.md)
Iris deliberately never terminates there — and classical step-based ITSs, which *do* have a
[bottom-out hint](../concepts/vanlehn-2011.md), are the systems that produced d = 0.76. **Iris
produced no learning gain.** One study is not enough to settle it, but this is now a live
disagreement rather than a settled design point, and it should be argued about explicitly.
→ [Socratic tutoring](../concepts/socratic-tutoring.md)

## ⚠⚠ Limits — and one we did not know about

**1. 39.2% of enrolled participants were excluded.** This is the largest single caveat and it is
absent from the abstract. **452 enrolled → 275 analysed.**

| Exclusion reason | n | % |
|---|---:|---:|
| Timing inconsistencies | 48 | 10.6 |
| Outside study window | 40 | 8.8 |
| Attention checks failed | 26 | 5.7 |
| No chat history (AI arms) | 22 | 4.9 |
| Demographic data issues | 20 | 4.4 |
| Implausible/missing duration | 17 | 3.8 |
| Opt-out | 4 | 0.9 |

The authors' defence is fair: criteria were **pre-specified and applied uniformly**, and retention
was similar across arms (57.1% / 60.7% / 64.9%). But they concede *"it's not possible to compare
their characteristics on the primary outcome measures"* — the excluded students are gone. **The
analysed sample is the subset who followed protocol, which is not the population a deployed tutor
would serve.**

**2. ⚠ The instruments are much smaller than "validated scales" suggests.** We previously
described these as validated scales without saying how short they are:

| Instrument | Items |
|---|---:|
| Knowledge assessment (T1 and T2) | **6** |
| Code comprehension | **3** |
| Intrinsic / germane cognitive load | **2 each** |
| Extraneous cognitive load | 3 |
| ⚠ **Frustration** | **1** |
| Intrinsic motivation (IMI interest/enjoyment) | 7 |

The authors say so themselves: *"while ICL and GCL subscales contain only two items each, which
limits traditional reliability assessment… Results for two-item subscales should be interpreted
with caution."* **The germane-load result — the mechanism this node leads with — rests on two
Likert items.** It is the most theoretically important number in the paper and the least
robustly measured.

**3. ⚠ The identical six-question test was given twice, 90 minutes apart.** Part of the ~0.8-point
gain in every arm is a retest effect, and a 0–6 scale has almost no room to separate three groups.
The authors flag *"the coarse granularity of the Code Comprehension measure (0–3 points) may
reduce sensitivity."*

**4. No delayed post-test.** *"The absence of delayed testing prevents conclusions about retention
or the durability of any observed learning effects."* → this is where
[the productive-failure literature says the effect appears](../concepts/productive-failure.md), so
its absence is not neutral.

**5. One 90-minute session, one topic, one CS1 course, one institution.** A single exercise is a
very short dose, and
[Steenbergen-Hu & Cooper found ITS effects appear only over a full school year](../concepts/vanlehn-2011.md).
**The dissociation is the robust part; the null is dose- and instrument-limited.**

**6. GPT-4-era models.** Both arms. The comparison may not hold for reasoning models.

⭐ **Their own list of why the null might be wrong is worth quoting, because it is honest and
because two of the three are testable by us:** the 90 minutes *"may have been insufficient for
differential cognitive processing to consolidate"*; the assessments *"may have lacked sensitivity
to detect differences that existed but fell below the measurement threshold"*; and — the
interesting one — AI may have let weaker students *"encounter learning opportunities otherwise
inaccessible… students processed more material, albeit less deeply per unit."*

## What we take from this

1. **Scaffolding is worth building anyway** — it kept motivation up, preserved an honest score
   distribution, and was rated better overall — **but do not promise it produces learning gains.**
   The best available evidence says it does not, at least in a single 90-minute session.
2. **Measure performance and learning with different instruments** — this study can see the
   dissociation only because it did — **and make them bigger than six items.**
   → [behavioral evaluation](../evaluation/behavioral-evaluation.md)
3. ⭐ **Measure germane cognitive load.** It is a validated construct, cheap to administer, and it
   is the mechanism. Nobody else in this base measured it. **Use more than two items** — TUM's
   biggest finding is also its thinnest measurement, and improving on that is a real contribution.
4. ⭐ **Steal the ingestion pipeline.** Auto-captioning diagram-only slides, hybrid retrieval with
   a cross-encoder rerank, and citations carrying slide numbers and video timestamps are all
   specified concretely enough to reimplement. → [content generation](../practice/content-generation.md)
5. **Their closing recommendation is our assessment-integrity argument:** we need *"assessment
   designs resilient to environments where performance no longer reliably tracks understanding."*
   → [assessment integrity](../practice/assessment-integrity.md)
6. ⭐ **Re-analyse their data.** The dataset and R code are on Zenodo under CC-BY. A reanalysis
   asking whether learning gain tracks *completion* rather than *condition* would test
   [VanLehn's mechanism](../concepts/vanlehn-2011.md) directly, on somebody else's data, for free.

## Open questions

- [ ] Does knowledge gain in their data correlate with **exercise performance within arm**? If
      completion predicts learning better than condition does, that is a publishable reanalysis
      and it settles the question this node raises above.
- [ ] Would a fourth arm — **scaffolded hints plus a completion requirement** — separate? That is
      the design VanLehn's mechanism and Bloom's mastery threshold both point at, and nobody has
      run it.
- [ ] Does the hint ladder need a bottom-out step? Iris says no; classical ITS says yes; **this
      study cannot distinguish them** because it has no arm with a terminating ladder.

## Connects to

- [Bastani et al. 2025](bastani-2025-harm.md) — the same dissociation, K-12, with a harm result
- [VanLehn 2011 and the meta-analyses](../concepts/vanlehn-2011.md) — the completion mechanism this measures, and the proximal/distal table
- [Productive failure](../concepts/productive-failure.md) — germane load is the struggle
- [Bloom's 2 sigma](../concepts/blooms-two-sigma.md) — the mastery threshold the missing fourth arm would need
- [Assessment integrity](../practice/assessment-integrity.md) — their closing recommendation
- [The deployed RAG + SRL tutor](../systems/rag-tutor-southeast.md) — variance compression, read differently
- [LearnLM](../systems/learnlm.md) — preference and pedagogy diverging, again
- [RAG in education](../concepts/rag-in-education.md) — Iris's ingestion pipeline is the most detailed one we hold
- [Diagram reading](../domain/diagram-reading.md) — auto-captioning diagram-only slides is a cheap partial answer
- [Socratic tutoring](../concepts/socratic-tutoring.md) — the ladder that never bottoms out

## Sources

- [Bassner, Lenk-Ostendorf, Beinstingel, Wasner & Krusche (2026), "Less stress, better scores, same learning: The dissociation of performance and learning in AI-supported programming education," *Computers and Education: Artificial Intelligence* 10, 100537](https://doi.org/10.1016/j.caeai.2025.100537) `[read — full text, 21 pp., 2026-09-03]` · CC-BY gold OA. Local: `course-materials/papers/bassner-2025-tum-dissociation.pdf`
- [Dataset and analysis code, Zenodo 10.5281/zenodo.16905779](https://doi.org/10.5281/zenodo.16905779) `[found]` — ⭐ **not yet downloaded; the reanalysis above needs it**
- Bassner, P., Frankford, E. & Krusche, S. (2024). *"Iris: An AI-driven virtual tutor for computer science education."* ITiCSE 2024. `[found]` — the system paper for the tutor evaluated here
</content>
