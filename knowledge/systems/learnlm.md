# LearnLM

**Type:** system / model
**One line:** Google DeepMind's family of Gemini models fine-tuned for pedagogy — the only
serious attempt to move teaching ability into the weights rather than the prompt.
**Why we care:** It's the direct test of whether pedagogy is a prompting problem or a
training problem. The answer appears to be: training helps, and not as much as you'd hope.

> **Verification: `[read]` — full text (LearnLM: Improving Gemini for Learning,
> arXiv:2412.16429), 2026-08-31. The framing in this node was subtly wrong — corrected below.**

## The bet — and it is not "pedagogy in the weights"

The obvious reading is "fine-tune a model to be Socratic." That is **not** what they did, and
the distinction matters.

Their framing is **pedagogical instruction following**: train the model to *follow
pedagogical system instructions well*, rather than to embody one fixed pedagogy. Each
training conversation is seeded with a **different** pedagogical System Instruction, sampled
from the kinds of instruction developers actually write when building tutors. The model
learns to obey the pedagogy it is given.

**This preserves developer control instead of removing it** — which is exactly what we would
want, since our pedagogy needs to be decided by our
[policy layer](../concepts/guardrails.md), not by a model vendor.

Method: SFT plus **RLHF**. Their finding on the two: *"While SFT seems to improve pedagogical
instruction following somewhat, RL is significantly more effective, as preference judgements
often contain subtle distinctions in how instructions are interpreted."*

**Their five-category rubric** is a usable evaluation taxonomy in its own right:
inspires **active learning** · manages **cognitive load** · deepens **metacognition** ·
stimulates **curiosity** · **adapts to the learner** (goals, needs, affect).

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

**The evaluation behind those numbers is the largest of its kind in this literature**, and worth
knowing in detail because it sets the bar for what a credible tutoring evaluation looks like:

| | |
|---|---|
| Pedagogy experts **role-playing learners** | **186** |
| Separate pedagogy experts **rating** | **248** |
| Conversations collected | **2,360** |
| Learner + model messages | **58,459** |
| Expert assessments | **10,192** (≈3 independent reviews per conversation pair) |
| Scenarios | **49**, across diverse subjects |
| Rubric | **29 items**, 7-point Likert, anchored at *"as good as a very good human tutor"* |

Rater qualification was specified: *"advanced academic degrees and two or more years of experience
as a tutor."* Rubric categories covered cognitive load, active learning, metacognition, curiosity
stimulation, adaptivity and overall quality. **LearnLM ranked highest in every category.**

**How it was trained** — note this is *not* a separate pedagogy model: *"we mix our data directly
with Gemini's SFT, RM, and RL stages."* Co-training, not a fine-tune on top. Each training
conversation begins with a **different System Instruction describing the pedagogical behaviour**,
which is the whole point of the "instruction following" reframing — it *"avoids committing our
models to any particular definition of pedagogy, and instead allows teachers or developers to
specify desired model behavior."*

## ⭐⭐ Where LearnLM *lost* — the Socratic tax, measured

This is the most useful part of the paper for us, and it is buried in a qualitative table. Among
the explanations experts gave for preferring a **competitor**:

| Theme | Share of non-LearnLM preference explanations |
|---|---|
| **Conversation style** | **36.3%** — LearnLM described as **"patronizing"**; competitors seemed **"warmer"** |
| Info amount | 25% — competitors more succinct or more comprehensive |
| Clarity | 20% — competitors' explanations were clearer |

And directly: participants reported **weaker experiences than GPT-4o in "stimulating their
interest" and "perceived warmth."**

**A model tuned to guide rather than tell is experienced as condescending.** That is the cost of
the Socratic stance, stated by pedagogy experts who were predisposed to like it, and it lands on
exactly the axis that determines whether students keep using a voluntary tool.
[Students already route around Socratic design](../concepts/socratic-tutoring.md);
[PeteChat logged 0% hint uptake](petechat-purdue.md); this says *why* the pull is so weak.

**Design consequence:** warmth and concision are not decorations to add at the end. They are in
tension with the pedagogy, they were measured to be in tension, and if we do not deliberately
budget for them we will ship the patronizing version.
→ [engagement decay](../concepts/engagement-decay.md)

⚠ **And their own headline limitation:** *"it is unclear how well the results translate to
improvements in learning outcomes."* All of the above is **intrinsic** — expert judgement of
conversation quality — not learning. They also flag that every model compared has since been
updated, so *"our results only reflect a reasonably fair comparison at a specific moment."*

**Arena for Learning** (May 2025, arXiv:2505.24477, read in full 2026-09-01): **189 educators**
role-played realistic learning scenarios; **206 experts** judged blind, head-to-head, multi-turn
comparisons. **Gemini 2.5 Pro was preferred in 73.2% of matchups**, ranking first overall.

The design fixes a real flaw in Chatbot-Arena-style evaluation: those arenas *"require sending
identical inputs to each model… on every turn,"* which makes them structurally unable to test
tutoring, where the whole point is that a good tutor **steers the conversation somewhere different
from where a bad one would.** Here each model shepherds its own conversation, and experts judge the
resulting trajectories. **If we ever benchmark tutoring, this is the design to copy.**

Per-principle adherence (7-point scale, −3.0 to +3.0, reported as a percentage of the maximum):
**active learning 84.4%**, curiosity 82.9%, metacognition 82.8%, **cognitive load 82.1%**
(= +2.0 raw), adapting to student needs 82.0%. Gemini 2.5 Pro led on every one.

Head-to-head win rates, excluding ties: **71.3% vs Claude 3.7 Sonnet, 74.2% vs OpenAI o3, 81.8%
vs GPT-4o.** Rankings computed as **Elo** ratings via a Bradley-Terry model, the same machinery
as Chatbot Arena.

### ⭐ The result buried in the ranking order

Final pedagogy ranking: **Gemini 2.5 Pro, then ChatGPT-4o, then Claude 3.7 Sonnet and o3 tied,
then GPT-4o last.**

**ChatGPT-4o placed second. GPT-4o placed fifth. That is the same model.** The difference is the
product wrapper — the system prompt, the interface, whatever OpenAI layers on top of the raw API.

**A product layer moved one model from last place to second on pedagogical quality.** That is the
single cleanest piece of evidence in this knowledge base that *what you build around the model
matters as much as which model you pick* — and it comes from an evaluation run by a competitor
with no incentive to make the point.
→ [the convergent architecture](../PAPER.md), [guardrails](../concepts/guardrails.md)

⚠ **Two caveats.** This is **Google evaluating Google's own model**, and while the protocol is
blind and the raters independent, the scenario bank and rubric are Google's. And their own stated
limits: the expense of expert evaluation, *"the boundaries of its current bank of learning
scenarios,"* and that arena conversations *"represent single snapshots of a longer learning
journey that unfolds over days, weeks, or even months."* They close by naming the open question
themselves — *"do these pedagogical capabilities translate to concretely better learning outcomes
for students?"* — and calling for RCTs.

**Actual learning outcome:** students supported by LearnLM were **5.5 percentage points** more
likely to solve novel problems on subsequent topics (**66.2%** vs **60.7%**) than students working
with human tutors alone.

⚠⚠ **But read the design before quoting that number — LearnLM never spoke to a student
unsupervised.** In the UK RCT (arXiv:2512.23633, read in full 2026-09-01), **17 expert human tutors
supervised it**, with the remit to *"revise each message it drafted until they would be satisfied
sending it themselves."* Every message was approved, edited or rewritten by a human before it
reached a student.

**So the comparison is human tutor + AI drafts versus human tutor alone.** That is
**[Tutor CoPilot's design](tutor-copilot.md)**, not an autonomous tutor — and it means the two
strongest positive results in this entire knowledge base are **both hybrid**:

| Study | Design | Effect |
|---|---|---|
| [Tutor CoPilot](tutor-copilot.md) | AI coaches the human tutor | **+4 p.p.**, +9 p.p. for weakest tutors |
| **LearnLM UK RCT** | AI drafts, human approves | **+5.5 p.p.** (66.2% vs 60.7%) |

**Nobody has a comparably strong result for an AI tutoring a student alone.**
→ [what this means for our project](../PAPER.md)

That last number is the one that matters, and it deserves emphasis in both directions: it
is a **real, positive, published learning effect** — one of very few in this literature —
and it is **small**, and it is measured against *human tutors alone* rather than against
an unassisted control.

## The UK classroom RCT — read in full

**N = 165 students, five UK secondary schools, Eedi mathematics platform, N = 17 supervising
tutors.** Three-way randomisation: a **static pre-written hint**, an **interactive human tutor**,
or **supervised LearnLM**. Support was triggered whenever a student got the first question of a
study unit wrong, and the same question was re-presented immediately afterwards.

**Draft acceptance — the number that matters for a hybrid design:**

- **74.4% of 3,617 drafted messages accepted with no edits at all**; 76.4% with zero or minimal
  edits (one or two characters — *"virtually always… a tutor deleting or changing an emoji"*).
- Of the **926** edited or rewritten, the **median intervention altered 59 characters** — a few
  words.
- ⭐ **Post-hoc systematic review of the whole corpus found zero instances of harmful or risky
  content and five factual errors: 0.1% of 3,617 messages.**

⚠ **Do not carry that 0.1% error rate into our domain.** This is secondary-school mathematics.
[Thermodynamics property lookups fail at 44–63% for R-134a](../domain/thermoqa.md) and
[students name table values as the failure they see](../evidence/student-ai-perceptions-2025.md).
The safety result is real and domain-bound.

**On interaction format:** *"interactive support with a human tutor proved far more effective for
this kind of immediate course-correction"* than a static pre-written hint. Chat beat canned hints —
which is the one place this literature clearly favours conversation over
[pre-authored hint ladders](../concepts/productive-failure.md).

**Tutors reported learning from the model** — several said they picked up new pedagogical
practices from LearnLM's Socratic drafts. That is an unmeasured but real second-order benefit of
the hybrid design, and it is the same claim [Tutor CoPilot](tutor-copilot.md) makes.

### Earlier summary

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

- [ ] ⚠ **A direct contradiction worth resolving.** LearnLM's entire premise is *pedagogical
      instruction following* — it is trained so that a system instruction shapes its teaching.
      But [MathTutorBench](../evaluation/mathtutorbench.md) tested exactly that and found LearnLM
      among the models showing *"decreased or similar performance"* when given pedagogical
      instructions in the prompt, while GPT-4o *gained* significantly. Either the benchmark's
      instructions differ from the ones LearnLM was trained on, or the capability does not
      generalise past the training distribution. **This is a cheap, publishable experiment**:
      take LearnLM, vary the system instruction across pedagogies, and measure whether behaviour
      actually moves.

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

- [LearnLM: Improving Gemini for Learning, arXiv:2412.16429](https://arxiv.org/html/2412.16429v1) `[read]` — the preference numbers
- [LearnLM Team, Google, "Evaluating Gemini in an Arena for Learning," arXiv:2505.24477](https://arxiv.org/pdf/2505.24477) `[read — full text, 26 pp., 2026-09-01]`
- [LearnLM Team (Google) & Eedi, "AI tutoring can safely and effectively support students: An exploratory RCT in UK classrooms," arXiv:2512.23633](https://arxiv.org/pdf/2512.23633) `[read — full text, 31 pp., 2026-09-01]`
- [DeepMind LearnLM Nov 2025 report](https://storage.googleapis.com/deepmind-media/LearnLM/learnLM_nov25.pdf) `[found]`
