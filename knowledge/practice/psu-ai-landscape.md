# Penn State's AI Landscape

**Type:** practice / institutional
**One line:** Penn State already runs an enterprise generative AI platform with Claude,
ChatGPT, and Gemini, available to every student, with terms stating personal information is
not used to train the models.
**Why we care:** This removes what we had identified as the project's single scariest
compliance obstacle, and it simultaneously defines the competitor our tutor has to beat.

## What exists

**AI Studio** — Penn State's enterprise generative AI platform. A single interface providing
access to models from **OpenAI (ChatGPT), Anthropic (Claude), and Google (Gemini)**, letting
users pick the model for the task.

- Launched for University **employees in April**; extended to **all students** in the fall
- Described as "a Penn State-managed environment with its own governance, enabled models,
  knowledge-source options, and privacy controls"
- On first login, users acknowledge data handling, permitted use, and the limitations of
  AI-generated content

**AI Essentials** — a self-paced online AI literacy course, available to all students.

**AI Center of Excellence in Teaching and Learning** — awarded **46 grants** to Penn State
faculty and faculty teams in its inaugural cycle, through two instructional innovation grant
programs supporting integration of generative AI into teaching and learning. Funding projects
for **2026–27**.

**Also available:** Microsoft Copilot, Google Gemini and Gemini Notebook, Adobe Firefly.
An "AI Creative Labs" program has engaged 900+ students across seven colleges since spring
2025. Penn State Harrisburg launches a BS in AI Methods and Applications in fall 2026.

## The privacy terms — the important part

Penn State's published position on AI Studio:

- **"Personal information is not used to train AI Studio or its underlying AI models."**
- Penn State IT employees do not actively monitor individual prompts or conversations
- Chats disclosed only in limited circumstances — health or safety emergency, or legal
  request

**That first bullet is the exact requirement** the FERPA "school official" exception imposes
on a vendor, and the reason institutions have paused AI rollouts elsewhere: contracts that
referenced FERPA generally but never addressed whether the vendor trained on inputs.

If AI Studio is an approved channel for coursework data, then building on it is a
fundamentally different compliance posture than calling a commercial API ourselves.
**This is the single highest-leverage thing to confirm in week 1.**
→ [IRB and compliance](../../admin/irb.md)

## Three consequences for our project

**1. The compliance path may already exist.** Confirm with the instructor sponsor and PSU IT
whether AI Studio can be used for a course tutor handling student coursework, and whether it
exposes an API or only a chat UI. **If there's no API, this advantage largely evaporates for
a custom application** — that's the question that decides it.

**2. It defines our comparison condition, and it's a hard one.** Every PSU student already
has free, sanctioned access to Claude, ChatGPT, and Gemini. Our tutor is not competing with
"nothing." It's competing with **frontier models the university already handed them**.

That's the same situation as [ASU](../systems/asu-openai.md), and it makes the honest claim
harder: we must beat a frontier model with course context, a
[student model](../concepts/knowledge-tracing.md), and
[property tools](../domain/property-data-tools.md) — the seven layers, not the model.
→ [open question C4](../../docs/03-open-questions.md)

**3. There is an institutional funding and legitimacy path.** The AI Center of Excellence
awards instructional innovation grants for 2026–27. A thermodynamics AI tutor with an
instructor sponsor is squarely in scope. Worth asking about even if we don't apply —
the Center will know who else at PSU is doing this, which is worth as much as money.

## Also: the TCI connection

The [Thermodynamics Concept Inventory](../evaluation/concept-inventories.md) was developed at
Penn State. Two independent institutional advantages in the same project is unusual — use
both.

## Open questions — all week 1

- [ ] **Does AI Studio expose an API, or only a chat interface?** This decides everything.
- [ ] Can AI Studio be used for a research pilot handling student coursework? Who approves?
- [ ] What exactly do the AI Studio terms say? Read the actual acknowledgement text, not the
      press release.
- [ ] Is our instructor sponsor aware of / connected to the AI Center of Excellence?
- [ ] Did any of the 46 grants go to something adjacent? **We should not duplicate a funded
      PSU project by accident.** Ask the Center directly.
- [ ] Who at PSU developed the TCI, and are they reachable?

## Connects to

- [IRB and compliance](../../admin/irb.md) — the obstacle this may remove
- [ASU + OpenAI](../systems/asu-openai.md) — the same institutional strategy elsewhere
- [U-M Maizey](../systems/umich-maizey.md) — what the mature version looks like
- [concept inventories](../evaluation/concept-inventories.md) — the other PSU asset
- [Canvas access](../../admin/canvas-access.md) — questions for the sponsor

## Sources

- [AI at Penn State](https://ai.psu.edu/) `[read]`
- [Penn State launches AI Studio for faculty and staff](https://www.psu.edu/news/campus-life/story/penn-state-launches-ai-studio-faculty-and-staff) `[skimmed]`
- [AI literacy course, suite of services now available to Penn State students](https://www.psu.edu/news/academics/story/ai-literacy-course-suite-services-now-available-penn-state-students-enrolled-summer) `[skimmed]` — the privacy terms
- [A student guide to AI at Penn State](https://www.psu.edu/news/academics/story/student-guide-ai-penn-state-resources-and-tips-know-fall) `[skimmed]`
- [AI Center of Excellence awards first instructional innovation grants](https://www.psu.edu/news/faculty-and-staff/story/ai-center-excellence-awards-first-instructional-innovation-grant-recipients) `[skimmed]`
- [AI at Penn State — FAQs](https://ai.psu.edu/resources/frequently-asked-questions) `[found]` — **read this properly**
