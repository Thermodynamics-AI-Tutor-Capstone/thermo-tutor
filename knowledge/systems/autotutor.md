# AutoTutor

**Type:** system
**One line:** A natural-language dialogue tutor from the University of Memphis built on
*expectation and misconception-tailored* dialogue — conversational tutoring twenty years
before ChatGPT.
**Why we care:** AutoTutor's EMT design is the template for our misconception catalogue,
and it solved the "what do I say back" problem without a language model.

## The core mechanism: EMT dialogue

Arthur Graesser's group at Memphis's Institute of Intelligent Systems derived AutoTutor's
design from **empirical analysis of ~100 videotaped, transcribed human tutoring sessions**
— middle schoolers in math, college students in research methods.

What they found human tutors actually do:

1. Anticipate a set of **expectations** — specific correct things a good answer contains.
2. Anticipate a set of **misconceptions** — specific wrong things students frequently say.
3. Ask a challenging question, then track the student's answer across multiple turns.
4. Semantically match student contributions against both sets.
5. Respond with dialogue moves chosen by what's been covered and what's been triggered.

That's it. **The pedagogy is a data structure, not a personality.**

## Why this matters more now, not less

An LLM can generate a fluent tutoring response without knowing what the student is
supposed to end up understanding, or which specific wrong idea they're exhibiting.
AutoTutor could not generate fluent text — but it always knew both.

The synthesis nobody has properly built: **EMT's explicit expectation/misconception
structures, with an LLM handling the language.** The LLM does what it's good at
(understanding messy student text, producing natural responses); the EMT structure does
what it's good at (knowing what "done" looks like, and naming the specific error).

This is directly actionable for us. Our
[misconception catalogue](../../research/domain/skill-graph-draft.md) should be built as
an EMT structure — per knowledge component, the expectations and the named misconceptions
— rather than as prose for a prompt.

## Later work: affect

Later AutoTutor versions detected **boredom, confusion, and frustration** from
conversational cues, body language, and facial features, and adapted accordingly. Confusion
in particular is not a bug in this literature — it's often a marker of productive
struggle. → [productive failure](../concepts/productive-failure.md)

## Evidence

Reviewed in "AutoTutor and Family: A Review of 17 Years of Natural Language Tutoring" and
"Conversations with AutoTutor Help Students Learn" (IJAIED). Effect sizes should be pulled
from those directly rather than trusted from summaries.

## Open questions

- [ ] What effect sizes, in which domains? (Needed to place AutoTutor against
      [VanLehn's](../concepts/vanlehn-2011.md) d = 0.76 step-based figure.)
- [ ] How much authoring per topic? EMT structures are hand-built — what did that cost?
- [ ] Has anyone built EMT-structured prompting for an LLM tutor? **Search harder for
      this; if not, it's an opening.**
- [ ] Are any of the expectation/misconception corpora published and reusable?

## Connects to

- [Socratic tutoring](../concepts/socratic-tutoring.md) — EMT is the disciplined
  alternative to "be Socratic"
- [knowledge components](../concepts/knowledge-components.md) — expectations map onto KCs
- [our skill graph and misconception catalogue](../../research/domain/skill-graph-draft.md)
- [productive failure](../concepts/productive-failure.md) — confusion as signal

## Sources

- [Graesser et al., "AutoTutor and Family: A Review of 17 Years of Natural Language Tutoring," IJAIED](https://link.springer.com/article/10.1007/s40593-014-0029-5) `[skimmed]`
- ["Conversations with AutoTutor Help Students Learn," IJAIED](https://link.springer.com/article/10.1007/s40593-015-0086-4) `[skimmed]`
- [AutoTutor: An ITS With Mixed-Initiative Dialogue (chapter)](https://bpb-us-w2.wpmucdn.com/blogs.memphis.edu/dist/d/2954/files/2019/10/AutoTutor-An-intelligent-tutoring-system-with-mixed-initiative-dialogue.pdf) `[found]`
- [AutoTutor detects and responds to learners' affective and cognitive states](https://www.academia.edu/568630/AutoTutor_detects_and_responds_to_learners_affective_and_cognitive_states) `[found]`
