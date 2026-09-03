# Disclosure and Ethics

**Type:** practice
**One line:** Whether students should be told they're talking to an AI, what happens to their
conversations, and who is responsible when the tutor is confidently wrong.
**Why we care:** Our tutor will be wrong about R-134a roughly half the time. Students need to
know that, and we need to have decided what we owe them before we deploy.

## The disclosure question

[Jill Watson](../systems/jill-watson.md) was deployed in spring 2016 **without students
knowing**. The reveal at the end of term made it famous. Students were reportedly delighted —
and the field has never really settled whether that was acceptable.

For us it's moot in one direction: our tutor will be obviously an AI. But the harder version
persists.

**What students actually need disclosed is not "this is an AI" — it's "here is where this AI
is unreliable."**

That's a much more demanding standard, and the
[capability data](../domain/llm-thermodynamics-capability.md) makes it concrete:

- ~44–63% accuracy on R-134a problems
- 45–90% in supercritical regions
- ~32% on diagram interpretation
- A near-certain unwarranted reversibility assumption on ambiguous adiabatic problems

A student who doesn't know this treats every confident answer as equally reliable. **A student
who cannot yet distinguish right from wrong in thermodynamics is definitionally unable to
catch these errors** — that's why they're using a tutor.

**Design implication:** region-aware confidence signaling isn't a nicety, it's the honest
minimum. The tutor should behave differently — hedge, show work, escalate to a human — where
we know it's unreliable. → [grounding and verification](../concepts/grounding-and-verification.md)

## What we owe students on data

Beyond the [IRB requirements](../../admin/irb.md):

- **What is logged.** Every turn, every attempt, every hint. Students should know.
- **Who can see it.** Especially: can the instructor see individual conversations? The
  [interview protocol](../../research/student-interviews/protocol-draft.md) asks students
  this (Q16) precisely because the answer affects whether they'll be honest with the tutor.
  A tutor students perform for is not a tutor.
- **Whether it affects grades.** If the answer is "no," say so loudly and repeatedly.
- **What leaves the institution.** [PSU AI Studio](psu-ai-landscape.md) states personal
  information is not used to train the underlying models. If we build outside AI Studio, we
  owe students the equivalent statement — and it has to be true.

## ⚠ The argument against personalisation itself, from an unrelated field

*This one comes from outside education and is included because nothing inside education makes
it. Treat it as a prompt for our own thinking, not as evidence.*

A 2025 IEEE RO-MAN review of **personalisation in human-robot collaboration for manufacturing**
raises an objection to adaptive systems that this knowledge base has no version of:

> *"By transferring the burden of considering individual needs from managers to technology,
> employees may lose their individuality… employees have limited opportunity to work according to
> their subjective experience **as the system has dictated their ability**, and it is assumed this
> gives a fair assessment of their current capacity."*

**Swap "employees" for "students" and it is a direct objection to a
[student model](../concepts/knowledge-tracing.md).** A tutor that estimates mastery per knowledge
component and routes accordingly has *decided who the student is*, on evidence the student cannot
see and did not consent to being read that way. The system's estimate becomes the student's
allowed range.

⚠ **The authors label their own argument speculative** — *"such arguments may be speculative"* —
and it is untested in either field. But it sharpens two things we should decide before a pilot:

- **Can a student see and contest their own model?** Our data-transparency list above says *what*
  is logged; it does not say whether the student can read the *inference* drawn from it.
- **Does the tutor ever tell a student what it thinks they cannot do?** [The proactive/reactive
  allocation policy](../systems/hybrid-human-ai-tutoring.md) splits a cohort on a prior test
  score. That is defensible as staffing and corrosive as a label, and the difference is entirely
  in whether the student is told.

⭐ *One small parallel worth noting from the same review, because it lands on the same question
from the other side:* **users with prior experience wanted to tune the system's parameters
themselves, while novices preferred the system to choose for them.** That is the same split the
[proactive/reactive study](../systems/hybrid-human-ai-tutoring.md) staffed for, arrived at in
industrial robotics. Two unrelated literatures, one shape: **novices want the system to decide;
experienced users want the control.**

## The responsibility question

When the tutor confidently teaches a student that an adiabatic process is isentropic, and the
student writes that on an exam — whose fault is that?

There's no settled answer in this literature, and we should have a position before a pilot
rather than after an incident. Reasonable components of one:

- Real verification, not just a disclaimer → [grounding and verification](../concepts/grounding-and-verification.md)
- A named [guardrail metric](../systems/khanmigo.md) tracked in production, with a threshold
  that triggers action
- A visible way for students to flag a wrong answer, and a commitment to actually look
- Instructor visibility into what the tutor has been telling their students *in aggregate* —
  which is useful to them and also a safety mechanism

## The academic integrity boundary

[CS50's Duck](../systems/cs50-duck.md) works partly because CS50's honesty policy and the
tool's guardrails were designed together. Most course tutors have to guess where the line is
because the course never wrote it down implementably.

**Ask the instructor sponsor to state, concretely, what help is legitimate on a
thermodynamics problem set.** Not a philosophy — rules a program can follow. If they can't,
the tutor's behavior will be arbitrary until they do, and that's worth reporting as a finding
in its own right. → [guardrails](../concepts/guardrails.md),
[open question C5](../../docs/03-open-questions.md)

Context worth carrying into that conversation: detection is not a fallback. The best AI
detectors reach 85–90% on unmodified AI text and drop to **50–60%** when students edit it, and
a growing number of universities have banned detectors as unreliable. **The line has to be
drawn by design, not enforced by detection.**

## Open questions

- [ ] Should the tutor show confidence, and does a confidence signal actually change student
      behavior — or does it get ignored like a EULA?
- [ ] Should instructors see individual conversations? (Our position: no, and say so — but
      it's the sponsor's call and worth arguing explicitly.)
- [ ] What's our incident process if the tutor teaches something wrong at scale?
- [ ] Does telling students "this is unreliable on refrigerants" reduce use, and is that
      actually a bad outcome?

## Connects to

- [LLM capability in thermodynamics](../domain/llm-thermodynamics-capability.md) — what needs disclosing
- [grounding and verification](../concepts/grounding-and-verification.md) — the technical duty of care
- [IRB](../../admin/irb.md) — the formal requirements
- [guardrails](../concepts/guardrails.md) — the integrity boundary
- [Jill Watson](../systems/jill-watson.md) — the 2016 non-disclosure

## Sources

- [Inside Higher Ed, "AI Detectors Are Out, New Assessments Are In" (Aug 2026)](https://www.insidehighered.com/news/tech-innovation/artificial-intelligence/2026/08/05/ai-detectors-are-out-new-approaches-are) `[skimmed]` — detector accuracy figures
- [PSU AI Studio privacy terms](psu-ai-landscape.md) `[read]`
- [Georgia Tech Jill Watson coverage (2016)](https://news.gatech.edu/news/2016/05/09/artificial-intelligence-course-creates-ai-teaching-assistant) `[skimmed]`
- [Fant-Male & Pieters (2025), "A Review of Personalisation in Human-Robot Collaboration and Future Perspectives Towards Industry 5.0," *IEEE RO-MAN 2025*, pp. 223–230](https://doi.org/10.1109/RO-MAN63969.2025.11217866) `[read — full text, 8 pp., 2026-09-03]` — ⚠ **out of domain: industrial manufacturing robotics, no education content whatsoever.** Assessed and set aside; the two paragraphs above are the only thing we took from it. Local: `course-materials/papers/personalisation-human-robot-collab-review.pdf`. See [the bibliography's "Assessed and set aside" section](../../docs/02-bibliography.md)
