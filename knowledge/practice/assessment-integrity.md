# Assessment integrity — what a tutor does to grades as a signal

**Status:** `[synthesis]` — drawn from primaries read in full, no dedicated literature yet found.

**One line:** Every deployment that has looked has found the same shape — **assisted work goes up,
unassisted work goes down or stays flat** — which means a tutor silently destroys the validity of
homework as a measure at the same time as it improves the homework.

---

## The measured version

[Bastani et al. 2025](../evidence/bastani-2025-harm.md) is the only study that has cleanly
separated the two. Unguarded GPT-4 in Turkish high-school maths:

| Arm | While assisted | On the unassisted exam |
|---|---|---|
| **GPT Base** | **+48% vs. control** | **−17% vs. control** |

**The +48% and the −17% are the same students on the same material.** The practice score was not
a noisy measure of learning; it was a measure of the tool. And the sign flips.

This is the single most important operational fact in this repository for anyone who plans to use
homework performance as an outcome — including us, in our own evaluation.
→ [evaluation design](../evaluation/README.md)

## The field version

**[PeteChat](../systems/petechat-purdue.md)**, Purdue ECE 20875. TAs reported that heavy GPT
reliance was *"inflating homework scores (north of 95%) while exam performance drops."*
⚠ **Testimony, not measurement** — no gradebook analysis was run. But it is Bastani's pattern
described independently by people watching it happen in an engineering course.

And in the same course's pre-guardrail corpus, **boundary testing / system probing ran at 22% of
student messages in the homework context** (13.4% overall). Roughly one homework message in five
was an attempt to get around the tutor's limits, and the system **sometimes complied**.

## What students do when observed

**Amoozadeh et al. (2024)**, *"Student-AI Interaction: A Case Study of CS1 Students"*
(arXiv:2407.00305, Houston / CMU / Abilene Christian / IIT) watched **15 gender-balanced CS1
students** solve programming tasks with ChatGPT — think-aloud, screen video, and full conversation
logs, open-coded by two authors.

- ⚠ **In about a third of cases the student pasted the full task description into ChatGPT
  "without making any effort on their own."** Not after getting stuck — as the opening move.
- ⚠ **"Few students verified their solutions."**
- Students who submitted whole task descriptions **correlated with lower self-efficacy**,
  matching prior work that lower-self-efficacy students lean hardest on the tool.
- Mixed on the outcome: **overall self-efficacy rose** after the session.

⚠ **n = 15, self-selected, one intro course, qualitative.** Not a rate to quote as a population
estimate. But it is direct observation rather than log inference, and "delegate immediately,
verify nothing" is the behaviour our design has to assume exists.

The design reading is the same one [PeteChat](../systems/petechat-purdue.md) arrived at: the
tutor has to notice *"this is the assignment text, pasted verbatim"* as a distinct event, because
it is the most common thing a struggling student does first.

## ⚠ The guardrail does not hold, and upgrading the model makes it worse

**[CS50's duck](../systems/cs50-duck.md)** is the most-resourced AI tutor deployment in higher
education, and it is explicitly instructed **not** to produce direct code solutions. Across
**10 million messages**:

| Model | Message-level code blocks | Conversation-level |
|---|---|---|
| GPT-4 | 20% | 44% |
| **GPT-4o** | **25%** | **56%** |
| *Overall* | *22% (2.1M responses)* | *48% (635k of 1.3M conversations)* |

**Nearly half of all conversations contained generated code, against an explicit instruction not
to generate any.** CS50 named the mechanism **instruction dilution**, and note the direction of
the change: **the newer, better model complied less.**

**Two consequences we should treat as design constraints:**

1. **A prompt is not a guardrail.** If Harvard cannot hold this line with a prompt at CS50's
   level of investment, neither can we. Refusal has to be enforced outside the model — by
   detecting that a query matches an active assessment item and routing it, not by asking nicely.
   → [why pedagogy in the system prompt fails](../concepts/guardrails.md)
2. **Guardrails silently decay on model upgrade.** Nothing in the deployment changed except the
   model, and compliance dropped. **Any integrity behaviour we rely on needs a regression test
   that runs on every model change** — which is exactly what CS50 built after finding this.
   → [continuous evaluation](../evaluation/README.md)

## What the deployments actually do about it

- **Assessment-aware mode** ([PeteChat](../systems/petechat-purdue.md)): detect that a query
  resembles an active assignment item, then refuse complete solutions, respond with hints aligned
  to the instructor's method, and show an integrity banner. The detection is the load-bearing
  part — it needs the assignment list, which means **LMS integration is an integrity requirement,
  not just a convenience.** → [LMS integration](lms-integration.md)
- **Debugging as error-message explanation, never as a code fix** — reframes the highest-demand
  use case into one that cannot be copy-pasted into a submission.
- **Rubric-grounded regrade helper**: retrieve the rubric, explain the deductions, make the
  student articulate why they think it is wrong, and only then offer escalation to a human TA.

## The instructional response: reward the journey, not the answer

**Melanie Cooper (2026)**, *"A Preliminary Set of Principles to Support Learning in the Context of
Generative AI,"* **J. Chem. Educ.** 103, 36–42 (read in full 2026-09-01) — a perspective from one
of chemistry education's most cited researchers, and the clearest statement of the instructional
side of this problem.

Her premise is the mechanism this node keeps running into: *"**learning requires effort and
engagement which can easily be bypassed using AI**."*

**Four principles:**

1. **Design AI systems to support self-regulated learning** — the same commitment
   [the deployed RAG + SRL tutor](../systems/rag-tutor-southeast.md) made.
2. ⭐ **Build a course structure and culture that rewards the journey to knowledge rather than
   the correct answer to relatively trivial tasks.**
3. **Use AI's affordances to extend what students know and can do**, rather than to replace what
   they should be doing.
4. **Develop clear and equitable policies** for AI use — which
   [students asked for in their own words](../evidence/student-ai-perceptions-2025.md), and which
   [suppressed use at USAFA when absent](../evidence/student-ai-perceptions-2025.md).

**Principle 2 is the one that changes what we build.** Her concrete proposal is to **shift grading
weight to formative tasks that require initial student input**, rather than relying on
*"summative assessments and randomized homework systems (that can be answered by AI)."*

**That is an assessment-design answer to the integrity problem, and it is better than a
detection-based one.** If the graded artefact is the student's *reasoning trace* — their stated
assumptions, their chosen control volume, their first wrong attempt and their correction — then
an AI that hands over the final number has produced nothing gradeable. **Our tutor already
generates exactly that trace** if we log it.
→ [behavioral evaluation](../evaluation/behavioral-evaluation.md)

⚠ **Her sharpest claim, and it aims squarely at our course:** traditional courses *"where
emphasizing facts and algorithmic problem solving are emphasized) will become obsolete as these
tasks are easily (and perhaps better) carried out by AI bots."* **Engineering thermodynamics as
usually taught — look up the property, apply the balance, get the number — is precisely that
description.** It is uncomfortable, it is arguably correct, and it is a stronger motivation for
this project than anything in our current framing: **the tutor is not a convenience, it is a
response to the part of the course that automation has already devalued.**

## What this means for our project

1. **Never report a homework-based outcome as evidence the tutor worked.** State this in the
   study design before we collect anything, or a reviewer will state it for us.
2. **Our primary outcome must be unassisted and proctored** — which points at
   [STPFaSL](../evaluation/concept-inventories.md) administered without tool access.
3. **We can run the study PeteChat could not.** The homework-inflation-versus-exam-drop pattern is
   asserted from TA impressions in engineering and measured only in Turkish high-school maths.
   Pairing gradebook homework scores against proctored exam scores in a thermodynamics course, with
   tutor usage logs as the moderator, is a genuinely novel and cheap contribution.
4. **Budget for integrity regression tests** from the first prototype, and re-run them on every
   model upgrade.

## Open questions

- [ ] Is there any published study of AI-tutor availability and *grade distribution* in an
      engineering course? Nothing found so far — this may be the gap it looks like.
- [ ] What does PSU's academic-integrity policy actually say about a course-sponsored AI tutor?
      → [PSU AI landscape](psu-ai-landscape.md)
- [ ] Does assessment-aware refusal drive students to ChatGPT instead, making the measured
      integrity gain illusory? Nobody has measured substitution.

## Connects to

- [Bastani et al. 2025](../evidence/bastani-2025-harm.md) — the measurement
- [PeteChat](../systems/petechat-purdue.md) — the field report and the design response
- [CS50 duck](../systems/cs50-duck.md) — instruction dilution at 10M-message scale
- [Guardrails](../concepts/guardrails.md) — why the prompt is the wrong layer
- [LMS integration](lms-integration.md) — assessment awareness needs the assignment list
- [Disclosure and ethics](disclosure-and-ethics.md)

## Sources

- [Cooper, M. M. (2026), "A Preliminary Set of Principles to Support Learning in the Context of Generative AI," *J. Chem. Educ.* 103, 36–42](https://pubs.acs.org/doi/pdf/10.1021/acs.jchemed.5c01413) `[read — full text, 7 pp., 2026-09-01]` — CC-BY

Synthesised from primaries read in full and cited in the linked nodes, plus:

- [Amoozadeh, Nam, Prol, Alfageeh, Prather, Hilton, Srinivasa Ragavan & Alipour (2024), "Student-AI Interaction: A Case Study of CS1 Students," arXiv:2407.00305](https://arxiv.org/pdf/2407.00305) `[read — full text, 15 pp., 2026-09-01]` The gap flagged in
[the bibliography](../../docs/02-bibliography.md) — *"prior work on AI tutors and academic
integrity — what happens to homework grades as a signal when a tutor exists"* — **remains
genuinely unfilled.** If someone finds a dedicated literature, it belongs here.
