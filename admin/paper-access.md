# Papers we cannot reach, and exactly what unblocks each

**Drop retrieved PDFs into `course-materials/papers/`** (git-ignored — safe for anything
copyrighted). Tell me when they land and I'll read and integrate them.

Three categories, easiest first. **Category A is free and legal — those papers are already open
access and are blocked only by bot detection.**

---

## A. Open access, blocked only by a bot check

**These are not paywalled.** Opening the link in a normal browser and hitting "download PDF" gets
them in under a minute each. My scripted fetches get 403s because I'm not a browser.

| # | Paper | Why we want it | Link |
|---|---|---|---|
| A1 | ⭐ **Porto: PRISMA review of 46 AI-tutor studies in engineering education** (IEEE Access, gold OA) | **The single highest-value item on this list.** A systematic map of our exact field — it tells us what our search has been missing | [ieeexplore.ieee.org/document/11217866](https://ieeexplore.ieee.org/document/11217866) |
| A2 | **TUM: "Less stress, better scores, same learning"** (Elsevier, gold OA) | We have the abstract; the **effect sizes, cognitive-load scales and figures are unread**. Our sixth dissociation study | [doi.org/10.1016/j.caeai.2025.100537](https://doi.org/10.1016/j.caeai.2025.100537) |
| A3 | **bioTutor** (MDPI *Educ. Sci.*, gold OA) | Abstract only. Need the **link to its open-source repo** and what "didactically structured" means concretely | [mdpi.com/2227-7102/16/5/812](https://www.mdpi.com/2227-7102/16/5/812) |
| A4 | **Improving Hybrid Human-AI Tutoring** (EDM 2026, Zenodo) | Human/AI role division — directly relevant, since the two best results in the field are hybrid | [zenodo.org/records/21039782](https://zenodo.org/records/21039782) |
| A5 | **Rosé et al. 2005 — the NPSG human-tutor study** (CMU KiltHub) | The study CycleTalk was trying to replicate. We only have it secondhand | DOI `10.1184/r1/6469769` |
| A6 | **Koedinger, Corbett & Perfetti — the KLI framework** (CMU KiltHub) | The standard framework for knowledge components; our skill graph should be built on it | [learnlab.org background readings](https://learnlab.org/index.php/background-readings) |

---

## B. Genuinely paywalled — needs PSU library

Request through **PSU Libraries' article delivery / interlibrary loan**. Most arrive as a PDF by
email, often same-day. If the library has a browser extension that surfaces "access via your
institution" links, that handles several of these directly.

| # | Paper | Why we want it | DOI |
|---|---|---|---|
| B1 | ⭐ **VanLehn (2011), "The Relative Effectiveness of Human Tutoring, ITS, and Other Tutoring Systems"**, *Educational Psychologist* | **We cite its numbers constantly and have never read it.** d = 0.76 / 0.79 and the step-vs-substep taxonomy underpin much of our paper | `10.1080/00461520.2011.611369` |
| B2 | ⭐ **Kulik & Fletcher (2016), "Effectiveness of Intelligent Tutoring Systems"**, *Review of Educational Research* | Source of the famous median 0.66 **and** the 0.13 on standardized tests. We have both secondhand from a survey | `10.3102/0034654315581420` |
| B3 | **Rosé, Kumar, Aleven, Robinson & Wu (2006), "CycleTalk: Data Driven Design…"**, *IJAIED* 16(2) | **The fullest account of the closest precedent to this project.** IOS Press blocks everything | `10.3233/irg-2006-16(2)06` |
| B4 | **Ma, Adesope, Nesbit & Liu (2014), ITS meta-analysis** | The largest ITS meta-analysis (107 effect sizes, 73 studies). Secondhand only | search title |
| B5 | **Roscoe & Chi (2007)** — tutor learning, knowledge-building vs knowledge-telling | Why explaining teaches the explainer; relevant to our Socratic design | `10.1007/s11251-007-9034-5` |
| B6 | **Rosé et al. (2004), "CycleTalk: Toward a Dialogue Agent…"**, ITS 2004, LNCS 3220 | The design rationale paper. Springer; **no abstract published anywhere** | `10.1007/978-3-540-30139-4_38` |
| B7 | ⭐ **Midkiff, Litzinger & Evans (2001)**, FIE — the **Thermodynamics Concept Inventory** origin | **Penn State authors.** The origin of the instrument we nearly adopted | IEEE FIE 2001, F2A-3 |
| B8 | **"Assessment in CS50 with AI"** (SIGCSE TS 2025) | How Harvard changed assessment once the tutor existed | `10.1145/3641555.3705061` |
| B9 | **NALA-Assess** (NTU) and **Eva.ai** (Aristotle) | Two more university deployments, both closed | see [institutional landscape](../knowledge/practice/institutional-landscape.md) |

---

## C. The one thing that would let me do Category A myself

**Browserbase has no credit.** The MCP connects and navigates fine, but every `extract` and
`observe` call fails:

```
AI_APICallError: Insufficient Balance
```

**Topping up that account unblocks all six Category A papers without you touching them**, and any
future bot-checked source. It is the highest-leverage single fix on this page.

⚠ **It does not help with Category B** — those are real paywalls, and I won't use your credentials
to get past them. Library request is the right route.

---

## What I still need that isn't a paper

### PSU ME 300 — we have nothing

Every positive result in this literature came from expert hand-work on **one course's content**.
We have a detailed map of Delaware's, Purdue's, ETH's, WPI's and UT Arlington's courses and
**nothing about ours**. Anything here helps:

- Syllabus, schedule, learning objectives
- Problem sets and past exams (⚠ **git-ignored** — do not commit copyrighted material)
- Which textbook, which property tables, which software (EES? CoolProp? Cantera?)
- Enrolment, section sizes, who teaches it, whether there are TAs and office hours
- Canvas setup — is LTI available, what integrations already exist
- Any existing pass/fail or grade-distribution data

### Two literatures I have barely touched

Flagged as standing gaps in `CLAUDE.md`. I can start on both without any access from you — say the
word:

- **Current agent design** — planning, tool use, memory, multi-agent orchestration, routing. Our
  architecture notes come mostly from education papers, which lag this badly.
- **Observability and evaluation for agents** — tracing, eval harnesses, regression testing against
  model upgrades. [CS50's instruction dilution](../knowledge/systems/cs50-duck.md) shows this
  matters operationally and we have almost nothing.

---

## Status

Update this table as things arrive.

| Item | Status |
|---|---|
| A1–A6 | ⬜ blocked on browser or Browserbase credit |
| B1–B9 | ⬜ blocked on PSU library |
| ME 300 materials | ⬜ blocked on Lance |
| Agent design / observability sweep | ⬜ **not blocked — can start any time** |
