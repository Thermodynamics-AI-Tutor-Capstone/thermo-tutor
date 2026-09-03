# Papers we cannot reach, and exactly what unblocks each

**Drop retrieved PDFs into `course-materials/papers/`** (git-ignored — safe for anything
copyrighted). Tell me when they land and I'll read and integrate them.

Three categories, easiest first. **Category A is free and legal — those papers are already open
access and are blocked only by bot detection.**

---

## What is still missing, after the 2026-09-03 acquisition audit

**113 of 124 paper-type citations are now held** (91%) — see
[`paper-holdings.md`](paper-holdings.md) for the full inventory and the acquisition recipes that
worked. **Eleven remain.** Of those, only these actually matter:

### Needs a browser (open access, bot-blocked)

| # | Paper | Why we want it |
|---|---|---|
| **1** | ⭐⭐ **Porto et al. (2025), PRISMA review of AI-driven ITS in engineering education**, *IEEE Access* — [document/11217866](https://ieeexplore.ieee.org/document/11217866), DOI `10.1109/access.2025.3626473` | **The highest-value missing item.** A systematic map of our exact field — the thing most likely to show what our search is still missing. Gold OA, but **ieeexplore is its only host** (DOAJ lists no mirror) and it returns 502/403 to scripts |
| **2** | **Pardos et al. (2023), "OATutor," CHI 2023** — [dl.acm.org](https://dl.acm.org/doi/10.1145/3544548.3581574) | **CC-BY gold open access** and ACM still 403s the PDF path. Our [OATutor node](../knowledge/systems/oatutor-berkeley.md) is `[skimmed]`; OATutor is the forkable open-source ITS |

⚠ *A note on the first one: the paper that landed in `input/` on 2026-09-03 was a different PRISMA
review — "…for Intelligent IS/IT Project Portfolio Dashboard." Easy mistake; the title above is the
one we need.*

### Needs PSU library (genuinely paywalled)

| # | Paper | Why |
|---|---|---|
| **3** | ⭐ **Biswas, Leelawong, Schwartz & Vye (2005), "Learning by Teaching: A New Agent Paradigm for Educational Software,"** *Applied AI* 19(3–4) | **The only genuinely paywalled paper we have tagged `[read]`** — i.e. we have made claims from it without holding it. Cited in [Betty's Brain](../knowledge/systems/bettys-brain.md). T&F 403s despite bronze OA; the Vanderbilt mirror's WAF rejects requests |
| **4** | **Midkiff, Litzinger & Evans (2001)**, IEEE FIE — the **Penn State** Thermodynamics Concept Inventory origin | Unpaywall confirms `is_oa=false`, no repository copy anywhere. [PSU Pure record exists](https://pure.psu.edu) |
| **5** | **"Assessment in CS50 with AI"** (SIGCSE TS 2025) | Genuinely closed |
| **6** | **Rosé et al. (2006), IJAIED 16(2)** — the fullest CycleTalk account | IOS Press blocks entirely |

### Not actually papers — resolve differently

- **Anderson et al., "Cognitive Tutors: Lessons Learned"** — the source is a **114 KB HTML page**
  that fetches fine and has been read in full. There is simply no PDF at that host. Nothing to
  store; the rule doesn't apply.
- **PhysPort TCI / TTCI-T pages** — instrument pages, not papers. The instruments sit behind
  **PhysPort educator verification**, which is a request Lance should make since
  [our concept-inventory node makes claims about them](../knowledge/evaluation/concept-inventories.md).
- **D'Mello & Graesser AutoTutor affective states** (academia.edu login wall) and
  **Goel & Polepeddi 2018** (closed Routledge chapter) — both `[found]`, low priority, and the
  latter is **superseded by its 2024 successor which we now hold**.

⚠ **One data-quality flag:** **Bloom (1984), the 2-sigma paper, is an image-only JSTOR scan** —
its extracted text is 186 words of cover page, not the article. No OCR tooling is installed
(`tesseract` / `ocrmypdf` absent; `brew install ocrmypdf` would fix it). **Low priority**, because
[VanLehn's primary already establishes that Bloom's 2 sigma is a mastery-learning result rather
than a tutoring one](../knowledge/concepts/vanlehn-2011.md) — we are citing Bloom as a historical
claim that was corrected, not as evidence. Worth OCRing only if someone wants to quote him
directly.

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
| A2, A3, A4, A5, A6 | ✅ **acquired 2026-09-03** — in `course-materials/papers/` |
| **A1 — Porto PRISMA review** | ⬜ **still blocked.** IEEE Xplore returns 403 to scripts. The single highest-value outstanding item |
| B1 VanLehn 2011, B2 Kulik & Fletcher | ✅ **acquired 2026-09-03** — the two we had been citing secondhand |
| B3–B9 | ⬜ blocked on PSU library |
| ME 300 materials | ⬜ blocked on Lance |
| Agent design / observability sweep | ✅ **done 2026-09-03** — [architecture](../knowledge/practice/agent-architecture.md) and [observability](../knowledge/practice/agent-observability.md) |

## Still wanted, added 2026-09-03

- **A1, the Porto review** — unchanged in importance. IEEE blocks scripted access.
- ⭐ **Practitioner observability sources.** Both new agent nodes are built entirely on 2026
  preprints. **OpenTelemetry's GenAI semantic conventions** and the established tracing/eval
  products are not covered at all, and that is a real gap — papers are not where this practice
  actually lives.
- **bioTutor's source repository** — the paper says open-source but does not name the repo.
