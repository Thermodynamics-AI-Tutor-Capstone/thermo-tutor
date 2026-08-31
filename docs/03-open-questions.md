# Open Questions

The list that drives this phase. Each question has a method attached, because a question
with no method is a conversation, not research.

Owner column is blank until the team assigns. Keep it current — this file is the
project's actual to-do list during discovery.

---

## A. What students actually do

**A1. What is a thermo student's real workflow at 11pm the night before a problem set is
due?**
Not what they say they should do. What they do. Which tabs are open, in what order, and
what triggers the switch from "trying" to "getting the answer."
*Method:* semi-structured interviews, retrospective walkthrough of the most recent
assignment. Possibly a diary study for a subset. *Owner:* ___

**A2. Why do students choose Chegg over ChatGPT, or vice versa?**
Our assumption is convenience and confidence in correctness. Probably incomplete.
*Method:* interviews. Direct question, then probe the gap between stated and revealed
preference. *Owner:* ___

**A3. What do students believe an AI tutor is for?**
If the mental model is "answer machine," a Socratic tutor reads as a broken answer
machine. Reframing may be a bigger lever than any feature.
*Method:* interviews; ask before demoing anything. *Owner:* ___

**A4. Where does a thermo student actually get stuck?**
Candidate levels: reading the problem, choosing the system boundary, identifying
licensed assumptions, finding the right property data, executing algebra, sanity-checking
the result. These need very different help.
*Method:* think-aloud protocol on a real problem. Higher effort, much higher signal than
interviews. *Owner:* ___

**A5. Would students voluntarily return to a tutor after week two?**
The Khanmigo question. 96% tried it; the median student used it in 17% of sessions.
*Method:* can only be answered by a live pilot. Until then, ask students directly what
would make them come back — and discount the answer heavily. *Owner:* ___

---

## B. What existing tools actually do

**B1. How does each incumbent behave when a student defects?**
The scripted test: attempt a problem, then say "just tell me the answer." Record what
each tool does at turn 1, 3, and 5 of escalating pressure.
*Method:* competitive teardown, identical script across tools. *Owner:* ___

**B2. How often is each tool simply wrong about thermodynamics?**
Especially: property values, entropy, unstated-assumption problems.
*Method:* fixed problem set with known answers, run against every tool. See B4.
*Owner:* ___

**B3. What do Mastering Engineering / McGraw Hill Connect / WileyPLUS already do well?**
These are the real incumbents in a thermo course and have a decade of adaptive-learning
telemetry. We should not reinvent their hint ladders in ignorance.
*Method:* hands-on, plus published documentation. Ask the instructor sponsor for access.
*Owner:* ___

**B4. Can we build a thermodynamics *pedagogy* benchmark?**

> **CORRECTED 2026-08-29.** This question originally read "can we build a thermodynamics
> tutoring benchmark," and named it the project's most likely publishable contribution.
> The correctness half **already exists and is better than what we would have built**:
> [ThermoQA](../knowledge/domain/thermoqa.md) (293 open-ended problems, three tiers,
> programmatic CoolProp ground truth, six frontier models × three runs) and
> [UTQA](../knowledge/domain/utqa.md) (50 items incl. diagrams, 19 models). Use them as
> instruments; do not rebuild them.

What does **not** exist is a thermodynamics analogue of
[MathTutorBench](../knowledge/evaluation/mathtutorbench.md) — measuring *teaching quality*
rather than correctness. That gap is real and is now our clearest novel contribution.

*Method:* collect real student errors; cut conversations at the moment of error
(MRBench-style); have instructors and experienced TAs author the expert next turn; score
candidate tutor responses by expert pairwise preference (the
[CS50 TF method](../knowledge/systems/cs50-duck.md)).
*Note:* the judges are instructors and TAs, not students — **a much lighter IRB path**, so
this can run while the student protocol is still in review. *Owner:* ___

---

## C. Design questions we can't answer yet

**C1. Is "what do I do next" a student failure or a legitimate request?**
The discourse taxonomy treats it as evidence that Socratic framing failed. Alternative
reading: strategic-level help is a real need that pure question-asking wrongly refuses.
*Method:* think-alouds (A4) plus literature on productive failure. *Owner:* ___

**C2. What is the right grain for a "concept" in thermodynamics?**
Too coarse (`entropy`) and mastery tracking is meaningless. Too fine (`interpolating
between two superheat table rows`) and we need thousands of items and can never get
enough data per concept. See `research/domain/skill-graph-draft.md`.
*Method:* domain analysis + instructor review + sanity check against how many
interactions a semester actually produces. *Owner:* ___

**C3. What would count as evidence that we succeeded?**
Options: normalized gain on the **TTCI-T** (⚠ *not* the TCI — never finished, developers
discourage use → [concept inventories](../knowledge/evaluation/concept-inventories.md)),
course grade, time-to-solution, voluntary return rate,
self-reported confidence, benchmark score. These can move in opposite directions.
**Decide before we collect anything**, or we'll be accused of picking the metric that
won. *Owner:* ___

**C4. What's the honest comparison condition?**
Beating "no help" is trivial. Beating ChatGPT is the interesting claim and a hard one —
students have ChatGPT for free and it's very good. Kestin beat active learning, which is
why that paper matters.
*Method:* team decision, with the instructor sponsor. *Owner:* ___

**C5. Does an AI tutor change what homework grades mean?**
If the tutor helps everyone, homework stops discriminating and the course's assessment
model shifts under the instructor's feet. This is the instructor's problem and they will
raise it. We should raise it first.
*Method:* conversation with the instructor sponsor. *Owner:* ___

---

## D. Feasibility and access

**D1. What Canvas access can we actually get?** See `admin/canvas-access.md`.

**D2. What does PSU IRB require, and how long does it take?** See `admin/irb.md`.
**Blocking for all of section A.**

**D3. Can we get the TTCI-T?** PhysPort gates instruments behind educator verification.
⚠ Superseded target: the TCI is unusable — see
[concept inventories](../knowledge/evaluation/concept-inventories.md).
Instructor sponsor is the path. *Owner:* ___

**D4. ~~What is the actual budget for API calls during a pilot?~~ ANSWERED.**
~$2.63–4.79 per student per semester; a 100-student pilot is $300–500. Cost is not a
constraint. → [cost economics](../knowledge/practice/cost-economics.md)

**D6. Does [PSU AI Studio](../knowledge/practice/psu-ai-landscape.md) expose an API?**
**The highest-leverage unanswered question in this document.** If yes, the compliance path
largely dissolves and we build on an already-approved channel. If it's a chat UI only, we're
back to vendor agreements and IRB review of data leaving the institution. *Owner:* ___

**D5. Who owns what we produce?**
Penn State IP policy for undergraduate capstone work. Matters if any of this becomes a
paper or a product. *Owner:* ___

---

## Questions we have already answered

Moved here so we stop relitigating them.

- **Should the LLM track student mastery?** No — specialized KT models are more accurate,
  faster, cheaper, and reproducible. (Key finding #3)
- **Should property values come from the model?** No — tool calls only. (Key finding #2)
- **Is "be Socratic" in the system prompt sufficient?** No. (Key finding #1)
- **Is there a validated pre/post instrument for thermo?** Yes, TCI/TTCI-T, developed at
  Penn State. (Key finding #5)
- **What will API costs be? (was D4)** ~$2.63–4.79 per student per semester; a 100-student
  pilot is $300–500. Not a design constraint.
  → [cost economics](../knowledge/practice/cost-economics.md)
- **Does PSU have an enterprise LLM agreement? (was in D2/admin)** Yes — **AI Studio**
  provides Claude, ChatGPT, and Gemini to all students, with published terms stating personal
  information is not used to train the models.
  → [PSU AI landscape](../knowledge/practice/psu-ai-landscape.md).
  **Still open: does it expose an API?**
- **Can we build a thermo correctness benchmark?** Don't — ThermoQA and UTQA exist. See B4.
