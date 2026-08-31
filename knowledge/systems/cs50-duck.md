# CS50 Duck (ddb / cs50.ai)

**Type:** system
**One line:** Harvard CS50's rubber-duck debugger — the largest and most-studied
course-embedded LLM tutor in production.
**Why we care:** The reference implementation for "helpful but won't spoil the answer,"
at a scale nobody else has reached, with published evaluation methodology we can copy.

> **Verification: `[read]` — "Teaching CS50 with AI" (SIGCSE 2024) full text, 2026-08-31.**

## What it is — three tools, not one

Built by David J. Malan's team at Harvard, deployed Summer 2023 onward:

1. **"Explain Highlighted Code" (EHC)** — a VS Code extension emulating what a human
   instructor does when you point at a confusing line
2. **style50** — code style evaluation
3. **The CS50 Duck (ddb)** — the conversational rubber-duck debugger, at
   [cs50.ai](https://cs50.ai), in VS Code, **and inside Ed**, the course discussion forum

Stated goal: *"approximate a 1:1 teacher-to-student ratio through software... designed to
guide students toward solutions rather than offer them outright."*

**The policy coupling is explicit and load-bearing:** per the course's own policy, CS50
*encouraged* these tools and **limited the use of commercial AI** (ChatGPT, GitHub Copilot,
Bing). The course tool wasn't competing against a better free alternative — the course
removed the alternative. Very few deployments can do this, and it is probably a large part of
why CS50's engagement numbers are so much better than everyone else's.
→ [engagement decay](../concepts/engagement-decay.md)

## The design commitment

The Duck "is mindful of CS50's policy on academic honesty and only answers questions as a
good tutor might, without spoiling answers outright" — it leads students toward answers
rather than handing them over.

Note what makes this workable: **CS50's course policy and the tool's guardrails were
designed together.** The tool doesn't have to guess where the academic-integrity line is,
because the course drew it and the tool enforces it. That coupling is rare and probably
essential. → [guardrails](../concepts/guardrails.md)

## Mechanisms worth stealing

**Usage throttling via "hearts."** Each student starts with **10 hearts**, regains one every
**three minutes**, and spends one per Duck interaction. Framed by the team as *dual-purpose*
— it controls GPT-4 costs, and it is pedagogy:

> *"it promotes thoughtful interaction with the CS50 Duck by encouraging students to
> carefully consider their questions. The underlying goal is to foster independent
> problem-solving skills and the ability to formulate precise questions... [and] encourages
> reflective breaks."*

**This is a [productive-failure budget](../concepts/productive-failure.md) implemented as a
rate limit, running at the scale of 200,000 users.** Students asked for it to be relaxed; the
team declined. It is the closest thing in production to the deterministic hint budget our
[Socratic tutoring](../concepts/socratic-tutoring.md) node argues for.

**Prompt-injection guard.** Every student request is checked for atypical non-alphanumeric
patterns. If triggered, CS50.ai makes an **independent GPT-4 call** to classify the input as
legitimate or an injection attempt; a confirmed attack **aborts the session**. A concrete,
implementable answer to our [defection script](../../research/competitive-teardown/README.md).

**Human-in-the-loop on the forum.** Every Duck response on Ed is *"subject to endorsement,
amendment, or deletion by a human staff member."*

**RAG over lecture captions** — segmented into self-contained **30-second** chunks, embedded
with `text-embedding-ada-002`, stored in **ChromaDB**, top-N retrieved per query. Note this is
the opposite choice from [Stan](stan-udel.md), which rejected vector RAG in favour of the
textbook's own index. → [RAG in education](../concepts/rag-in-education.md)

Configuration lives in **YAML** — different system prompts and user-prompt templates per use
case (CS questions, code explanation, style feedback).

## Scale and measured accuracy

- **50,000+ unique users** by December 2023; **201,000** students and teachers later
- **~35,000 prompts/day**, **9.4 million** cumulative
- **800,000+** questions in the 2024–25 academic year alone

**Accuracy, independently reviewed** (a senior staff member outside the dev team graded the
Duck's Ed answers, Summer 2023, 64 answers):

| Category | Correct |
|---|---|
| Curricular (25 answers) | **22/25 = 88%** |
| Administrative (39 answers) | **30/39 = 77%** |

The team's benchmark for context: ChatGPT is correct only ~48% of the time on software
engineering topics. Administrative accuracy is lower because GPT-4's training cutoff lags the
evolving syllabus — a grounding problem, not a reasoning one.

Fall 2023: of 180 Ed answers, only **70 were endorsed** by staff — an apparent 39%. The team
suspects this understates accuracy because Ed usage collapsed (see below) and only harder
questions were escalated there.

## Engagement — the best profile in this knowledge base

End-of-semester survey, ~500 on-campus students, 73% response rate:

| | |
|---|---|
| Used "constantly" | **28%** |
| Used "frequently" | **50%** |
| Used "infrequently" | 19% |
| **Never used** | **3%** |
| "Loved" them | 53% · "liked" 33% · neutral 13% · disliked 1% |

Mid-semester, 47% found them "very helpful"; but only **23% were "very confident"** in their
accuracy, which is a healthy sign that the "think critically" messaging landed.

Compare [KAIST](../evidence/kaist-vta-2025.md), where **50% never used the tutor at all**.

**The substitution effect.** Forum traffic collapsed as the Duck scaled:

| Term | Questions per student on Ed |
|---|---|
| Fall 2022 | 0.89 |
| Summer 2023 | 1.1 |
| **Fall 2023** | **0.28** |

A ~75% drop. Students moved to synchronous Duck interaction and escalated only hard questions
to humans. **Worth thinking about:** the AI became the primary witness to student confusion,
and human staff lost visibility.

**Anthropomorphism helped.** The team credits the lovable-duck framing for adoption —
*"Love love loved the duck. We're friends now."* [KAIST found the same effect
independently](../evidence/kaist-vta-2025.md).

**Their honest limitation**, worth quoting for our
[disclosure node](../practice/disclosure-and-ethics.md):

> *"Occasional inaccuracies alone would be permissible — human teachers are surely
> susceptible to error themselves — but AI tends to exhibit a tone of complete and
> authoritative confidence even when wrong, while humans might qualify the certainty of their
> answers."*

Scale caveat: CS50's online population is enormous and self-selected. These are not the
engagement numbers of a required course.

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

- [x] ~~What are the guardrail mechanisms?~~ System prompt + hearts throttle + injection
      guard + human endorsement on Ed + course policy limiting commercial AI.
- [x] ~~Which models?~~ GPT-3.5 and GPT-4 in combination as of the 2024 paper.
- [ ] **Any published learning-outcome data?** Still none found — satisfaction, usage, and
      answer accuracy only. Across 9.4M prompts, that absence is striking.
- [ ] Did the hearts throttle actually change question quality? They assert the pedagogical
      benefit; nobody measured it. **Testable, and a genuinely novel small study.**
- [ ] How does the Duck handle a student who explicitly demands the answer?
      (Our [defection script](../../research/competitive-teardown/README.md) should test this.)
- [ ] Read the 2025 follow-up ("Improving AI in CS50: Leveraging Human Feedback") for the
      TF-comparison methodology in detail.

## Connects to

- [guardrails](../concepts/guardrails.md) — course policy and tool policy designed together
- [Jill Watson](jill-watson.md) — the other flagship long-running deployment
- [PeteChat](petechat-purdue.md) — the same idea, smaller, with published design rationale
- [engagement decay](../concepts/engagement-decay.md) — CS50's numbers are the optimistic
  end of the range

## Sources

- [Liu, Zenke, Liu, Holmes, Thornton & Malan, "Teaching CS50 with AI" (SIGCSE 2024)](https://cs.harvard.edu/malan/publications/V1fp0567-liu.pdf) `[read]` — full text
- [Liu et al., "Improving AI in CS50: Leveraging Human Feedback" (SIGCSE TS 2025)](https://cs.harvard.edu/malan/publications/fp0627-liu.pdf) `[found]` — the TF comparison methodology
- ["Assessment in CS50 with AI" (SIGCSE TS 2025)](https://doi.org/10.1145/3641555.3705061) `[found]`
- [CS50.ai documentation](https://cs50.readthedocs.io/cs50.ai/) `[skimmed]` — scale figures
- [Student-AI Interaction: A Case Study of CS1 Students](https://arxiv.org/html/2407.00305v2) `[found]`
