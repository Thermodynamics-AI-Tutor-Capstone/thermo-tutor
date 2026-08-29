# Betty's Brain

**Type:** system
**One line:** A Vanderbilt "learning by teaching" environment where students teach a
software agent named Betty, then watch her fail their quizzes.
**Why we care:** It's the most under-exploited idea in this entire knowledge base. The LLM
era has almost entirely ignored learning-by-teaching, and an LLM is unusually well-suited
to play the student.

## What it is

Developed by **Gautam Biswas** and Vanderbilt's Teachable Agents Group, for middle
schoolers learning causal relationships in biological systems.

The inversion: **the student doesn't get taught. The student teaches.**

Students build a causal concept map — this increases that, which decreases the other —
which *is* Betty's knowledge. Betty then reasons over that map to answer questions and
take quizzes. When Betty gets something wrong, the student sees that their own
understanding was wrong, in a form they can inspect and repair.

## Why the mechanism works

Three things happen at once, all well-supported in learning science:

1. **Externalization.** To teach it, you must state it explicitly — which surfaces gaps
   that reading and nodding conceal.
2. **The protégé effect.** Students work harder for their agent than for themselves.
   Betty failing is a problem *the student caused and can fix*, not a judgment on the
   student.
3. **Metacognition.** Betty's Brain layers self-regulated-learning feedback on top,
   coaching students on how they're going about learning.

An experiment in a 5th grade science classroom compared three conditions: taught **by** an
agent, baseline learning-by-teaching, and learning-by-teaching **plus** self-regulated
learning feedback.

## Why nobody has done this with an LLM — and why we could

Pre-LLM teachable agents needed the student to express knowledge in a *formal*
representation, because that was the only thing the agent could reason over. Concept maps
are a constrained, laborious interface. That ceiling is gone: an LLM can be instructed to
adopt a specified — possibly wrong — model of thermodynamics and reason from it, taking
input in natural language.

**A thermodynamics application, concretely:** the student explains to the agent why the
entropy of the universe increases in an irreversible process. The agent adopts exactly the
understanding conveyed — misconceptions and all — and attempts a problem with it. The
student watches their own misconception produce a wrong answer.

That is a direct attack on the field's central failure mode. A student demanding "just
give me the answer" is asking to be a passive recipient. There is no answer to be given
when you are the teacher. The [crutch effect](../evidence/bastani-2025-harm.md) has nothing
to grab.

It also aligns with the [doer effect](cognitive-tutor.md): the student produces, the system
responds.

**Flagging this as the most interesting unexplored design direction we found.** It should
be one of the Phase 3 [rough drafts](../../admin/roadmap.md) — and it is testable as a
Wizard-of-Oz prototype with no engineering at all.

## Open questions

- [ ] Effect sizes from the Betty's Brain studies
- [ ] Does learning-by-teaching hold for university engineering, or is the evidence
      K-12-bound? **Check before betting on it.**
- [ ] Has anyone built an LLM teachable agent? Search harder — this seems too obvious to
      be untried.
- [ ] How do you stop the LLM from silently correcting the student's flawed model?
      (This is the hard engineering problem: models are trained to be right.)

## Connects to

- [productive failure](../concepts/productive-failure.md) — Betty failing is the point
- [Bastani 2025](../evidence/bastani-2025-harm.md) — the crutch effect this design defeats
- [Cognitive Tutor](cognitive-tutor.md) — the doer effect
- [our roadmap](../../admin/roadmap.md) — a Phase 3 prototype candidate

## Sources

- [Biswas et al., "From Design to Implementation to Practice a Learning by Teaching System: Betty's Brain," IJAIED](https://link.springer.com/article/10.1007/s40593-015-0057-9) `[skimmed]`
- [Designing Learning by Teaching Agents: The Betty's Brain System](https://dl.acm.org/doi/10.5555/1454278.1454280) `[found]`
- ["Learning by Teaching: A New Agent Paradigm for Educational Software"](https://www.tandfonline.com/doi/full/10.1080/08839510590910200) `[found]`
- [Engagement patterns of middle school students with AI teachable agents in mathematics learning, *Scientific Reports* (2025)](https://www.nature.com/articles/s41598-025-24841-8) `[found]` — recent, worth reading
