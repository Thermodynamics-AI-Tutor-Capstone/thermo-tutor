# CS50 Duck (ddb / cs50.ai)

**Type:** system
**One line:** Harvard CS50's rubber-duck debugger — the largest and most-studied
course-embedded LLM tutor in production.
**Why we care:** The reference implementation for "helpful but won't spoil the answer,"
at a scale nobody else has reached, with published evaluation methodology we can copy.

## What it is

A conversational AI at [cs50.ai](https://cs50.ai), free to students and teachers
worldwide, built by David J. Malan's team at Harvard. Students ask about their code or
about CS course concepts. It's presented as a rubber duck — the debugging tradition of
explaining your problem out loud to an inanimate object.

Stated pedagogical goal: **a 1:1 tutor available 24 hours a day.**

## The design commitment

The Duck "is mindful of CS50's policy on academic honesty and only answers questions as a
good tutor might, without spoiling answers outright" — it leads students toward answers
rather than handing them over.

Note what makes this workable: **CS50's course policy and the tool's guardrails were
designed together.** The tool doesn't have to guess where the academic-integrity line is,
because the course drew it and the tool enforces it. That coupling is rare and probably
essential. → [guardrails](../concepts/guardrails.md)

## Scale

- **201,000** students and teachers
- **~35,000 prompts/day**, **9.4 million** prompts cumulative
- **800,000+** student questions in the 2024–25 academic year alone
- Rollout: ~70 summer students (Summer 2023) → thousands online → several hundred on
  campus (Fall 2023) → global

**88%** of Duck users rate it always or frequently helpful.

Scale caveat worth noting: CS50's online population is enormous and self-selected. These
are not the engagement numbers of a required course.
→ [engagement decay](../concepts/engagement-decay.md)

## Published evaluation

Two SIGCSE papers, both worth reading for methodology:

- **Liu, Zenke, Liu, Holmes, Thornton, Malan, "Teaching CS50 with AI" (SIGCSE 2024)** —
  the system, the tools, the design decisions.
- **Liu, Zhao, Xu, Perez, Zhukovets, Malan, "Improving AI in CS50: Leveraging Human
  Feedback for Better Learning" (SIGCSE TS 2025)** — evaluation using **29 teaching
  fellows**, 24 completing all 50 comparisons, **1,309 pairwise comparisons** total, 801
  from TFs with 2+ semesters of experience. More-experienced TFs preferred the newer
  version more strongly.

**The TF-pairwise-comparison method is directly reusable for us.** It converts "is this
tutor response good?" — which is otherwise unanswerable — into a measurable preference
judgment by domain experts. It needs no student data and therefore no IRB gate on the
tutor-quality question.

## Open questions

- [ ] What are the actual guardrail mechanisms? Prompt-only, or is there a policy layer?
- [ ] Which models, and has that changed over time?
- [ ] Any published *learning outcome* data, as opposed to satisfaction and preference?
- [ ] What's the retention curve — do students keep using it through the course?
- [ ] How does the Duck handle a student who explicitly demands the answer?
      (Our [defection script](../../research/competitive-teardown/README.md) should test this.)

## Connects to

- [guardrails](../concepts/guardrails.md) — course policy and tool policy designed together
- [Jill Watson](jill-watson.md) — the other flagship long-running deployment
- [PeteChat](petechat-purdue.md) — the same idea, smaller, with published design rationale
- [engagement decay](../concepts/engagement-decay.md) — CS50's numbers are the optimistic
  end of the range

## Sources

- [Liu et al., "Teaching CS50 with AI" (SIGCSE 2024)](https://cs.harvard.edu/malan/publications/V1fp0567-liu.pdf) `[found]` — PDF didn't text-extract; needs a manual read
- [Liu et al., "Improving AI in CS50: Leveraging Human Feedback" (SIGCSE TS 2025)](https://cs.harvard.edu/malan/publications/fp0627-liu.pdf) `[found]` — the TF comparison methodology
- ["Assessment in CS50 with AI" (SIGCSE TS 2025)](https://doi.org/10.1145/3641555.3705061) `[found]`
- [CS50.ai documentation](https://cs50.readthedocs.io/cs50.ai/) `[skimmed]` — scale figures
- [Student-AI Interaction: A Case Study of CS1 Students](https://arxiv.org/html/2407.00305v2) `[found]`
