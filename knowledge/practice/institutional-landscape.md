# Institutional Landscape

**Type:** practice
**One line:** Roughly 74% of US institutions have at least one production AI deployment
touching students directly. The field has moved from pilots to infrastructure.
**Why we care:** It sets what "novel" means for our project, and it means the interesting
question is no longer *whether* to deploy AI but what to deploy and how to know if it worked.

## The state of play (2026)

- **~74%** of US institutions have at least one production AI deployment touching students
  directly (EDUCAUSE 2026 reporting)
- **88%** of students and **77%** of faculty use AI → [faculty adoption](faculty-adoption.md)
- [CS50's Duck](../systems/cs50-duck.md) answered **800,000+** student questions in 2024–25
- [Jill Watson](../systems/jill-watson.md) has expanded into a multi-course platform
- [U-M Maizey](../systems/umich-maizey.md): **3,500+** instances, **~15,000** users/day

## The three institutional strategies

| Strategy | Exemplar | The bet |
|---|---|---|
| **Buy access for everyone** | [ASU + OpenAI](../systems/asu-openai.md) | Distribution over design. Hand out frontier models, see what emerges |
| **Build a platform** | [U-M Maizey](../systems/umich-maizey.md), [Cogniti](../systems/cogniti-sydney.md) | Governance and control. Faculty build their own agents on institution-owned infrastructure |
| **Build one great course tutor** | [CS50 Duck](../systems/cs50-duck.md), [PeteChat](../systems/petechat-purdue.md), [Stan](../systems/stan-udel.md) | Depth over breadth. One course, done properly |

[Penn State appears to be running strategies 1 and 2 simultaneously](psu-ai-landscape.md):
AI Studio provides broad access to Claude/ChatGPT/Gemini, and the AI Center of Excellence
funds faculty-led instructional projects.

**Our project is strategy 3, inside an institution running 1 and 2.** That's a coherent
position — the depth play only makes sense where breadth already exists — and it's worth
stating that way to a sponsor or a review panel.

## What's conspicuously missing

**Learning outcome data.**

Three years of institutional AI deployment coverage reports: access numbers, project counts,
user counts, satisfaction scores, and grade correlations. Almost no controlled evidence.

The exceptions are few and mostly *not* institutional deployments:
[Kestin](../evidence/kestin-2025-rct.md) (one course, n=194),
[Bastani](../evidence/bastani-2025-harm.md) (high school, found harm),
[Tutor CoPilot](../systems/tutor-copilot.md) (K-12, hybrid),
[Khanmigo](../evidence/khanmigo-engagement-2026.md) (found engagement collapse).

**The institutions with the largest deployments have published the least about whether they
work.** That absence is a finding, and it defines where a rigorous small study is worth more
than another large deployment.

## What this means for "novel"

Building a course-specific AI tutor is **not novel in 2026.** Dozens exist. If our
contribution is framed as "we built an AI tutor for thermodynamics," a reviewer who knows this
landscape will ask what [Stan](../systems/stan-udel.md) didn't already do.

What remains genuinely open:
- **Rigorous evaluation of a course tutor** — the thing the big deployments skipped
- **Pedagogy measurement in engineering** → [MathTutorBench](../evaluation/mathtutorbench.md)
- **Honest voluntary-engagement reporting** → [engagement decay](../concepts/engagement-decay.md)
- **The [diagram problem](../domain/diagram-reading.md)** in engineering
- **Teaching [assumption identification](../domain/thermo-problem-benchmark.md)** — the skill
  every model lacks

**The research is the contribution, not the artifact.** For a capstone, that's good news:
rigor is cheaper than scale.

## Open questions

- [ ] Read the EDUCAUSE 2026 report properly — the 74% figure came via secondary coverage
- [ ] How many of those deployments are course tutors vs. chatbots vs. admin tools?
- [ ] Is anyone publishing negative institutional results? (If not, the record is
      publication-biased and the true picture is worse than it looks.)
- [ ] What are peer Big Ten institutions doing?

## Connects to

- [PSU AI landscape](psu-ai-landscape.md) — our institution's position
- [ASU](../systems/asu-openai.md) / [Maizey](../systems/umich-maizey.md) / [Cogniti](../systems/cogniti-sydney.md) — the three strategies
- [faculty adoption](faculty-adoption.md) — the human constraint
- [the paper, §VII](../PAPER.md) — the open problems in full

## Sources

- EDUCAUSE 2026 reporting, via [Perspective AI, "Where Universities Actually Deploy AI in 2026"](https://getperspective.ai/blog/ai-applications-in-education-where-universities-deploy-ai-in-2026) `[skimmed]` — **secondary source; find the EDUCAUSE original**
- [aiandacademia, "Higher education and AI in late 2025/early 2026"](https://aiandacademia.substack.com/p/higher-education-and-ai-in-late-2025early) `[found]`
- [Digital Education Council Global Survey 2026](https://www.digitaleducationcouncil.com/resource-library-items/ai-in-higher-education-global-survey-2026) `[skimmed]`
