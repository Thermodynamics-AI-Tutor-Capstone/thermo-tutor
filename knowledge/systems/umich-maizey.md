# U-M Maizey — University of Michigan

**Type:** system
**One line:** Michigan's university-built, closed generative AI platform — faculty create
course-specific tutors that appear in a Canvas side panel.
**Why we care:** The strongest *institutional-scale* numbers in this literature, and the
closest model for what a Penn State deployment could look like.

## What it is

Part of U-M's decision to build its own closed generative AI tools rather than route
students to commercial products — a data-governance choice as much as a technical one.
Maizey lets faculty and staff build retrieval-grounded assistants over their own content.

## Scale

- **3,500+ Maizey instances** in production across academic departments and operational
  offices (procurement, HR)
- **~15,000 users/day** across U-M's AI tools
- Canvas integration: when enabled in a course, students reach the tutor from the Canvas
  side panel

## ⚠ The results — and one number we should stop repeating

> **Corrected 2026-08-31.** This node previously reported a "5–9% grade improvement" as a
> headline institutional result. **Two independent searches failed to locate the underlying
> study, its methodology, or any control for selection effects.**

**The 5–9% grade claim: do not use it.** It circulates widely in trade coverage of a
1,000-student class, but there is no locatable study behind it. Students who opt into an
optional tutoring tool differ systematically from those who don't
([equity](../practice/equity.md)), and without the methodology we cannot even tell whether
that was addressed. This is precisely the kind of unvalidated headline figure that should not
enter a capstone report — and a reviewer who chases the citation will find what we found.

**The 94% figure is different and more defensible**: a head-to-head answer-quality comparison
against course staff across qualitative and quantitative questions — closer to the
[CS50 TF-comparison method](cs50-duck.md). Still worth locating the methodology before citing.

## The architecture, and it is our design

Two details make Maizey the closest institutional precedent for what we are proposing:

- It **"is based on an AI framework called retrieval-augmented generation (RAG)"** and indexes
  **Dropbox, Google Drive, Canvas, and public web links simultaneously**, with **scheduled
  reindexing**.
- Per EdTech Magazine: *"Faculty can integrate Maizey with the university's learning management
  system to set up **course-specific AI tutoring in just a few minutes**."*

**A faculty member at Michigan can stand up a course-specific RAG tutor over their Canvas
content in minutes.** That is roughly the product our project describes, already deployed at a
peer institution — which sharpens rather than removes our contribution, but should change how
we position it. Our differentiators have to be the layers Maizey does *not* have: a
[student model](../concepts/knowledge-tracing.md),
[property-data tools](../domain/property-data-tools.md), a
[pedagogical policy outside the prompt](../concepts/guardrails.md), and evaluation.

## ⭐ The API-access precedent — this answers our blocking question

Michigan publishes the rule explicitly:

> *"**Students cannot directly create U-M GPT Toolkit API keys** because access to the
> self-service portal is restricted to faculty and staff, and API key creation requires an
> approved U-M Shortcode due to associated costs. **Faculty or staff may sponsor eligible
> student employees by creating and managing API keys on their behalf.**"*

This is the documented norm at the peer institution whose stack Penn State's most closely
mirrors. **Plan on needing a faculty sponsor who holds the account and the cost centre.** It
converts our biggest open question from a blocker into a design constraint — we still confirm
the PSU specifics, but we should expect this answer and plan the sponsor conversation around
it. → [PSU AI landscape](../practice/psu-ai-landscape.md)

## Cost signals — useful, and not a price sheet

One procurement workload reportedly ran **~$65/year** on Maizey against a prior system costing
**3 FTEs and "a few hundred thousand dollars a year,"** with accuracy going from ~30% to
"nearly 100%." Pricing is **usage-based, not flat**, and Maizey is listed as **no-cost at U-M
through 30 June 2027**.

Treat $65 as a metered bill for one narrow workload, not as a rate card. It does corroborate
the general finding that [cost is not our constraint](../practice/cost-economics.md).

## Why this is our institutional template

Michigan and Penn State are structurally similar: large public research universities,
Canvas, central IT with an appetite for building. PSU already has **AI Studio** offering
Claude, Gemini, and ChatGPT to all students — see
[PSU AI landscape](../practice/psu-ai-landscape.md). Maizey is roughly what the mature
version of that looks like.

## Open questions

- [ ] **Can anyone locate the 1,000-student study at all?** Two searches failed. Until someone
      finds it, the 5–9% figure is unusable.
- [ ] How was the 94% effectiveness comparison actually run — who judged, how many items?
- [ ] Retention: do students keep using Maizey through the term?
- [ ] What is the underlying model, and is it swappable?
- [ ] How did they get Canvas side-panel integration approved? **Ask PSU IT the same
      question** → [LMS integration](../practice/lms-integration.md)

## Connects to

- [Cogniti](cogniti-sydney.md) — the same faculty-builds-it model, arrived at independently
- [PSU AI landscape](../practice/psu-ai-landscape.md) — our institution's version
- [LMS integration](../practice/lms-integration.md) — the Canvas side panel is the target
- [equity](../practice/equity.md) — why the 5–9% number needs a self-selection caveat

## Sources

- [EDUCAUSE Review, "How (and Why) the University of Michigan Built Its Own Closed Generative AI Tools" (Feb 2024)](https://er.educause.edu/articles/2024/2/how-and-why-the-university-of-michigan-built-its-own-closed-generative-ai-tools) `[found]` — **hard-blocked by Cloudflare to every automated route.** Opens fine in a browser, or via [this Wayback snapshot](https://web.archive.org/web/20251228083017/https://er.educause.edu/articles/2024/2/how-and-why-the-university-of-michigan-built-its-own-closed-generative-ai-tools). **Nothing in this node is sourced from it.**
- [U-M ITS — AI FAQ](https://its.umich.edu/computing/ai/faq) `[read]` — **the API key sponsorship rule**
- [EdTech Magazine, "How Three Universities Developed Their Chatbots" (May 2025)](https://edtechmagazine.com/higher/article/2025/05/how-three-universities-developed-their-chatbots) `[skimmed]` — scale and grade figures
- [Michigan Ross, "U-M GPT's Maizey tool guides students to success"](https://michiganross.umich.edu/news/u-m-gpt-s-maizey-tool-guides-students-success) `[found]`
- [U-M ITS AI release notes](https://its.umich.edu/computing/ai/release-notes) `[found]`
