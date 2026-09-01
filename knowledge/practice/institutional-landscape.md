# Institutional Landscape

**Type:** practice
**One line:** Roughly 74% of US institutions have at least one production AI deployment
touching students directly. The field has moved from pilots to infrastructure.
**Why we care:** It sets what "novel" means for our project, and it means the interesting
question is no longer *whether* to deploy AI but what to deploy and how to know if it worked.

## The state of play (2026)

- **37%** of institutions provide institution-wide chatbot licences; **14%** have built their
  own (EDUCAUSE). **57%** of leaders call AI a strategic priority, up from 49%.
- **~74%** of US institutions have at least one production AI deployment touching students
  directly (EDUCAUSE 2026 reporting, via secondary coverage)
- **88%** of students and **77%** of faculty use AI → [faculty adoption](faculty-adoption.md)
- But penetration into actual teaching is thin: only **15%** of students say AI is integrated
  into many of their courses, only **5%** say it has transformed how they learn, and **24%**
  report **no clear learning value**. **43% of US/Canada students support an institution-wide
  AI ban.**
- [CS50's Duck](../systems/cs50-duck.md) answered **800,000+** student questions in 2024–25
- [Jill Watson](../systems/jill-watson.md) has expanded into a multi-course platform
- [U-M Maizey](../systems/umich-maizey.md): **3,500+** instances, **~15,000** users/day

## The three institutional strategies

| Strategy | Exemplar | The bet |
|---|---|---|
| **Buy access for everyone** | [ASU + OpenAI](../systems/asu-openai.md) | Distribution over design. Hand out frontier models, see what emerges |
| **Build a platform** | [U-M Maizey](../systems/umich-maizey.md), [Cogniti](../systems/cogniti-sydney.md) | Governance and control. Faculty build their own agents on institution-owned infrastructure |
| **Build one great course tutor** | [CS50 Duck](../systems/cs50-duck.md), [PeteChat](../systems/petechat-purdue.md), [Stan](../systems/stan-udel.md) | Depth over breadth. One course, done properly |

**A fourth is emerging: the course-tutor-as-a-feature.** [U-M Maizey](../systems/umich-maizey.md)
lets faculty *"set up course-specific AI tutoring in just a few minutes"* over Canvas content,
and **UC Irvine's ZotGPT ClassChat** (launched January 2025) *"allows instructors to incorporate
course materials with LLMs for students at much higher detail than a standard chatbot."* UCI
also offers API access to researchers.

**This is the most important competitive fact in this node.** What our project proposes as a
build is increasingly a *checkbox* at peer institutions. That does not kill the project — those
platforms are RAG-over-course-content with no student model, no domain tools, no pedagogical
policy layer, and no evaluation — but it does mean **"we built a course-specific AI tutor" is
not a contribution in 2026**, and our framing has to be about the layers above that.

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

## More university systems, found but not yet read

A sweep for named institutional deployments (2026) turned up these. None is read; all are recorded
so the next sweep does not rediscover them.

| System | Institution | Status |
|---|---|---|
| **NALA-Assess** | Nanyang Technological University | AI chatbot for adaptive self-assessment. ⚠ Closed access |
| **Eva.ai** | Aristotle University of Thessaloniki | Conversational AI learning environment. ⚠ Closed (Springer) |
| *Guidance Over Adoption* | Adolfo Ibáñez University | ⭐ **Experimental** evidence on AI-assisted learning in higher ed. Green OA via SSRN but no abstract retrievable — **worth chasing, since experiments are rare here** |
| **Virginia Tech** | Virginia Tech | A published *"Comprehensive AI Governance & Activity Inventory"* — a governance artefact rather than a system, and a possible template for what PSU would want to see from us |

⚠ **Note the pattern in what we could not read.** Of the four, three are behind publisher bot
checks or paywalls, and the one green-OA item has no retrievable abstract. **The institutional
deployment literature is markedly less accessible than the arXiv-native AI literature**, which
systematically biases any survey — including this one — toward the systems built by AI labs rather
than by universities.

## Sources

- EDUCAUSE 2026 reporting, via [Perspective AI, "Where Universities Actually Deploy AI in 2026"](https://getperspective.ai/blog/ai-applications-in-education-where-universities-deploy-ai-in-2026) `[skimmed]` — **secondary source; find the EDUCAUSE original**
- [aiandacademia, "Higher education and AI in late 2025/early 2026"](https://aiandacademia.substack.com/p/higher-education-and-ai-in-late-2025early) `[found]`
- [Digital Education Council Global Survey 2026](https://www.digitaleducationcouncil.com/resource-library-items/ai-in-higher-education-global-survey-2026) `[skimmed]`
