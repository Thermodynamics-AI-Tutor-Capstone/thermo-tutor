# GPThermo — Worcester Polytechnic Institute

**Type:** system (lead)
**One line:** An in-house generative-AI thermodynamics tutor built at WPI and presented at ASEE
2025 — the third university-built thermodynamics tutor we know of, and the one we know least
about.
**Why we care:** It is the closest institutional peer to this project that exists. A US
engineering school built the thing we are proposing, for the same course, and published it.

> ⚠ **Verification: `[inaccessible]` — metadata only, 2026-09-01. We have not read a word of
> the paper.** Everything below the line is bibliographic fact; there are no claims about the
> system itself because we have none.

## What is actually established

| | |
|---|---|
| Title | *GPThermo: An In-House Generative Artificial Intelligence Tutor for Thermodynamics* |
| Authors | **H. L. Brown, Alireza Ebadi** |
| Institution | **Worcester Polytechnic Institute** |
| Venue | **ASEE Annual Conference, 2025** (conference paper) |
| DOI | [`10.18260/1-2--56669`](https://doi.org/10.18260/1-2--56669) |
| Citations | 0, as of this writing |

**"In-house" is the load-bearing word in the title** — it signals the same institutional posture
as [Stan](stan-udel.md), [PeteChat](petechat-purdue.md) and [Ethel](ethel-eth.md): built by the
department for its own course, rather than bought.

## ⚠ Why we could not read it

ASEE's PEER repository (`peer.asee.org`) sits behind a **Cloudflare challenge** that blocks
scripted access; the DOI resolves there and stops. Semantic Scholar holds **no abstract** and no
open PDF, and OpenAlex reports `oa_status: closed`. So unlike VanLehn or Kulik & Fletcher, this is
not a paywall — it is a bot check, and **a human with a browser can very likely just open it.**

**This is the cheapest high-value retrieval on our list.** Someone should open
[peer.asee.org/56669](https://peer.asee.org/56669) in a browser and save the PDF.
→ [access recipes](../README.md)

## What we need from it, in priority order

1. **Does it tutor, or does it answer?** Where does it sit on
   [Stan's six-level scale](stan-udel.md)? That single fact decides whether our space is still
   open.
2. **Does it call a property library** ([CoolProp or equivalent](../domain/property-data-tools.md)),
   or does it let the model do thermodynamic arithmetic?
3. **Any evaluation at all** — deployment size, learning outcomes, usage. ASEE papers frequently
   have none, which would itself be informative.
4. **How it handles T–s and P–v diagrams**, the failure mode nothing has solved.
   → [diagram reading](../domain/diagram-reading.md)
5. **Whether they published anything reusable** — prompts, a misconception catalogue, an
   evaluation set.

## Open questions

- [ ] **Read the paper.** See above; it needs a browser, not another script.
- [ ] Is there a follow-up? Zero citations and a 2025 conference date means any sequel would be
      2026 and very recent. Worth re-checking OpenAlex periodically.
- [ ] Are Brown and Ebadi worth contacting? A peer team one year ahead of us, at a comparable
      institution, is a better source than most papers — and ASEE is a community where that kind
      of email is normal. → [roadmap](../../admin/roadmap.md)
- [ ] **How many more of these are there?** GPThermo did not appear in any earlier sweep and
      surfaced only through a title search on OpenAlex. ASEE and ASME proceedings are largely
      invisible to arXiv-shaped searching, and that is exactly where engineering-education work
      on our topic lives. **The competitive landscape is probably wider than this base reflects.**

## Connects to

- [Stan](stan-udel.md) — the other US university thermodynamics assistant, read in full
- [Ethel](ethel-eth.md) — ETH's, which does grading as well as chat
- [PeteChat](petechat-purdue.md) — Purdue's, in a different engineering course
- [Institutional landscape](../practice/institutional-landscape.md)
- [Competitive teardown method](../../research/competitive-teardown/README.md)

## Sources

- Brown, H. L. & Ebadi, A. (2025). "GPThermo: An In-House Generative Artificial Intelligence Tutor for Thermodynamics." *ASEE Annual Conference*. [DOI 10.18260/1-2--56669](https://doi.org/10.18260/1-2--56669) · [peer.asee.org/56669](https://peer.asee.org/56669) `[inaccessible — Cloudflare challenge, not a paywall; retrievable by hand]`
