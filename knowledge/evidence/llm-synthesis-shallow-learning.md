# Learning from LLM syntheses is shallower — and citations don't fix it (n = 10,462)

**Type:** evidence
**One line:** Across **seven experiments with 10,462 participants**, people who learned a topic
from an LLM summary developed **shallower knowledge** than people who learned the same facts from
web links — **and adding real-time source links did not repair it.**
**Why we care:** Our whole grounding layer assumes provenance is the fix. This says provenance
fixes *accuracy*, not *depth*, and names the mechanism: **the synthesis is the problem, not the
sourcing.**

> **Verification: `[read]` — full text, 11 pp., 2026-09-01.**

*"Experimental evidence of the effects of large language models versus web search on depth of
learning."* **PNAS Nexus** 4, pgaf316 (2025).
[DOI 10.1093/pnasnexus/pgaf316](https://doi.org/10.1093/pnasnexus/pgaf316).

## The theory

> *"When individuals learn about a topic from LLM syntheses, they risk developing shallower
> knowledge than when they learn through standard web search, **even when the core facts in the
> results are the same**."*

The mechanism is structural, not a quality failure: the summary format *"**inhibits users from
actively discovering and synthesizing information sources themselves**, as in traditional web
search."* Search is effortful, and that effort has *"the often-overlooked benefit of constructing
deeper, and more unique, knowledge structures."*

**This is the same mechanism as [TUM's reduced germane cognitive load](tum-dissociation-2025.md),
arriving from a completely different literature.** One measures the load that disappears; the
other measures what disappears with it.

## What they measured

Not a knowledge test — something cleverer. Participants searched a topic, then **wrote advice for
another person** on it. That advice was scored, and shown to real recipients.

People who learned from LLM syntheses:

- **felt less invested** in forming their advice
- produced advice that was **sparser**, **less original**, and
- **less likely to be adopted by recipients**

**The downstream harm is measurable in a third party's behaviour**, which is a much harder outcome
to dismiss than a self-report.

## ⚠⚠ The finding that hits our architecture directly

> *"Participants reported developing shallower knowledge from LLM summaries **even when the
> results were augmented by real-time web links**."*

**Citations did not restore depth.**

Every grounded tutor in this knowledge base —
[Jill Watson](../systems/jill-watson.md), [Ethel](../systems/ethel-eth.md),
[PeteChat](../systems/petechat-purdue.md), [ARIA](../concepts/rag-in-education.md) — treats
source display as the answer to "how do we know this is trustworthy." **It is, for accuracy.**
This says it does **not** address the separate problem that reading a synthesis is a shallower act
than assembling an understanding yourself.

**Two different jobs, and we had been conflating them:**

| Problem | Fix |
|---|---|
| The tutor might be **wrong** | Retrieval grounding, provenance, a solver |
| The student learns **less deeply from being told** | ⚠ **Unsolved by any of the above** |

The second is what [productive failure](../concepts/productive-failure.md) and
[step-based interaction](../concepts/vanlehn-2011.md) exist to address, and it is why
**a tutor that answers well is not thereby a tutor that teaches well.**

## What we should do about it

1. **Stop treating provenance as pedagogy.** Showing sources is an accuracy and trust feature.
   Budget for depth separately.
2. **Make the student do the synthesis.** The
   [sub-question decomposition loop](../concepts/grounding-and-verification.md) is well-suited:
   the student assembles the solution and the system checks each step, rather than the system
   assembling and the student reading.
3. ⭐ **This is a testable design question for us.** Same thermodynamics content, delivered as a
   synthesis versus assembled by the student under guidance, measuring depth. Cheap, and nobody
   has run it in a technical domain.
4. **Note where it may not transfer.** Their task is open-ended topic learning and advice-giving.
   Thermodynamics problem-solving has a correct answer and a fixed procedure, which may make the
   "discover and synthesize sources" step less central. **Plausible boundary condition, untested.**

## ⚠ Limits

Seven online and laboratory experiments — **not classroom, not a technical subject, not graded
coursework.** The outcome is advice quality, not exam performance. Google's own "AI Overviews"
motivate the framing, so the target is search behaviour rather than tutoring specifically. Take
the mechanism as well-evidenced and the transfer to engineering education as an open question.

## Connects to

- [TUM dissociation](tum-dissociation-2025.md) — the same mechanism, measured as germane load
- [Grounding and verification](../concepts/grounding-and-verification.md) — what provenance does and doesn't buy
- [Productive failure](../concepts/productive-failure.md) — why the effort has to stay
- [RAG in education](../concepts/rag-in-education.md)
- [Bastani et al. 2025](bastani-2025-harm.md)

## Sources

- [\"Experimental evidence of the effects of large language models versus web search on depth of learning,\" *PNAS Nexus* 4, pgaf316 (2025)](https://academic.oup.com/pnasnexus/article-pdf/4/10/pgaf316/64956155/pgaf316.pdf) `[read — full text, 11 pp., 2026-09-01]` — gold OA
