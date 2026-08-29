# thermo-tutor

Senior capstone, Penn State — research toward an AI tutor for undergraduate engineering
thermodynamics.

> **Current phase: research and discovery. We are not building the product yet.**
>
> This repo holds literature review, competitive analysis, student interviews, domain
> modeling, and design drafts. Application code does not belong here yet. When we start
> building, that decision gets recorded as an ADR in `docs/` first.

## What we're trying to figure out

Not "can an LLM answer thermo questions" — it can, mostly. The open questions are:

1. What do students *actually* do when they have an AI available during a thermo course,
   as opposed to what we imagine they do?
2. Where do the existing tools (ChatGPT Study Mode, Khanmigo, Mastering Engineering,
   Chegg) genuinely help, and where do they quietly make learning worse?
3. Can a tutor hold a Socratic line when the student doesn't want it to? The literature
   says mostly no. Why, and what would fix it?
4. What would we have to measure to make a defensible claim that our thing worked?

## Layout

| Path | Contents |
|---|---|
| [`knowledge/`](knowledge/) | **The knowledge brain.** Cross-linked wiki of everything we've learned, with sources |
| [`docs/`](docs/) | Working notes — landscape review, key findings, bibliography, open questions |
| [`research/student-interviews/`](research/student-interviews/) | Interview protocol, consent materials, synthesis |
| [`research/competitive-teardown/`](research/competitive-teardown/) | Hands-on evaluations of existing tools |
| [`research/domain/`](research/domain/) | Thermodynamics knowledge model, misconception catalogue |
| [`admin/`](admin/) | IRB, Canvas access, roadmap, meeting notes |

## Start here

**→ [`knowledge/PAPER.md`](knowledge/PAPER.md) — *The State of the Art in AI Tutoring for
College Courses***

Read that first, end to end. It's a full survey of the field — the history from 1970s
intelligent tutoring systems through 2026 university deployments, what the evidence actually
shows, the architecture every serious system converged on, and what's specifically true about
LLMs and thermodynamics. Every claim links to a node with its sources.

Then:

1. [`knowledge/README.md`](knowledge/README.md) — how the wiki is organized and how to add to it
2. [`docs/03-open-questions.md`](docs/03-open-questions.md) — what we don't know, and who's chasing what
3. [`admin/roadmap.md`](admin/roadmap.md) — the semester plan
4. [`admin/irb.md`](admin/irb.md) — the critical path

## The four-sentence version

An LLM already solves thermodynamics better than any student who has sat the exam. That
turns out to be nearly irrelevant, because teaching is a different skill from solving and
the evidence says guardrailed AI tutors prevent harm without producing measurable learning.
The one design that reliably works is expert hand-crafted, course-specific scaffolding —
which means the thermodynamics domain work is the project, not the architecture. And none of
it matters if students stop using the thing in week three, which is what happened to every
large deployment that measured it.

## Hard rules for this repo

**This repository is public.** That has consequences:

- **No student data.** Not names, not IDs, not transcripts, not screenshots containing
  either. Interview synthesis is de-identified before it's committed. Raw notes never
  get committed at all.
- **No copyrighted course materials.** No textbook PDFs, no scans, no instructor slide
  decks, no exam banks, no solution manuals. Reference them by citation.
- **No secrets.** No API keys, Canvas tokens, or `.env` files.
- **Nothing collected from students before IRB determination is in hand.** See
  `admin/irb.md`. This is the project's critical path, not a formality.

If you're unsure whether something can be committed, it can't. Ask first.
