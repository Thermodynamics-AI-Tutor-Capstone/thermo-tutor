# Concepts

The ideas and techniques underneath the systems. Read these when you want to know *why* a
design choice is a design choice.

## The empirical anchors

| Node | The thing to know |
|---|---|
| [Bloom's 2 sigma](blooms-two-sigma.md) | The founding claim, and why it's overstated — **it was the 90% mastery threshold, not the tutor** |
| [VanLehn 2011](vanlehn-2011.md) | Human d=0.79; step-based ITS d=0.76. **The mechanism is completion: students learn from solutions they finish themselves. Six of the eight explanations for human tutoring are dead** |

## Pedagogy

| Node | The thing to know |
|---|---|
| [Socratic tutoring](socratic-tutoring.md) | Students route around it. "What do I do next" is the #2 move |
| [Productive failure](productive-failure.md) | Struggle before instruction. Explains why practice gains ≠ learning |
| [Guardrails](guardrails.md) | Prevent harm (−17% → 0). Do **not** produce learning |
| [Engagement decay](engagement-decay.md) | 17% session usage. **Where the field actually loses** |

## Student modeling

| Node | The thing to know |
|---|---|
| [Knowledge components](knowledge-components.md) | The grain problem, and the observations-per-KC budget |
| [Knowledge tracing](knowledge-tracing.md) | BKT/DKT/SAKT. Don't use an LLM for this |
| [Spaced repetition](spaced-repetition.md) | FSRS. The forgetting half. Untested on procedural skills |

## Architecture

| Node | The thing to know |
|---|---|
| [Grounding and verification](grounding-and-verification.md) | **The biggest lever in the field.** 2.5× accuracy from architecture, same model |
| [RAG in education](rag-in-education.md) | Table stakes, and it fails 43% of the time |

## The four-sentence summary

Tutoring effects are real but smaller than advertised, and were largely achieved by
1990s software that made students externalize every step — because **the active ingredient is
the student finishing a solution they generated, not the quality of what the tutor says.** Guardrails on an LLM prevent
active harm and produce no measured gain. Grounding and verification improve outcomes far
more than model choice or pedagogical fine-tuning. And none of it matters if students stop
using the thing in week three.

← back to [the paper](../PAPER.md) · [knowledge brain index](../README.md)
