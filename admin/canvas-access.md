# Canvas Access

We have an instructor sponsor, which moves us up the ladder considerably. This documents
what's actually available at each rung so we don't design around access we can't get.

## The ladder, hardest to easiest

### Rung 1 — LTI 1.3 / LTI Advantage  *(institutional, hardest)*
The "real" integration. Canvas supports LTI 1.3 + Advantage, which bundles:

- **Deep Linking** — the tool appears inside Canvas as an assignment or module item
- **Assignment and Grade Services (AGS)** — create gradebook columns and write grades
  back without the instructor creating them manually
- **Names and Roles Provisioning (NRPS)** — roster and enrollment data

**Blocker:** requires an **admin-issued developer key** at the Canvas instance level.
That's PSU IT, not the instructor. A student capstone will find this hard and slow, and
it may require a security review of a system that doesn't exist yet.

**Verdict:** stretch goal. Design for it, don't depend on it, and don't spend research
time on it this phase.

### Rung 2 — Instructor-scoped API token  *(realistic, our target)*
The instructor generates a Canvas API access token and authorizes us to use it for their
course. Canvas REST API then gives us syllabus, assignments, due dates, files, and
submissions for that course.

**Blocker:** the token carries the instructor's full permissions, which is a real
security concern and one they should push back on. Expect — and welcome — scrutiny. Ask
early; don't surprise them with it in month three.

**Verdict:** the plan of record, given a sponsor.

### Rung 3 — Student's own personal access token  *(always works)*
Each student generates their own token in Canvas settings and pastes it in. Scoped to
exactly what that student can already see. No IT involvement, no instructor involvement.

**Downside:** friction at signup — asking a student to generate an API token is a real
drop-off point, and "paste this secret into a website some students built" is a
reasonable thing to refuse. It also means we hold student credentials, which raises its
own compliance question.

**Verdict:** the fallback that cannot be taken away from us. Worth prototyping precisely
because it has no dependencies.

### Rung 4 — Manual upload  *(zero dependencies)*
Student or instructor uploads the syllabus and assignment PDFs directly.

**Verdict:** the floor. Everything must degrade to this. It's also entirely sufficient
for early research and rough drafts — which is where we are.

## Recommendation for this phase

**Don't build any of it yet.** We're in research. What we need now is to *know* which
rung we'll land on, because it changes what a pilot can even measure. Get the answer, not
the integration.

## Questions for the instructor sponsor

- [ ] Which Canvas instance is the course on, and which textbook does it use?
- [ ] Would you be willing to generate a course-scoped API token, or does that make you
      uncomfortable? (Both answers are fine — we need to know now.)
- [ ] Has anyone at PSU built a Canvas LTI tool before? Who did they talk to in IT?
- [x] ~~Does PSU have an enterprise agreement with an LLM vendor?~~ **Yes — AI Studio,
      with Claude/ChatGPT/Gemini.** → [PSU AI landscape](../knowledge/practice/psu-ai-landscape.md)
- [ ] **Does AI Studio expose an API, and does it already integrate with Canvas?** If it
      does both, it may solve the model-access and the LMS-access problems at once. **Highest
      priority question on this page.**
- [ ] Are you connected to the PSU AI Center of Excellence in Teaching and Learning? They
      awarded 46 instructional innovation grants for 2026–27 — we should know whether any
      overlap with this project before we duplicate funded work.
- [ ] Can you sponsor us for PhysPort educator verification to get the TCI?
- [ ] Do you use Mastering Engineering / Connect / WileyPLUS? Can we get evaluator access
      for the teardown?
- [ ] **How would an AI tutor change what homework grades mean to you?**
      (Question C5. Raise this before they do.)

## Questions for PSU IT — only if we go for rung 1

- [ ] What's the process for a developer key on the PSU Canvas instance?
- [ ] Is there a security review, and what's the lead time?
- [ ] Any precedent for student-built LTI tools?

## Reference

- Canvas LTI docs: https://developerdocs.instructure.com/services/canvas/external-tools/lti/file.tools_intro
- AGS / grading: https://developerdocs.instructure.com/services/canvas/external-tools/lti/file.assignment_tools
- API vs. LTI, plain language: https://ed.link/community/api-vs-lti-integration-for-canvas/
