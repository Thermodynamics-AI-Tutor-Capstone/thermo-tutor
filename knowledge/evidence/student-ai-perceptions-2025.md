# What engineering students already think about AI (UIC, n = 78)

**Type:** evidence
**One line:** ~90% of chemical engineering students already use AI for coursework, they **do not
trust it** (2.65–2.87 on a 5-point scale), and the students closest to our target population are
the **least calibrated** about that.
**Why we care:** This is the baseline our tutor competes against. We are not introducing AI to
these students — they have been using ChatGPT for two years and have already formed opinions.

> **Verification: `[read]` — full text, 31 pp., 2026-09-01.**

Bilgin, B. (UIC), Chen, C. V. H.-H. (Columbia) & **Velegol, S. B. (The Pennsylvania State
University)** (2025). *"Generative AI in Chemical Engineering Education: Rebuilding
Thermodynamics, Material and Energy Balances and Kinetics Courses with AI and Chemical Engineering
Students' Perception of AI."* **ASEE Annual Conference 2025.**

## ⭐⭐ Read the author list

**Stephanie Butler Velegol is a Teaching Professor of Chemical Engineering at Penn State**, and a
co-author on a paper about rebuilding a **thermodynamics** course with AI. She "pioneered the use
of flipped classes to increase active learning."

**This is the most actionable single fact in this knowledge base.** A faculty member at our own
institution, in an adjacent department, is already publishing on exactly our topic. She is a
plausible **sponsor, IRB path, course-access route, and co-author** — and the ask is a warm one,
because we are offering to build the tutoring layer her paper's students said they needed.
→ [PSU AI landscape](../practice/psu-ai-landscape.md), [IRB](../../admin/irb.md),
[roadmap](../../admin/roadmap.md)

## The survey

**n = 78**, University of Illinois Chicago, end of semester. Two cohorts: **sophomores in
Introduction to Thermodynamics** — our exact population — and seniors in Senior Design I.
~58% male, ~35% female; ~30% Latinx, ~30% Asian, ~30% White, ~7% Black. Nine Likert items plus
three open-ended questions, analysed with t-tests.

### Adoption is already near-universal

| Cohort | Prior academic AI use |
|---|---|
| **Sophomores (Thermodynamics)** | **87.2%** |
| Seniors | **92.3%** |

ChatGPT dominant. Sophomores use it for **concept clarification, MATLAB/VBA help, checking
homework, and generating study guides** — which is, almost line for line, the feature list of the
tutor we are proposing. **Whatever we build is a substitute for something they already have and
like.**

### But trust is low, and that is the opening

Likert means, 1 = strongly disagree to 5 = strongly agree:

| Dimension | Sophomores | Seniors |
|---|---|---|
| Awareness of AI's limitations | **4.36** | **4.54** |
| Can critically evaluate AI outputs | **4.03** | 3.73 |
| AI enhances concept understanding | **4.02** | 3.57 |
| AI improves academic performance | 3.83 | 3.38 |
| ⭐ **AI helps with problem-solving** | **3.76** | **2.65** * |
| Comfort/confidence with AI | 3.70 | 3.81 |
| Scientific soundness of AI output | 3.23 | 3.04 |
| ⚠ **Trust in AI outputs** | **2.87** | **2.65** |

\* statistically significant difference (p < 0.05); academic-performance expectations also differed
significantly. Gender and ethnicity analyses found no substantive differences.

**Trust sits below the midpoint for both groups.** Students use a tool they do not believe.
A grounded, tool-verified tutor is therefore not a technical nicety — **it is the only available
differentiator against the free product they already use.**
→ [grounding and verification](../concepts/grounding-and-verification.md)

### ⚠ The calibration gap, and it runs the wrong way for us

**Seniors rate AI's problem-solving help at 2.65; sophomores at 3.76.** Experience with
engineering makes students trust AI *less* for exactly the task our tutor performs.

Worse: sophomores rate **their own ability to critically evaluate AI output higher than seniors
do** (4.03 vs 3.73), while having less domain knowledge to evaluate with. **The population most
likely to accept a wrong answer is the population taking thermodynamics.** That is our users, and
it raises the cost of every error the tutor makes.
→ [assessment integrity](../practice/assessment-integrity.md),
[Bastani](bastani-2025-harm.md)

## What students say in their own words

They have already located the failure mode our whole architecture addresses:

> *"ChatGPT can barely do math."*

> *"I couldn't use AI on actual assignments as often times **the formulas and values were wrong or
> not complex enough for the question**."*

That is [the property-lookup failure](../domain/llm-thermodynamics-capability.md), described
unprompted by sophomores in a thermodynamics class. **They have diagnosed the problem
[GPThermo](../systems/gpthermo-wpi.md) solves.**

Their adaptation is to retreat to conceptual use: *"this recognition led many students to develop
strategic approaches to AI usage, focusing on conceptual understanding rather than numerical
solutions."* One describes a workflow worth designing for directly:

> *"I would ask if my approach to problem solving is right or wrong. **I always ask for answers to
> questions after solving it by myself first**."*

**That student has independently invented productive failure.** → [productive failure](../concepts/productive-failure.md)

On dependency, unprompted and self-reported:

> *"My ability of doing my hw has decreased and i feel dependancy on chat gpt for studies."*

> *"we might not truly understand the concept of the problem."*

And a request that costs us nothing to honour:

> Students wanted *"clear expectations (as explicit as possible) from schools and professors on AI
> usage"* to avoid unintentional academic misconduct.

## What we should do differently because of this

1. **Do not pitch this as "students get AI help."** They have that. Pitch **verified numbers** and
   **a tutor that makes them work first** — the two things they say ChatGPT fails at.
2. **Measure trust as an outcome.** A 2.87 baseline is a low bar and a legible headline. Nobody in
   [this literature](../../docs/02-bibliography.md) reports a trust delta.
3. **Design the "check my approach" interaction explicitly.** A student described it as their
   ideal workflow, and it is [productive failure](../concepts/productive-failure.md) with the
   struggle already built in — the hardest part of PF, volunteered by the user.
4. **Sophomores are overconfident about spotting AI errors.** Surface uncertainty and provenance
   in the interface rather than assuming the student will catch a bad answer.
5. **Email Velegol.** → [roadmap](../../admin/roadmap.md)

## ⚠ Limits

Single institution for the student survey, one semester, self-report, end-of-semester recall,
**chemical** rather than mechanical engineering, and no link between perception and any
performance measure. The course-redesign half of the paper — three faculty using AI to generate
syllabi, content and assessments — reports no systematic accuracy evaluation, only that
*"challenges such as AI biases and content accuracy remain significant hurdles."* Treat the
attitude data as solid and the course-design claims as anecdote.

## Connects to

- [PSU AI landscape](../practice/psu-ai-landscape.md) — the Velegol lead
- [GPThermo](../systems/gpthermo-wpi.md) — the tool layer students are asking for
- [Bastani](bastani-2025-harm.md) — what happens when unverified help meets an unassisted exam
- [Productive failure](../concepts/productive-failure.md) — the workflow a student described
- [Engagement decay](../concepts/engagement-decay.md) — we compete with a tool they already open
- [Assessment integrity](../practice/assessment-integrity.md)

## Sources

- [Bilgin, Chen & Velegol (2025), "Generative AI in Chemical Engineering Education," *ASEE Annual Conference*](https://peer.asee.org/56640.pdf) `[read — full text, 31 pp., 2026-09-01]` · DOI `10.18260/1-2--56640`
