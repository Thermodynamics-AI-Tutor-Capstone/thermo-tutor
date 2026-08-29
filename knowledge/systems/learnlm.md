# LearnLM

**Type:** system / model
**One line:** Google DeepMind's family of Gemini models fine-tuned for pedagogy — the only
serious attempt to move teaching ability into the weights rather than the prompt.
**Why we care:** It's the direct test of whether pedagogy is a prompting problem or a
training problem. The answer appears to be: training helps, and not as much as you'd hope.

## The bet

Everyone else encodes pedagogy as instructions ("be Socratic, don't give answers"). LearnLM
trains on **pedagogical instruction following**, so the behavior is in the model.

## Results

**Expert preference over baselines** (expert pedagogical raters, diverse simulated learning
scenarios):

| Compared against | LearnLM preferred by |
|---|---|
| GPT-4o | **+31%** |
| Claude 3.5 Sonnet | **+11%** |
| Gemini 1.5 Pro (its own base model) | **+13%** |

Note the ordering: the gain over its *own base model* was +13%, smaller than the gap to
GPT-4o. Some of what looks like pedagogical training is model-family difference. Worth
holding onto — it caps how much you should expect from pedagogical fine-tuning alone.

**Arena for Learning** (May 2025): **189 educators** role-played realistic learning
scenarios; **206 experts** judged blind, head-to-head, multi-turn comparisons of leading
models. **Gemini 2.5 Pro was preferred in 73.2% of matchups**, ranking first overall.

**Actual learning outcome:** students who received short LearnLM tutoring sessions were
**5.5 percentage points** more likely to solve novel problems on subsequent topics than
students working with human tutors alone.

That last number is the one that matters, and it deserves emphasis in both directions: it
is a **real, positive, published learning effect** — one of very few in this literature —
and it is **small**, and it is measured against *human tutors alone* rather than against
an unassisted control.

## The UK classroom RCT

165 students across five UK secondary schools, LearnLM integrated into chat tutoring on the
Eedi mathematics platform, prompted to adopt a Socratic approach guiding students to find
their own mistakes. Framed by DeepMind as evidence AI tutoring can "safely and effectively"
support students — note that **safety** is the headline claim, consistent with the pattern
in [Bastani](../evidence/bastani-2025-harm.md): the field's defensible claims are about
harm avoidance.

## What this means for us

1. **Model choice is a real but bounded lever.** Preference differences between frontier
   models on pedagogical quality are meaningful but nothing like the
   [3× swing Jill Watson got from architecture](jill-watson.md).
2. **The expert-preference methodology is reusable.** Blind head-to-head multi-turn
   comparisons judged by experts is exactly the
   [CS50 TF-comparison method](cs50-duck.md) at scale, and needs no student data — no IRB
   gate. **This should be how we evaluate our tutor's pedagogy.**
3. If we use Gemini anywhere, LearnLM behavior is available through Gemini. Worth an arm
   in a comparison.

## Open questions

- [ ] Is LearnLM accessible as a distinct API, or folded into Gemini?
- [ ] What did the pedagogical training data look like? Is any of it public?
- [ ] Does the +5.5pp result hold in STEM problem-solving, or is it maths-specific?
- [ ] Has anyone reproduced the arena methodology independently?

## Connects to

- [Socratic tutoring](../concepts/socratic-tutoring.md) — LearnLM's prompted stance
- [MathTutorBench](../evaluation/mathtutorbench.md) — the other pedagogy measurement effort
- [CS50 Duck](cs50-duck.md) — the same expert-comparison evaluation idea, smaller
- [guardrails](../concepts/guardrails.md) — prompt vs. weights as places to put policy

## Sources

- [LearnLM: Improving Gemini for Learning, arXiv:2412.16429](https://arxiv.org/html/2412.16429v1) `[skimmed]` — the preference numbers
- [Evaluating Gemini in an Arena for Learning, arXiv:2505.24477](https://arxiv.org/pdf/2505.24477) `[skimmed]` — the 73.2% arena result
- [AI tutoring can safely and effectively support students: An exploratory RCT in UK classrooms, arXiv:2512.23633](https://arxiv.org/abs/2512.23633) `[found]`
- [DeepMind LearnLM Nov 2025 report](https://storage.googleapis.com/deepmind-media/LearnLM/learnLM_nov25.pdf) `[found]`
