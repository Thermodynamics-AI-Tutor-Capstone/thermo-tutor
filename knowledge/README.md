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

**Current source status: 105 `[read]`, 73 `[skimmed]`, 71 `[found]`** (plus 2 abstract-only and
2 confirmed inaccessible).

**Second correction pass, 31 Aug 2026** — nine parallel readers worked through the classical
ITS literature, productive failure, engineering RAG deployments, diagrams, the evaluation
ecosystem, and the institutional sources. That produced roughly twenty further corrections. The
ones that changed a design decision:

| What we had said | What the source says |
|---|---|
| BKT can't work at ~3 observations per component | Conflated two counts. Parameters are fit on the **pooled cohort**; our per-student density is ~10× the standard benchmarks |
| Andes used Bayesian networks | **Removed before the results were produced.** *"not the source of Andes1's power"* — an accurate student model is useless if nothing can act on it |
| Productive failure needs collaboration | **It doesn't.** Kapur's largest effects came from individual, unguided generation |
| PF's two core components | There are **seven** criteria; collaboration isn't essential; *instruction building on student solutions* ranks #1 |
| Substep tutoring is worse than step | **Not comparable numbers.** Substep ≈ step ≈ human > answer-only |
| ITS meta-analyses give g ≈ 0.32–0.37 | That's Steenbergen-Hu & Cooper. **Kulik & Fletcher: 0.66. Ma: 0.43** |
| The TCI is our outcome instrument | Never finished; developers discourage use. **Use STPFaSL** |
| Maizey improved grades 5–9% | **No locatable study.** Retracted |
| ASSISTments: two studies, ~a year of gains | **One study**, ~two-thirds of a year — and the **independent replication was null** |
| Stan is the only thermodynamics tutor | **[CyclePad](systems/cyclepad-cycletalk.md) has been in the USNA curriculum since 1996** |
| CycleTalk showed dialogue beats a bare simulator by 0.35 SD | **0.35 SD is a *dose* comparison between two dialogue conditions; the authors discarded their own control comparison over a quiz confound. The real dialogue-vs-control figure is 0.25 SD, from a one-sentence USNA follow-up** — [node](systems/cyclepad-cycletalk.md) |
| CycleTalk was preceded by Wizard-of-Oz studies | **No WoZ study exists.** What preceded it was a human-tutor classroom study (Rosé et al., AI-ED 2005) — [node](systems/cyclepad-cycletalk.md) |
| CycleTalk engaged students in negotiation dialogue about design trade-offs | **Never built.** The negotiation exchange is a CHI *position paper* illustration in future tense. What shipped was scripted short-answer KCDs — [node](systems/cyclepad-cycletalk.md) |
| CycleTalk was a dialogue agent layered on an articulate simulator | **It never called the simulator's explanation facility.** It model-traced student actions against a pre-authored behavior graph and never read cycle state — [node](systems/cyclepad-cycletalk.md) |
| LearnLM's UK RCT shows an AI tutor beat human tutors by 5.5 p.p. | **LearnLM never spoke to a student unsupervised.** 17 expert tutors reviewed every message before it was sent. The comparison is *human + AI drafts* vs *human alone* — [node](systems/learnlm.md) |
| Jill Watson 2024 scores 78.7% vs OpenAI Assistant's 30.7% | **76.7% vs 31.3%** — the earlier figures came from a secondary summary; the primary is [arXiv:2405.11070](systems/jill-watson.md) |
| The original 2016 Jill Watson was a success because students couldn't tell it from a human TA | **The legacy knowledge-based system passes 26.0% of course questions** — below an off-the-shelf OpenAI Assistant. Indistinguishable ≠ correct — [node](systems/jill-watson.md) |

**Third correction pass, 3 Sep 2026 — the primaries behind our headline numbers.** Eight papers
we had been citing secondhand or as `[abstract only]` were acquired and read in full.

| What we had said | What the primary says |
|---|---|
| VanLehn: human tutoring beat substep-based by d = 0.12 | **Sign error. d = −0.12** — substep-based systems slightly *outperformed* human tutors — [node](concepts/vanlehn-2011.md) |
| VanLehn rests on "10 comparisons drawn from 28 evaluation studies" | **A garble.** *Ten* is the number of pairwise comparison *types*; *28* is one row's count. The informal search "yielded 87 comparisons" — [node](concepts/vanlehn-2011.md) |
| Step-based beats answer-based, d = 0.76 vs 0.31 | **Those are separate study sets against different baselines.** The only **direct** manipulation is **two experiments with one database-design tutor, one of them null** — [node](concepts/vanlehn-2011.md) |
| VanLehn 2011 is a meta-analysis | **He says it isn't:** *"this review does not meet current standards for meta-analyses"* — non-replicable search, single coder, and **"reports the assessment with the largest effect size"** per study — [node](concepts/vanlehn-2011.md) |
| The 0.31 for answer-based tutoring is VanLehn's finding | **Imported wholesale from C. Kulik & Kulik (1991)**; the "40% reliable" is his own admitted approximation — [node](concepts/vanlehn-2011.md) |
| Bloom's 2 sigma failed for unclear reasons (small studies, weak controls) | **The tutoring arm's mastery threshold was 90% against the classroom arm's 80%.** *"This alone could account for the advantage"* — and classroom mastery learning alone scored ~1.0 SD — [node](concepts/blooms-two-sigma.md) |
| Substep tutoring is worse than step (d = 0.40 vs 0.76) | Restated precisely: the **direct** contrast is **d = 0.16 over 11 comparisons, 0 reliable.** Equivalence, not penalty — [node](concepts/knowledge-components.md) |
| Kulik & Fletcher's headline ITS effect is 0.66 | **0.66 is the unweighted median.** Their own **random-effects weighted estimate is g = 0.50, 95% CI [0.40, 0.59]** — in the results section, never in the abstract — [node](concepts/vanlehn-2011.md) |
| Kulik & Fletcher's collapse is 0.66 → 0.13 | More precisely **0.73 local → 0.13 standardized**, and it is the **largest of 15 moderators (r = −.63); hold test type constant and every other moderator stops predicting** — [node](concepts/vanlehn-2011.md) |
| ITS effects are ~0.66 against a control group | **Only against a business-as-usual control.** Against a control given the tutor's own content in cheaper form, the median is **0.24** and the mean **0.18**. ⚠ **Ours is the second kind** — [node](concepts/vanlehn-2011.md) |
| ITS effect sizes are roughly uniform across settings | **Postsecondary 0.75 vs K-12 0.44; mathematics 0.40 vs other subjects 0.72; ≤80 participants 0.78 vs >250 participants 0.30** — [node](concepts/vanlehn-2011.md) |
| VanLehn found substep tutoring genuinely weaker | **Kulik & Fletcher diagnose the artefact:** all six nonconventional-control studies were substep systems and none were step-based. *"Due more to the type of control groups in VanLehn's studies than to substep-based tutoring itself"* — [node](concepts/vanlehn-2011.md) |
| ITSs beat human tutors (Kulik & Fletcher) | ⚠ **We do not follow them here.** Their 0.4 for "human tutoring" is drawn mostly from **peer and cross-age** meta-analyses that VanLehn explicitly excluded. Like-for-like, ITS ≈ human tutor — [node](concepts/vanlehn-2011.md) |
| Implementation quality is a deployment detail | **It is an effect-size variable.** Same system: experienced teacher **+0.96**, teachers new to it **−0.23**; 1-minute response lag **0.01** vs **0.31** once fixed; Cognitive Tutor year 1 **−0.06**, year 2 **+0.20** across ~20,000 students — [node](concepts/vanlehn-2011.md) |
| TUM: both AI arms raised scores, neither raised learning | Sharpened: **the control arm had the numerically *largest* knowledge gain (0.85 vs 0.83 and 0.71)** while scoring 29.9% against ChatGPT's 71.8% — [node](evidence/tum-dissociation-2025.md) |
| TUM used "validated scales" for its outcomes | **The knowledge test is 6 items, code comprehension 3, germane load 2, and frustration is a single item.** The authors say two-item subscales *"should be interpreted with caution"* — [node](evidence/tum-dissociation-2025.md) |
| TUM analysed N = 275 | **452 enrolled; 39.2% excluded.** Pre-specified and uniform across arms, but the analysed sample is the protocol-compliant subset — [node](evidence/tum-dissociation-2025.md) |
| Students preferred the tool that taught them less | ⚠ **Only on instrumental items.** ChatGPT won "helped me", "understood me", "easy to use" — but **"overall AI experience" leaned to the scaffolded tutor** (p = .059) — [node](evidence/tum-dissociation-2025.md) |
| A hint ladder must bottom out in the canonical solution | ⚠ **Now contested.** Iris's four-tier ladder *deliberately never reveals the solution*, and it is the design our own §V argues against — [node](evidence/tum-dissociation-2025.md) |
| CycleTalk's human-tutor predecessor showed NPSG learned most, beating the script marginally (p < .1) | **p = .11, and the magnitude is 1–2 points against SDs of 9–10.** On the applied design task **human tutoring and the script tie exactly at 63%**; on the conceptual test both score +3%. The only reliable contrast is that both beat the pseudotutor — [node](systems/cyclepad-cycletalk.md) |
| Rosé 2005 compared three conditions | **It is a 3 × 2 factorial, six conditions.** The crossed **goal-orientation** manipulation — "learn as much as possible" vs "maximise efficiency" — passed its manipulation check and **moved no outcome at all** — [node](systems/cyclepad-cycletalk.md) |
| Human tutoring in thermodynamics is the benchmark to beat | ⚠ **Three graduate-student tutors produced 100%, 38% and 0% on the applied task** (p < .005). **Tutor variance exceeded the treatment effect**, and the excluded tutor *"tended to take over and do the lab for them"* — conceptual residual **−18%** — [node](systems/cyclepad-cycletalk.md) |
| bioTutor was deployed to 407 students | **407 is the enrolment.** 316 gave feedback, **94 (29.7%) reported using it, and 73 completed the questionnaire — the N behind every satisfaction number** — [node](systems/biotutor-eth.md) |
| Five systems converged on an instructor dashboard, so build one | Still true, ⚠ **and not one of the five has been evaluated.** bioTutor's authors: the summaries' *"accuracy, usefulness, and pedagogical reliability were not systematically evaluated,"* and whether lecturers acted on them *"remains to be investigated"* — [node](systems/biotutor-eth.md) |
| bioTutor is a course-grounded chatbot with a dashboard | **Its interaction design is the finding.** The UI requires the student to formulate their own question *and their own answer* before the tutor responds — [node](systems/biotutor-eth.md) |
| Our ~90 knowledge components need a grain, and grain is the whole question | **Grain is one of four axes**, and the decisive one is **rationale vs. convention**: argumentation only produces learning on components that have a reason behind them — [node](concepts/kli-framework.md) |
| KC grain is an argument we settle by judgement | **Two empirical tests exist.** Description length (6–9 words ≈ fact, 10–12 ≈ rule, 12–21 ≈ schema) and **median correct-execution latency (3–6 s / 6–10 s / 10–14 s by type)** — the second is logged for free by any step-based tutor — [node](concepts/knowledge-components.md) |
| Our cross-cutting skills are an unusual feature of engineering | They have a name and a discovery method: **integrative KCs**, found by `P(hard task) ÷ P(easy task)` on paired problems — [node](concepts/kli-framework.md) |
| Our outcome should be a distal, unassisted measure | Necessary but not sufficient. **Robust learning has three legs — retention, transfer, and *accelerated future learning* — and we plan for one.** KLI also insists the denominator is **instructional time** — [node](concepts/kli-framework.md) |

**The through-line:** nearly every correction made a claim *weaker and more specific*.
Summaries — including good ones — round findings toward their headline, and secondary sources
propagate misattributions. Two numbers we were citing turned out not to exist in their cited
sources at all.

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

**When the publisher blocks scripted downloads, go to the repository copy.** Sage, IOS Press and
Springer all serve bot challenges, but the author's institutional repository usually holds a
CC-BY copy. `locations` in the OpenAlex response lists them. For **DSpace 7** repositories (ETH
Zürich, most European universities) the web page is a JavaScript app that returns nothing useful
to curl — use the REST API instead:

```bash
# 1. handle -> item UUID
curl -s "https://<host>/server/api/pid/find?id=hdl:20.500.11850/<N>" | python3 -c "import json,sys;print(json.load(sys.stdin)['uuid'])"
# 2. UUID -> bundles; take the one named ORIGINAL
curl -s "https://<host>/server/api/core/items/<UUID>/bundles"
# 3. bundle -> bitstreams; the content href is the PDF
curl -s "https://<host>/server/api/core/bundles/<BUNDLE_UUID>/bitstreams"
```

This is how we got [Sinha & Kapur 2021](concepts/productive-failure.md) after Sage refused.

**ASEE papers: append `.pdf` to the ID.** `peer.asee.org/<id>` serves a Cloudflare challenge that
defeats curl and WebFetch alike; `peer.asee.org/<id>.pdf` serves the file directly. ASEE is the
main venue for engineering-education research — including work on our own course — and this makes
all of it reachable.

```bash
curl -sL "https://peer.asee.org/56669.pdf" -o paper.pdf   # works
```

⚠ **Search ASEE, ASME and IEEE Access by hand.** They are largely invisible to arXiv- and
Semantic-Scholar-shaped queries, and they are where engineering-education research lives. Both
[GPThermo](systems/gpthermo-wpi.md) and the Porto systematic review were missed by every automated
sweep and surfaced only through OpenAlex **title** queries.

**Keep verification tags in sync across nodes.** The same paper is often cited from several
nodes, and upgrading one to `[read]` leaves the others stale — which makes the base look less
sourced than it is and invites needless re-reading. This finds them:

```bash
python3 - <<'EOF'
import re, pathlib, collections
rank = {'read':3, 'skimmed':2, 'abstract only':1, 'found':0, 'inaccessible':0}
seen = collections.defaultdict(list)
pat = re.compile(r'\]\((https?://[^)]+)\)[^`\n]{0,80}`\[([a-z][^\]]*?)\]`')
for md in pathlib.Path('knowledge').rglob('*.md'):
    for m in pat.finditer(md.read_text()):
        url = m.group(1).rstrip('/').split('#')[0]
        tag = m.group(2).split('—')[0].strip()
        base = tag if tag in rank else ('read' if tag.startswith('read') else tag)
        seen[url].append((md, tag, rank.get(base, -1)))
for u, v in seen.items():
    if len(v) > 1 and len({r for _,_,r in v}) > 1:
        best = max(r for _,_,r in v)
        print(u[:80])
        for md, tag, r in v:
            print(f"   {'KEEP ' if r==best else 'STALE'} [{tag[:28]:28s}] {md}")
EOF
```

**Verify what you downloaded is actually a PDF.** A login wall or maintenance page returns HTTP
200 with HTML, and `file` reports the *filename* — so `file x.pdf | grep pdf` always matches.
Check the magic bytes instead: `head -c 5 x.pdf | grep -q '%PDF'`.

**Known-blocked, do not keep retrying:** ASU (`public.asu.edu`) is behind Cloudflare Access, so
VanLehn's own copies of his papers now require an ASU login. DTIC has been under maintenance
throughout. CMU KiltHub serves Cloudflare JS challenges. IOS Press blocks entirely. For these,
**PSU library access is the answer**, not another download attempt.
