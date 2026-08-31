# Roadmap

A research-first plan. Deliberately no build phase scheduled — we'll add one when the
research says what to build, and that decision gets written down as an ADR first.

Dates are placeholders. Fill them in against the actual capstone calendar.

---

## Phase 0 — Unblock (weeks 1–2)

Everything here is a dependency for something else. Do it now, in parallel, or it
compounds.

| Item | Why it's first | Owner |
|---|---|---|
| **CITI training, all members** | Hard prerequisite for IRB submission; takes hours | |
| **IRB protocol drafted and submitted** | Blocks every student conversation. Weeks of lead time. | |
| **Instructor sponsor meeting** | Answers in `admin/canvas-access.md` gate several decisions | |
| **Confirm course + textbook** | Determines notation, tables, the whole knowledge model | |
| **Ask about PSU enterprise LLM agreement** | Could remove the entire FERPA obstacle in one email | |
| **PhysPort educator verification (for the TTCI-T)** | Slow, and it's our outcome measure. ⚠ *Not* the TCI — see [concept inventories](../knowledge/evaluation/concept-inventories.md) | |

**Do not** start writing an application while this is pending. There's nothing to build
yet and it will be wrong.

## Phase 1 — Understand (weeks 3–7)

Two tracks in parallel. The teardown track isn't IRB-blocked, so it runs regardless of
how the IRB queue goes — which is exactly why it should be someone's job on day one.

### Track A — Competitive teardown *(not IRB-blocked, start immediately)*
- Finalize the five-problem set with instructor review
- Run tier 1 tools (ChatGPT, Claude, Gemini, Chegg)
- Run tier 2 incumbents (Mastering, Connect, WileyPLUS) — needs sponsor for access
- Produce the comparison matrix
- **Key output:** where every tool fails in the same place

### Track B — Student research *(IRB-gated)*
- Recruit 12–15 participants across the sampling frame
- Run interviews
- Run 4–6 think-aloud sessions (higher effort, much higher signal)
- Open-code, reconcile, synthesize
- **Key output:** where in the problem-solving process students actually seek help, and
  what triggers the switch to answer-seeking

### Track C — Domain modeling *(no dependencies)*
- Instructor review of `research/domain/skill-graph-draft.md`
- Misconception literature search
- Map KCs to one semester of real assignment problems
- Run the observations-per-KC calculation (question C2)

## Phase 2 — Synthesize and specify (weeks 8–11)

- Reconcile the three tracks. Where do students' reported problems, the tools' actual
  failures, and the concept map agree?
- Build the **thermodynamics tutoring benchmark** (question B4) — correctness set plus
  pedagogy set. This is the most likely publishable output and it needs no student data.
- Run existing tools against the benchmark to establish baselines.
- Write the design spec: what would we build, and what does it do that nothing above
  does?
- **Answer question C3 in writing** — what counts as success — before any pilot design.

## Phase 3 — Rough drafts (weeks 12+)

Prototypes to think with, not products. Explicitly disposable.

Candidates, in rough order of value-per-effort:

- **Paper prototype / Wizard-of-Oz.** A team member plays the tutor over chat, following
  a hint-ladder policy by hand. Tests the pedagogy with zero engineering. Probably the
  highest-information experiment available to us.
- **Prompt-only baseline.** Claude or GPT with a carefully written tutoring prompt and
  the course syllabus pasted in. Establishes what the trivial version already achieves —
  and the honest floor we'd have to beat.
- **Property-tool spike.** Wire CoolProp/Cantera to a model via tool calls and check
  whether it fixes the property-data failure. Small, self-contained, answers a real
  question.
- **Hint-ladder mock.** A static UI showing graduated hints for one problem. Something to
  put in front of students.

Each prototype should answer a named question from `docs/03-open-questions.md`. If it
doesn't, don't build it.

## Not scheduled

- Application architecture
- Canvas integration
- Deployment
- The tutor itself

These come after Phase 2 says what they should be. If they get scheduled earlier,
something has gone wrong with the plan.

---

## Standing risks

| Risk | Mitigation |
|---|---|
| IRB takes longer than expected | Track A and C are unblocked; sequence them first |
| Instructor sponsor becomes unavailable | Document everything they tell us; don't single-thread on one conversation |
| We drift into building because building is more fun | This roadmap. Re-read it. |
| Research produces "students want an answer machine" | That is a finding, not a failure. Report it. |
| Scope creep into a full LMS | The deliverable is a tutor, informed by research |
