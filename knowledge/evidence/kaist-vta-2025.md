# KAIST VTA deployment (2025)

**Type:** study (large-scale real-world deployment)
**One line:** An LLM teaching assistant deployed to 477 graduate students for 14 weeks —
the best usage dataset in this knowledge base, and it says the students who used it most
were the ones with the *least* prior experience.
**Why we care:** It is the only study here that measures voluntary university-level
engagement, cost, and *who* uses an AI tutor, all at once. Two of its findings correct
claims elsewhere in this wiki.

> **Verification: `[read]` — full text, 2026-08-31.**

## The study

Sunjun Kweon, Sooyohn Nam, Hyunseung Lim, Hwajung Hong, Edward Choi — **KAIST**, South
Korea. arXiv:2506.17363.

- **477 graduate students**, introductory AI programming course, **14-week** deployment
- **3,869** student–VTA interaction pairs across **916 conversations**
- **Three survey rounds**: pre-, mid-, and post-deployment
- Compared against **144 student–instructor interactions** from the same course the prior year
- Source released: [github.com/sean0042/VTA](https://github.com/sean0042/VTA)

## Finding 1 — the usage distribution, in full

| Group | Usage | Students | Total Q&A |
|---|---|---|---|
| A | ≥100 times | **6** | 1,154 |
| B | 18–99 | 53 | 1,872 |
| C | 5–17 | 69 | 604 |
| D | <5 | 107 | 239 |
| **E** | **never used it** | **237** | — |
| | | **472** | **3,869** |

**Half the class never touched it.** Six students — **1.3%** — generated **30%** of all
interactions. Groups A and B together, **12.5% of the class, produced 78%** of all traffic.

This is the power-user concentration our [equity](../practice/equity.md) node previously
sourced from a consultancy blog, now confirmed with real university data.
→ [engagement decay](../concepts/engagement-decay.md)

## Finding 2 — who used it, and this reverses our earlier claim

Average interactions, by **prior coding experience**:

| Prior experience | Avg. interactions |
|---|---|
| **None** | **62.2** |
| Beginner | 11.2 |
| Intermediate | 5.5 |
| Advanced | 4.5 |

The same pattern held for prior machine-learning knowledge. **Students with the least
preparation used the tutor an order of magnitude more than the best-prepared.**

Reinforcing it: the pre-survey asked whether students had ever refrained from asking a human
instructor a question *"due to discomfort, fear of burdening them, or concern that your
question might seem silly."* **58% said yes.**

| | Comfort (pre) | Comfort (post) | Avg. usage |
|---|---|---|---|
| Had refrained from asking humans | 0.69 | 0.76 | **13.2** |
| Had not | 0.42 | 0.47 | 7.8 |

**The students who were too intimidated to ask a person used the AI most, and got more
comfortable over the term.**

This directly contradicts the "voluntary AI tools benefit the already-advantaged" claim, at
least in this setting. Both patterns can be true in different populations — the
consultancy-sourced 5% figure is K-12-flavored, this is graduate-level — but for *our*
setting (university engineering), **this is the better evidence, and it points the other
way.** → [equity](../practice/equity.md)

## Finding 3 — the AI absorbed the conceptual questions

Distribution of question types, human TA (prior year) vs. VTA:

| Question type | Human TA | Virtual TA |
|---|---|---|
| Coding practice | 9.0% | 10.4% |
| **ML theory** | **8.3%** | **35.0%** |
| Projects | 66.4% | 39.7% |
| Course operation | 15.3% | 9.7% |

Students asked the VTA **four times as many conceptual/theory questions** as they had asked
human TAs. The "I don't understand the concept" questions were apparently not being asked of
humans at all — consistent with the 58% hesitancy figure.

**For our project this is the strongest available argument to an instructor sponsor:** the
tutor surfaces confusion that currently goes unvoiced, and (if logged) makes it visible.
→ [faculty adoption](../practice/faculty-adoption.md), and compare
[Stan's question mining](../systems/stan-udel.md)

## Finding 4 — perceptions diverge by usage

- **Helpfulness declined overall**: 3.64 (pre) → 3.60 (mid) → **3.54** (post)
- **But among high-frequency users (A/B/C) it improved significantly** (p = 0.043)
- **Group D (<5 uses) collapsed**: 3.72 → **3.26**. Group D also rated *human* TAs highest
  (4.06) — they had high expectations, used it 2.2 times on average, and were disappointed
- **Trustworthiness rose** after deployment (students were initially skeptical) but stayed
  **below human instructors** throughout

The aggregate satisfaction number hides two opposite trends. **Reporting only the mean would
have been actively misleading** — a lesson for our own evaluation design.

## Finding 5 — anthropomorphism predicts engagement

**123 of 916 conversations (13%)** contained social cues — greetings, thanks, relational
remarks. Those students averaged **27.8 interactions** versus **11.4** for the rest.

Echoes [CS50's duck](../systems/cs50-duck.md), where students said *"Love love loved the
duck. We're friends now"* and the team credited the lovable framing for adoption. Two
independent deployments, same signal.

## Finding 6 — the real cost number

**$180 total** for the 14-week deployment across 477 students, covering API usage and
conversation-log storage.

That is **$0.38 per enrolled student**, or about **$0.76 per student who actually used it**.
An order of magnitude below the vendor-blog estimate our
[cost node](../practice/cost-economics.md) previously carried. Measured, published, and from
a real course.

## Open questions

- [ ] What model, and what did the system prompt look like? (Source is released — read it.)
- [ ] Why did 237 students never engage at all? Not investigated.
- [ ] Does the inexperienced-students-use-it-more pattern hold in undergraduate engineering,
      or is it specific to graduate students who know they're behind?
- [ ] Any learning-outcome data, or perception and usage only? (Appears to be the latter.)

## Connects to

- [equity](../practice/equity.md) — **this node corrects it**
- [engagement decay](../concepts/engagement-decay.md) — the distribution, and Group D
- [cost economics](../practice/cost-economics.md) — the real per-student figure
- [CS50 Duck](../systems/cs50-duck.md) — anthropomorphism, and a contrasting engagement profile
- [Khanmigo engagement](khanmigo-engagement-2026.md) — the K-12 comparison

## Sources

- [Kweon, Nam, Lim, Hong & Choi, "A Large-Scale Real-World Evaluation of an LLM-Based Virtual Teaching Assistant," arXiv:2506.17363](https://arxiv.org/abs/2506.17363) `[read]` — full text
- [github.com/sean0042/VTA](https://github.com/sean0042/VTA) `[found]` — source released
