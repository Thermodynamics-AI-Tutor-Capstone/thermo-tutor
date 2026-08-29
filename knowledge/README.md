# The Knowledge Brain

This is where the project's facts live. It is a **cross-linked wiki**, not a folder of
reports: the paper at [`PAPER.md`](PAPER.md) is the way in, and every claim in it links
to a node with the sources behind it.

## Start here

**→ [`PAPER.md`](PAPER.md) — *The State of the Art in AI Tutoring for College Courses***

Read that first, end to end. It's the map. Everything else is territory.

## How this is organized

| Directory | What's in it |
|---|---|
| [`systems/`](systems/) | Individual tutoring systems — one node per system, with history, architecture, and measured results |
| [`concepts/`](concepts/) | Ideas and techniques — knowledge tracing, Socratic tutoring, guardrails, productive failure |
| [`evidence/`](evidence/) | Individual studies, especially RCTs. The empirical record, one node per study |
| [`domain/`](domain/) | Thermodynamics-specific findings — what LLMs can and can't do in *our* subject |
| [`evaluation/`](evaluation/) | Benchmarks and instruments for measuring tutors and learning |
| [`practice/`](practice/) | Deployment realities — cost, LMS integration, compliance, faculty, equity |

## How to use it

**Reading.** Follow the links. Every node ends with a *Connects to* section. If you find
yourself needing background, it's probably one hop away.

**Contributing.** Rules that keep this useful rather than a pile:

1. **One node, one thing.** A system, a concept, a study. If a node is about two things,
   it's two nodes.
2. **Every factual claim carries its source.** Inline, with a link. If we can't cite it,
   it goes in the *Open questions* section of the node, not in the body.
3. **Mark verification status honestly.** Each source is tagged:
   - `[read]` — someone on the team read the full text
   - `[skimmed]` — abstract, summary, or secondary coverage only
   - `[found]` — we know it exists and haven't opened it

   Most of this repo is currently `[skimmed]`. That is a normal starting state and a
   standing to-do, not a defect to hide. **Upgrading a source to `[read]` and correcting
   what was wrong is real work and counts as a contribution.**
4. **Link liberally.** A `[[link]]` to a node that doesn't exist yet is fine — it marks
   something worth writing.
5. **Contradictions stay visible.** When two sources disagree, say so in the node and say
   which we believe and why. Do not average them into mush. See
   [`domain/llm-thermodynamics-capability.md`](domain/llm-thermodynamics-capability.md)
   for a worked example — two 2025-26 benchmarks reach opposite conclusions about the
   same models.

## Node template

```markdown
# <Name>

**Type:** system | concept | study | benchmark
**One line:** <what this is, in a sentence>
**Why we care:** <relevance to our project, one or two sentences>

## <body sections>

## Open questions
- what we don't know about this

## Connects to
- `[Other node](../dir/other.md)` — why they're related

## Sources
- `[Title](url)` `[read|skimmed|found]` — what it's good for
```

## Status

Built August 2026 from a systematic literature sweep. Breadth is decent; depth is
uneven. The biggest gaps are tracked in
[`../docs/03-open-questions.md`](../docs/03-open-questions.md) and in the *Open
questions* section of each node.
