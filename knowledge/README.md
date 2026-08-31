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

Built August 2026 from a systematic literature sweep, then deepened on **31 Aug 2026** by
reading **15 papers in full** rather than from summaries.

**That reading pass produced eight corrections to things this base had asserted.** They are
flagged with ⚠ in the affected nodes and summarised at the top of
[`PAPER.md`](PAPER.md). The largest:

| What we had said | What the source actually says |
|---|---|
| Stan is our closest competitor, a Socratic thermo tutor | It targets **Levels 1–2 only** (point to the page, summarize) and explicitly excludes tutoring. No evaluation of any kind |
| The TCI is a validated PSU-developed instrument, our outcome measure | **Developers discourage its use**; *"never finished"*; PhysPort's lowest validation rating. Use the TTCI-T |
| Diagram reading is a uniform 32% wall | Range is **6% to 76%**; reasoning models largely clear it |
| Voluntary AI-tutor users skew already-advantaged | At university level the **least-prepared** students used it **14× more** |
| Khanmigo's study was observational | It is a **two-year cluster RCT**, and the AI added no detectable learning |
| Socratic-subversion evidence is strong | One course, one week, one problem, extra credit, and the authors disclaim causal inference |
| o3 solved every exam problem correctly | It lost points on graphics and made one major error |

**The pattern is worth internalizing:** in nearly every case, reading the primary source made
the claim *weaker and more specific*. Summaries — including good ones — systematically round
findings toward their headline. That is why the `[read]` / `[skimmed]` / `[found]` tags exist.

**Current source status: 54 `[read]`, 86 `[skimmed]`, 80 `[found]`.**

Remaining priority reads are listed at the end of [`PAPER.md`](PAPER.md) §IX.

**A note on access, because it cost us a day of wrong assumptions:** we recorded
[Kestin et al.](evidence/kestin-2025-rct.md) as paywalled. It is **gold open access** —
the earlier failure was a cookie-consent redirect, not a paywall. Before assuming a paper is
inaccessible, check **OpenAlex** for an OA location:

```bash
curl -s "https://api.openalex.org/works/doi:<DOI>" | python3 -m json.tool | grep -A3 best_oa_location
```

It returns the free PDF URL when one exists, and also surfaces PubMed Central and DOAJ
mirrors. Most of what looks paywalled in this field is not.
