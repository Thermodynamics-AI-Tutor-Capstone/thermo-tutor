# Cogniti — University of Sydney

**Type:** system
**One line:** A platform that lets *instructors* build their own AI agents for their own
courses — an "AI stunt double for teachers" — rather than IT shipping one tutor for
everyone.
**Why we care:** The strongest example of the "tutor factory" architecture, and the answer
to a question we should ask ourselves: is our deliverable one tutor, or the thing that
makes tutors?

## What it is

Built by **Professor Danny Liu** and the Educational Innovation team at the University of
Sydney. Teachers create custom AI agents ("agents") steered with their own instructions
and resourced with their own course materials, then embed them in the university's LMS.

Liu is a molecular biologist by training working across educational technology, student
engagement, learning analytics, and pedagogical research — which shows in the design.

## The design commitment

**Teachers stay in control.** This is the defining choice and it's a pedagogical position,
not a technical one: the person who knows the course sets the agent's behavior, rather
than a central team guessing on their behalf.

Consequences worth noting:
- Scales across wildly different subjects — deployments span **chemical engineering to
  musicology**, and language agents that converse at a student's level.
- Distributes the hand-crafting work that [Kestin's result](../evidence/kestin-2025-rct.md)
  suggests is where learning gains actually come from.
- Also distributes the *risk*: an instructor who writes a bad agent ships a bad agent.

## Trajectory

- Won the **Australian Financial Review 2025 AI Award**
- Published to **Microsoft Azure Marketplace** (June 2026), available to academics
  globally
- Built on Azure OpenAI Service

## The question it poses for us

If the differentiator in this field is **course-specific hand-work**, then a platform that
makes hand-work cheap may matter more than any single tutor. [U-M Maizey](umich-maizey.md)
reached the same conclusion independently — 3,500+ instances built by faculty rather than
one central tutor.

Against that: our brief is a thermodynamics tutor, and a platform is a much bigger
engineering project with much weaker research claims. Noting the tension, not resolving it.

## Open questions

- [ ] Any published learning-outcome evidence, or adoption and satisfaction only?
- [ ] What guardrails does the platform enforce vs. leave to the instructor?
- [ ] How many instructors actually build good agents? What's the quality distribution?
- [ ] Is there a knowledge-tracing / mastery layer, or is each agent stateless chat?
- [ ] Can it be self-hosted, and what does it cost?

## Connects to

- [U-M Maizey](umich-maizey.md) — the same instructor-builds-it model, independently
- [LMS integration](../practice/lms-integration.md) — Cogniti's embedding approach
- [faculty adoption](../practice/faculty-adoption.md) — this design lives or dies on it
- [PeteChat](petechat-purdue.md) — the opposite bet: one deeply-tuned course tutor

## Sources

- [Sydney, "Cogniti, an 'AI stunt double' for teachers, wins AFR AI Award" (June 2025)](https://www.sydney.edu.au/news-opinion/news/2025/06/03/cogniti-an-ai-stunt-double-for-teachers-wins-afr-ai-award.html) `[skimmed]`
- [Sydney, "AI education platform Cogniti goes global on Microsoft Marketplace" (June 2026)](https://www.sydney.edu.au/news-opinion/news/2026/06/15/ai-education-platform-cogniti-goes-global-on-microsoft-marketplace.html) `[skimmed]`
- [Microsoft customer story — Sydney + Azure OpenAI](https://www.microsoft.com/en/customers/story/1785425602161769458-university-of-sydney-azure-openai-service-higher-education-en-united-states) `[found]`
- [Intentional Teaching podcast — Clemson, Hesse, Liu on teaching with AI agents](https://intentionalteaching.buzzsprout.com/2069949/episodes/17282776-teaching-with-ai-agents-with-matthew-clemson-isabelle-hesse-and-danny-liu) `[found]`
