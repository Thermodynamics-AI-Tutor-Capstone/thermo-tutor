# Kestin et al. 2025 — AI tutoring outperforms in-class active learning

**Type:** study (RCT)
**One line:** Harvard physics, n=194. An AI tutor produced roughly **2× the learning gains**
of an active-learning classroom, in less time, with higher engagement.
**Why we care:** The field's best result, the strongest argument that this is worth doing,
and — read carefully — a much narrower claim than it's usually quoted as.

## The study

Greg Kestin, Kelly Miller, Anna Klales, Timothy Milbourne, Gregorio Ponti.
**Scientific Reports, June 2025.** Harvard **Physical Sciences 2**, Fall 2023, ~180–194
students.

**Design — the part worth copying.** Within-subject alternating: students switched weekly
between two conditions. One week, an in-class session using refined active-learning methods.
The next, at home with a purpose-built AI tutor.

This design does three things well:
- Every student gets both conditions, so nobody is denied the tool — which dissolves the
  ethical objection to withholding
- Each student is their own control, which is enormously statistically efficient at n=194
- It's realistic — the tutor is used how a tutor would actually be used

**We should copy this design.** → [our roadmap](../../admin/roadmap.md)

## The results

- **Roughly 2× the learning gains** of the active-learning condition
- **Less time** spent on the content
- Higher self-reported engagement, motivation, and satisfaction

## The design of the tutor

Reported features: **expert-authored scaffolds**, enforced step-by-step reasoning, and
built-in guardrails against hallucination.

Note what's *not* in that list: no novel model, no fine-tuning, no knowledge tracing. The
described innovation is **hand-built pedagogical structure for specific problems**, by a
physics-education researcher who knew where students get stuck.

## Reading it honestly

**What makes it strong:**

The comparison condition was **active learning**, not lecture. Active learning is the
well-evidenced gold standard in physics education; beating it 2× is a serious result.
Substituting "lecture" here would make the finding far less impressive, and many secondary
write-ups blur this.

**What makes it narrow:**

- **n = 194, one course, one semester, one institution.** Harvard undergraduates in a
  physical sciences course are not a general population.
- **One instructor, who is a physics education researcher.** Kestin built the tutor. The
  intervention and the expertise are confounded, and probably inseparably.
- **The scaffolds were hand-authored per problem.** This is the part that doesn't transfer
  by copying a prompt, and it's plausibly where the entire effect lives.
- Effect sizes in education technology reliably shrink as studies scale. Compare
  [Tutor CoPilot](../systems/tutor-copilot.md) (n=1,800, +4pp) and
  [Bastani](bastani-2025-harm.md) (n=1,000, ≈0).

## The lesson we should actually take

Not "AI tutors produce 2× gains." The defensible reading is:

> **An AI tutor, built by a domain expert with hand-authored scaffolds for specific
> problems in a specific course, outperformed an excellent classroom in that course.**

Which tells us where to spend our effort: **the thermodynamics domain work — the problems,
the misconceptions, the hint ladders — is the project.** The architecture is plumbing.

It also tells us what our comparison condition should be, and that the honest one is hard.
→ [open question C4](../../docs/03-open-questions.md)

## Open questions

- [ ] **Read the full paper.** Effect sizes, instruments, what the scaffolds actually were.
- [ ] Is the tutor or its prompts published anywhere?
- [ ] How much authoring effort per problem? This sets our achievable scope.
- [ ] What was the outcome measure — a concept inventory, or course-specific items?
      → [concept inventories](../evaluation/concept-inventories.md)
- [ ] Has anyone replicated it in another course or institution?

## Connects to

- [Bastani 2025](bastani-2025-harm.md) — the contrasting null result, and the reconciliation
- [Bloom's 2 sigma](../concepts/blooms-two-sigma.md) / [VanLehn 2011](../concepts/vanlehn-2011.md) — the baselines to read this against
- [concept inventories](../evaluation/concept-inventories.md) — how to measure gains
- [our roadmap](../../admin/roadmap.md) — the alternating design is directly reusable

## Sources

- [Kestin et al., "AI tutoring outperforms in-class active learning," *Scientific Reports* (2025)](https://www.nature.com/articles/s41598-025-97652-6) `[skimmed]` — **priority full read**
- [Hechinger Report coverage](https://hechingerreport.org/proof-points-ai-tutor-harvard-physics/) `[skimmed]`
- [Harvard Gazette, "Professor tailored AI tutor to physics course. Engagement doubled."](https://news.harvard.edu/gazette/story/2024/09/professor-tailored-ai-tutor-to-physics-course-engagement-doubled/) `[skimmed]`
- [ETC Journal critical review of the study](https://etcjournal.com/2025/11/10/review-of-kestin-et-al-s-june-2025-harvard-study-on-ai-tutoring/) `[found]` — read this for the critiques
