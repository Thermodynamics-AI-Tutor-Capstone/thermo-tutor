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
