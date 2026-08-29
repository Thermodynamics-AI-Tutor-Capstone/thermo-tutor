# LMS Integration

**Type:** practice
**One line:** Canvas LTI 1.3 / Advantage versus REST API tokens — what each buys, and what
each costs in institutional approval.
**Why we care:** "It has access to their Canvas" is in our project brief, and the access path
determines what a pilot can measure.

## The two mechanisms

**LTI 1.3 / LTI Advantage** — the standards-based integration. Canvas supports it and it
bundles three services:

| Service | What it does |
|---|---|
| **Deep Linking** | The tool appears inside Canvas as an assignment or module item |
| **Assignment and Grade Services (AGS)** | Create gradebook columns and write grades back without the instructor making them manually |
| **Names and Roles Provisioning (NRPS)** | Roster and enrollment data |

**Requires an admin-issued developer key** at the Canvas instance level. That's PSU IT, not
the instructor, and it may trigger a security review of a system that doesn't exist yet.

**Canvas REST API** — direct API calls with an access token. Gives syllabus, assignments, due
dates, files, submissions. Simpler, and the token carries whatever permissions its owner has.

The plain-language distinction ([Edlink has a good writeup](https://ed.link/community/api-vs-lti-integration-for-canvas/)):
**LTI is about launching and being embedded; the API is about reading and writing data.** A
tutor that needs both course content *and* placement inside Canvas eventually wants both.

## The access ladder

See [our access plan](../../admin/canvas-access.md) for the full version. Summary:

| Rung | Mechanism | Blocker | Verdict |
|---|---|---|---|
| 1 | LTI 1.3 + Advantage | Admin developer key from PSU IT | Stretch goal |
| 2 | Instructor-scoped API token | Instructor's full permissions — legitimate security concern | **Plan of record** (we have a sponsor) |
| 3 | Student's own personal token | Signup friction, we hold student credentials | Fallback that can't be taken away |
| 4 | Manual upload | None | The floor. Must always work |

## What [U-M Maizey](../systems/umich-maizey.md) achieved, and the question it raises

When Maizey is enabled in a Canvas course, students reach the tutor from **the Canvas side
panel**.

That's rung 1, at a peer institution, and it's worth understanding how they got there — the
approval path is probably more transferable than the technology. **Ask PSU IT the same
question Michigan's team must have answered.**

## The friction argument, which matters more than the plumbing

Every access rung above 4 adds setup steps, and setup steps are where voluntary tools die.

- Rung 3 asks a student to generate an API token and paste it into a website built by three
  undergraduates. Many will reasonably decline, and the ones who don't skew toward the
  already-confident. → [equity](equity.md)
- Rung 1 is the *only* option with zero student friction: the tutor is simply already there,
  inside the LMS the student already has open.

Given that [17% session engagement](../evidence/khanmigo-engagement-2026.md) is the field's
actual failure mode, **integration depth is an engagement feature, not a convenience
feature.** That reframes it from "nice to have" to something worth spending institutional
capital on. → [engagement decay](../concepts/engagement-decay.md)

## What we actually need this phase

**Nothing built.** We're in research. What we need is to *know* which rung we'll land on,
because it determines what a pilot can measure and how much friction stands between a student
and the tutor.

Get the answer, not the integration.

## Open questions

- [ ] Which Canvas instance is the course on?
- [ ] Will the sponsor generate a course-scoped API token, or is that uncomfortable? **Both
      answers are fine — we need to know now.**
- [ ] Has anyone at PSU built a Canvas LTI tool? Who did they talk to in IT?
- [ ] Does [AI Studio](psu-ai-landscape.md) already have a Canvas integration we could ride?
      **Would solve both problems at once — check first.**
- [ ] What's the PSU developer key process, and the lead time?

## Connects to

- [our Canvas access plan](../../admin/canvas-access.md) — the operational version
- [U-M Maizey](../systems/umich-maizey.md) — the Canvas side panel, achieved
- [engagement decay](../concepts/engagement-decay.md) — friction as the churn mechanism
- [equity](equity.md) — friction filters unevenly
- [PSU AI landscape](psu-ai-landscape.md) — possibly a shortcut

## Sources

- [Canvas LTI documentation (Instructure)](https://developerdocs.instructure.com/services/canvas/external-tools/lti/file.tools_intro) `[skimmed]`
- [Canvas Assignment and Grade Services](https://developerdocs.instructure.com/services/canvas/external-tools/lti/file.assignment_tools) `[skimmed]`
- [Edlink, "API vs. LTI integration for Canvas"](https://ed.link/community/api-vs-lti-integration-for-canvas/) `[skimmed]`
