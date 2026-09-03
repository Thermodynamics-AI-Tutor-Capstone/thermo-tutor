# Hybrid human-AI tutoring — the other inversion, and a staffing ratio

**Type:** system / deployment model
**One line:** CMU and Stanford put **remote human tutors behind an off-the-shelf commercial ITS**
and then asked the only question nobody else asks — *which students should the humans interrupt?*
**Why we care:** It is the mirror image of [Tutor CoPilot](tutor-copilot.md), it reports the
**proactive-vs-reactive** contrast our whole knowledge base has been circling, and it is the only
place in this base with **a concrete tutor-to-student ratio attached to an outcome.**

> **Verification: `[read — full text, 13 pp., 2026-09-03]`.** Local copy:
> `course-materials/papers/edm-2026-hybrid-human-ai-tutoring.pdf` (+ `.txt`). CC BY-NC-ND.

Gurung, A., Gao, G., Guo, B., Houk, A., Gatz, E., Thomas, D. R., Gupta, S., Branstetter, L.,
**Brunskill, E.**, **Aleven, V.**, **Koedinger, K. R.** & Gutterman, J. (2026). *"Improving Hybrid
Human-AI Tutoring by Differentiating Human Tutor Roles Based on Student Needs."* **EDM 2026**,
Seoul, pp. 130–142. [DOI 10.5281/zenodo.21039782](https://doi.org/10.5281/zenodo.21039782).
Carnegie Mellon + Stanford. Analysis code at `tiny.cc/EDM26`.

**Note the author list.** Koedinger and Aleven built [Cognitive Tutor](cognitive-tutor.md) and
[are the source of the completion mechanism VanLehn credits](../concepts/vanlehn-2011.md);
Brunskill is the RL-for-education lead. This is the classical-ITS establishment working on
human-AI hybrids, not an LLM group.

---

## ⭐⭐ The inversion, and why it is the opposite of Tutor CoPilot

| | Who gets the AI | Who gets the human | Result |
|---|---|---|---|
| [**Tutor CoPilot**](tutor-copilot.md) | **the tutor**, as a suggestion engine | the student, live | +4 p.p. exit tickets; ⚠ **null on MAP** |
| **This** | **the student**, as [IXL](aleks.md)-style adaptive practice | **the tutor supervises several students at once** | +25% time on task, +36% skill proficiency, **+61% MAP growth** |

**Same hybrid premise, opposite plumbing, and the distal measure is the same instrument — NWEA
MAP — with opposite signs.** That contrast is the reason this node exists.

⚠ **They are not comparable as evidence.** Tutor CoPilot is a preregistered RCT with a control
group and reports a null on MAP. **This study has no control group at all** — see ⚠⚠ below. Do
not read "hybrid tutoring moves MAP" out of the pair.

---

## The design

**635 students, grades 5–8, one middle school in a Mid-Atlantic US state, 2024–25.** Of ~1,000
eligible, 635 opted in under IRB consent. **AI tutor: [IXL](aleks.md)** — a commercial adaptive
math platform whose own effect against business-as-usual is **0.08 SD** (Evidence for ESSA Tier 1;
state-level replications 0.10–0.13 SD).

**Human tutors:** undergraduate and graduate students from a US university, trained, working
**remotely over Zoom** twice a week during school hours. After setup, **~30 minutes of practice
per session.** Students sat in individual breakout rooms doing IXL; tutors visited.

⭐⭐ **The allocation policy, which is the paper's actual contribution:**

| Group | Assignment rule | Tutor ratio | Time per student | Tutor behaviour |
|---|---|---|---|---|
| **Proactive** | **below** within-grade median on prior-year state test | **1 : 4** | ~7.5 min | tutor **initiates** — visits breakout rooms, checks progress unasked |
| **Reactive** | **at or above** the median | **1 : 10** | ~1–3 min | **on demand only** — student raises hand or uses Zoom chat |

> ⭐ *"'Proactive' and 'reactive' refer to how tutors deliver support, not how students seek it."*

**Identification: difference-in-discontinuities (DiDC)** — a regression discontinuity at the
median cutoff, differenced against a pre-period. **Fall = AI-only for everybody. Spring = the
differentiated human-AI policy.** Fall IXL data and winter MAP are the baseline; spring IXL and
spring MAP are the outcome. Analysis restricted to the **Imbens–Kalyanaraman bandwidth** around
the cutoff (**n = 287, 52% of the sample**).

Validity work is genuinely careful: **McCrary manipulation tests** found no sorting at the cutoff
in any grade; covariate balance checked on ethnicity, gender and socioeconomic status; continuity
checked on winter MAP and fall IXL; robustness via alternative bandwidths, CCT bias-corrected
estimates, and donut checks.

---

## Results

**Human-AI vs. the AI-only baseline** (IK bandwidth):

| Outcome | Effect | p |
|---|---|---|
| Time on task | **+25%** (+1.32 hours) | < .001 |
| IXL skill proficiency | **+36%** (+6.10 skills) | < .001 |
| **Relative MAP growth** | **+61%** | **.003** |
| ⚠ Relative MAP growth, **full sample** | **+26%** | **.086 — not significant** |

Students under human-AI tutoring hit **≈ 2× NWEA's national expected growth norm** for their
grade. *(NWEA's 2025 norms, from 13.8 million students: 4 RIT points winter→spring for grades 5–6,
3 points for grades 7–8. "Relative growth" is observed ÷ expected.)*

**Proactive vs. reactive:**

| Comparison | Estimate | p |
|---|---|---|
| Proactive × human-AI interaction, IK bandwidth | **+0.75** | **.065** *(marginal)* |
| Proactive × human-AI interaction, full sample | +0.78 | .010 |
| **At the cutoff:** reactive group's growth | **1.74× expected** | .007 |
| **At the cutoff:** proactive minus reactive | −0.33 | **.579 — no difference** |
| Interaction with prior performance (the gap-narrowing claim) | −1.61 | ⚠ **.247 — not significant** |
| Time on task, proactive vs. reactive | −0.11 | n.s. |
| ⚠ Skill proficiency, proactive vs. reactive | **−1.52** (IK) / **−2.56** (full, p < .01) | reactive **higher** |

**Averaged over the whole range, proactive students grew 2.18× expected against reactive students'
1.70×. At the cutoff itself the two are identical.** The authors read that as evidence the median
is a well-chosen threshold — both groups benefit, and the proactive advantage comes from students
*far below* it.

---

## ⚠⚠ What is wrong with this, and it matters

**1. There is no control group.** The comparison is (a) these same students in the fall, and
(b) NWEA's national growth norms. The authors say so plainly:

> *"Our reliance on national growth norms as a reference point, rather than a matched control
> group, limits causal inference."*

**Everything that differs between a school's fall and its spring is confounded with the
intervention** — teacher familiarity, curriculum sequence, test-taking practice, the shorter
winter→spring interval. Normalising by grade-level growth norms handles some of it and not the
kind that is local to this school. **"2× expected growth" is a description of one cohort, not an
effect size.**

**2. The headline is significant only in the 52% subsample.** +61% at p = .003 inside the IK
bandwidth; **+26% at p = .086 in the full sample.** The authors justify prioritising the local
estimate — parallel trends are more plausible among locally comparable students — and that is a
defensible choice. **It is still the case that the number in the abstract does not survive on the
whole sample.**

**3. ⚠⚠ The gap-narrowing claim rests on an interaction at p = .247.** The paper is candid — *"the
interaction… was also not statistically significant (−1.61, p = .247); however, the magnitude of
this estimate suggests a meaningful pattern"* — and then builds the conclusion, the abstract and
the title's promise on it. **Interpreting the magnitude of a null interaction is exactly the move
this knowledge base exists to catch.** The gap-narrowing result should be filed as a hypothesis.

**4. ⭐ On the in-platform proficiency measure the gap *widened*.** *"The proficiency gap widened
by 3.69 skills (14.79%), with the reactive group demonstrating greater proficiency than their
proactive peers."* So the same intervention **narrows the gap on the distal test (marginally,
n.s. at the cutoff) and widens it on the proximal one (significantly, in the full sample).**
That is the [proximal/distal law](../concepts/vanlehn-2011.md) running *backwards*, and neither
the paper nor we have an explanation for it. Worth sitting with.

**5. Nobody recorded what the tutors did.** *"The absence of Zoom interaction data (actual
student–tutor interactions) represents a missed opportunity for deeper analysis, especially for
understanding which elements of proactive tutoring were effective."* **The active ingredient is
unobserved.** Compare [Tutor CoPilot classifying 550,000 messages](tutor-copilot.md).

**6. No consistent student–tutor pairing.** Students were assigned to breakout rooms at random
each session; tutors covered a fixed set of *rooms*, not a fixed set of *students*. The authors
flag this as a design flaw to fix, citing evidence that relational continuity matters.

**7. Self-selected sample.** 635 of ~1,000 eligible consented.

**8. The effect is a bundle, and they say so.** *"The estimates likely reflect the benefits of the
implemented policy as a bundle, rather than the isolated effect of the assignment policy itself…
the combined effects of student needs, teacher context, tutor behavior, AI tutor use, and the
proactive–reactive assignment rule."*

---

## ⚠⭐ The skeptical reading they do not offer

The authors present agreement with **Borchers et al. (2025)** as converging evidence:

| Intervention, same platform, same research group | Time on task | Skill proficiency |
|---|---|---|
| **This study** — differentiated proactive/reactive human tutoring | **+25%** | **+36%** |
| **Borchers et al. 2025** — rewards-based **goal setting**, no differentiation | **+25%** | **+38%** |

**Two completely different interventions produced the same two numbers.** The authors read
convergence. The other reading is that **+25% time and ~+37% skills is what happens to IXL
metrics when anything at all changes about how the sessions are run** — a ceiling in the platform
measure rather than a treatment effect. ⚠ **Neither reading is established, and the coincidence
should be stated whenever the +25/+36 is quoted.**
→ [behavioral evaluation](../evaluation/behavioral-evaluation.md)

---

## ⭐⭐ What this is genuinely good for

**1. It is the first study in this base to *test* proactivity rather than lament its absence.**

Our base has been accumulating the same observation from four directions:

| Source | Finding |
|---|---|
| [CycleTalk](cyclepad-cycletalk.md) | help requested on **14%** of actions; firing dialogue on *success* beat firing on *hint request* |
| [PeteChat](petechat-purdue.md) | hint utilisation **0.0%** across 284 messages |
| [Khanmigo](../evidence/khanmigo-engagement-2026.md) | median student engaged the AI in **17%** of sessions where they erred |
| [KAIST](../evidence/kaist-vta-2025.md) | **50% of 477 students never used it once** |
| **This study** | proactive check-ins for below-median students; **+0.75 relative growth over reactive, p = .065** |

**Five lines, one conclusion: waiting to be asked is a design failure.** ⚠ And this is the only
one where proactivity was the manipulation — at marginal significance, in K-8 maths, with a human
doing the interrupting.

**2. ⭐ A staffing ratio attached to an outcome — the only one we have.** **1 tutor : 4 students
proactively for the bottom half; 1 : 10 reactively for the top half.** That is a concrete,
quotable allocation policy, and it is the kind of thing a department asks for before it will fund
anything. → [cost economics](../practice/cost-economics.md),
[institutional landscape](../practice/institutional-landscape.md)

**3. ⭐ "Readily available performance data can inform resource allocation decisions."** The
assignment rule is a **within-grade median split on last year's state test** — no student model,
no knowledge tracing, no LLM. **The cheapest possible differentiation policy, and it is the
intervention.** → [knowledge tracing](../concepts/knowledge-tracing.md), which this bypasses
entirely.

**4. It reframes what the AI is for.** In this design the AI tutor is *the practice environment*
and the human is *the attention allocator*. The AI's own effect (IXL, 0.08 SD) is small; the human
layer on top of it is where the movement is. **If that is the shape of the win, our project's
question changes from "how good is our tutor" to "what does our tutor let a TA do that they could
not do before."** → [Tutor CoPilot](tutor-copilot.md), [faculty adoption](../practice/faculty-adoption.md)

---

## ⭐ The literature review is worth more than most of our nodes

These are the numbers the paper assembles, and several are new to us. ⚠ *All secondhand — we hold
none of these primaries.*

| Source | Finding |
|---|---|
| Nickow et al., meta-analysis | Human tutoring **0.36 SD** overall; **0.59 SD** by certified teachers; **0.21 SD** by non-professionals |
| Guryan et al. | High-dosage in-person human tutoring, year-long RCT: **0.26 SD** on state tests |
| ⭐ Bhatt et al. | **4:1 in-person human-AI, alternating days: 0.23 SD** — statistically level with full human tutoring at **30% lower cost** |
| ⚠ Ready et al. | **Virtual** tutoring **0.05 SD** overall — but **0.26 SD** among students who met the recommended dose. **High variance in AI tutor use, "likely due to reduced accountability and disengagement"** |
| Gurung et al. (this group, prior) | Human-AI raised in-platform progress by **0.36 grade levels** — **but no significant aggregate state-test effect.** Students **1 SD below the mean gained +0.15 SD** (p < .001) |
| Chine et al. | Propensity-matched: **~2× learning gains** from in-person human-AI tutoring |
| Steenbergen-Hu & Cooper | ⭐ **Automated systems were *less* effective for lower-performing students** — the premise this whole policy is built on |
| Holstein et al. | Directing **teacher** attention toward struggling students raised gains **for the whole class** |

⭐⭐ **Ready et al. is the one to internalise.** *Virtual* tutoring averaged 0.05 SD and reached
0.26 SD among students who actually showed up — **a fivefold difference driven entirely by dose,
in the delivery mode our project would use.** Combined with
[Steenbergen-Hu & Cooper's short-duration null](../concepts/vanlehn-2011.md) and
[Khanmigo's engagement collapse](../evidence/khanmigo-engagement-2026.md), **dose is the variable, and remote
delivery is where it leaks.**

⚠ **And note the direction of the earlier Gurung result:** in-platform progress moved, state tests
did not, *except* for the bottom of the distribution. This paper's positive MAP result is the
same group's next attempt at that outcome — with the control group removed.

---

## Open questions

- [ ] **Does proactive > reactive survive a real control group?** The authors want an RCT of the
      whole differentiated policy against business-as-usual, and note the ethical objection to
      randomising within it. That is the study to watch for.
- [ ] ⭐ **Can the "proactive check-in" be automated?** Every ingredient here is a human deciding
      *when to interrupt whom*. That is a scheduling policy over engagement telemetry, and it is
      the part of this design an LLM could plausibly do — or at least queue for a TA.
      → [agent architecture](../practice/agent-architecture.md)
- [ ] **What is the university analogue of a within-grade median split?** Prior-course GPA?
      A diagnostic? Our own [concept inventory](../evaluation/concept-inventories.md) pre-test?
      **The allocation rule has to exist before the allocation policy can.**
- [ ] **Why did the proficiency gap widen while the MAP gap (maybe) narrowed?** Nobody addresses
      it and it is the most interesting anomaly in the paper.
- [ ] Borchers et al. (2025), *"Engagement and learning benefits of goal setting with rewards in
      human-AI tutoring,"* AIED 2025 — **needed to judge whether the +25%/+38% coincidence is
      convergence or a ceiling.** Not held.
- [ ] Chine et al., *"Educational Equity Through Combined Human-AI Personalization"* — the ~2×
      in-person result this one replicates remotely. Not held.

## Connects to

- [Tutor CoPilot](tutor-copilot.md) — the same hybrid premise wired the other way round
- [Cognitive Tutor](cognitive-tutor.md) — Koedinger and Aleven's own lineage
- [ALEKS](aleks.md) — the commercial adaptive-practice tier IXL belongs to
- [The ITS meta-analyses](../concepts/vanlehn-2011.md) — Steenbergen-Hu & Cooper's low-achiever finding is this policy's premise
- [Khanmigo](../evidence/khanmigo-engagement-2026.md), [PeteChat](petechat-purdue.md), [CycleTalk](cyclepad-cycletalk.md) — the engagement problem this attacks with humans
- [Engagement decay](../concepts/engagement-decay.md) — dose is the variable
- [Cost economics](../practice/cost-economics.md) — 1:4 and 1:10 are the numbers to cost out
- [Faculty adoption](../practice/faculty-adoption.md) — this design needs TAs, not just software

## Sources

- [Gurung, Gao, Guo, Houk, Gatz, Thomas, Gupta, Branstetter, Brunskill, Aleven, Koedinger & Gutterman (2026), "Improving Hybrid Human-AI Tutoring by Differentiating Human Tutor Roles Based on Student Needs," *EDM 2026*, pp. 130–142](https://doi.org/10.5281/zenodo.21039782) `[read — full text, 13 pp., 2026-09-03]` · CC BY-NC-ND. Local: `course-materials/papers/edm-2026-hybrid-human-ai-tutoring.pdf`
- Analysis code: `tiny.cc/EDM26` `[found]` — anonymised GitHub repo; holds the sensitivity, CCT and donut robustness checks not shown in the paper
- Borchers, Houk, Aleven & Koedinger (2025), "Engagement and learning benefits of goal setting with rewards in human-AI tutoring," *AIED 2025*, pp. 46–59. `[found]`
- Chine, Brentley, Thomas-Browne, Richey, Gul, Carvalho, Branstetter & Koedinger, "Educational Equity Through Combined Human-AI Personalization: A Propensity Matching Evaluation," *AIED*. `[found]`
</content>
