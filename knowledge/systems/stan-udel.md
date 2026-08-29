# Stan — University of Delaware

**Type:** system
**One line:** An LLM-based thermodynamics course assistant deployed in University of
Delaware chemical engineering, Fall 2025.
**Why we care:** **This is our closest competitor.** Same subject, same idea, same year,
one year ahead of us. Understanding exactly how our approach differs is a prerequisite for
claiming any novelty.

> ⚠️ **Highest-priority full read in the entire knowledge base.** Everything below is from
> a skimmed automated extraction of the PDF and may contain errors. Someone needs to read
> the paper properly and correct this node.

## Architecture (as understood)

- **Models:** open-weight models run locally via **Ollama**. Explicitly offline-capable.
- **Retrieval:** RAG over course materials, specifically **Sandler's *Chemical Engineering
  Thermodynamics***.
- **Voice:** Faster-Whisper for speech-to-text, Silero VAD for voice activity detection.
- **Delivery:** a Sphinx documentation site with a Jupyter-based interface.

The local-model choice is the interesting one. It's a **privacy architecture decision** —
nothing leaves the machine — bought at a real cost in model quality. Given what
[LLM capability in thermodynamics](../domain/llm-thermodynamics-capability.md) says about
frontier models struggling on complex thermo, open-weight local models are starting from
further back. Whether that tradeoff paid off is a question the paper may answer and we
should find out. → [compliance](../../admin/irb.md)

## Pedagogy

Socratic prompting with **explicit refusal** to solve problems outright — guiding
questions instead of solutions. Aligned with retrieval-practice and spacing principles.

The refusal-based design is exactly the pattern that
[the discourse research](../concepts/socratic-tutoring.md) suggests students route around.
Whether Stan observed that is one of the most valuable things we could learn from this
paper.

## Reported limitations

- Failure modes on complex problem types
- Constrained model reasoning on multi-step thermodynamic calculations

Both consistent with the benchmark literature — see [ThermoQA](../domain/thermoqa.md),
where Tier 3 full-cycle problems drop as low as 52.7% even for frontier models.

## What we need to find out

- [ ] Which specific open-weight models, and what were the observed accuracy rates?
- [ ] Was there **any tool calling for property data**, or does the model recall values?
      (If not, this is a significant and citable weakness — see
      [property data tools](../domain/property-data-tools.md).)
- [ ] What usage numbers? How many students, how many sessions, what retention?
- [ ] Any learning outcome measurement, or usage/satisfaction only?
- [ ] Did students defect from the Socratic frame, and how did the system respond?
- [ ] Was it integrated with an LMS?
- [ ] **Would the authors talk to us?** Same subject, one year apart. Worth an email.

## How our brief differs (provisionally)

Based on what we know, our project as scoped adds: per-concept mastery tracking over time
([knowledge tracing](../concepts/knowledge-tracing.md)), live course context from Canvas
([LMS integration](../practice/lms-integration.md)), and a pedagogical policy outside the
prompt. Stan appears to be RAG + Socratic prompt + voice.

**This differentiation is provisional and rests on a skimmed reading. Verify before
putting it in any report.**

## Connects to

- [LLM capability in thermodynamics](../domain/llm-thermodynamics-capability.md) — what
  Stan's underlying models can and can't do
- [property data tools](../domain/property-data-tools.md) — the layer Stan may be missing
- [Socratic tutoring](../concepts/socratic-tutoring.md) — the design pattern Stan committed to
- [PeteChat](petechat-purdue.md) — the same "course-specific tutor" pattern, different domain

## Sources

- [Stan: An LLM-based thermodynamics course assistant, arXiv:2603.04657](https://arxiv.org/pdf/2603.04657) `[skimmed]` — PDF cached locally in the session tool-results directory
