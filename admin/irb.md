# IRB — Penn State

> ## Status: NOT SUBMITTED
> **This is the project's critical path.** Every student-facing activity in
> `docs/03-open-questions.md` section A is blocked until we have a determination letter.
> Owner: ___ · Target submission date: ___

## Why this applies to us

The common misconception is that IRB is for clinical trials and that "just talking to a
few students in my class" doesn't count. It does. Human subjects research is a systematic
investigation designed to contribute to generalizable knowledge, involving living
individuals about whom we obtain data through intervention or interaction. Interviewing
students about their study habits, recording it, analyzing it, and putting it in a
capstone report that we might publish is squarely that.

**This includes:**
- Semi-structured interviews (`research/student-interviews/protocol-draft.md`)
- Think-aloud sessions
- Surveys
- Any pilot where we log what students do with a tool we built
- Concept inventory pre/post scores

**This includes informal pilots with friends in the class.** There is no "we were just
chatting" exemption once the intent is research.

## Likely path

Most education research of this shape qualifies for **exempt** review under the
educational-settings category (research conducted in established educational settings
involving normal educational practices) or the benign-interviews category. Exempt still
requires a **submission and a written determination** — you do not get to decide you're
exempt.

Realistic timeline: weeks, not days. Exempt determinations are faster than full board
review but still queue. **Submit before you think you need to.**

## Checklist

- [ ] Identify faculty advisor of record — likely the instructor sponsor. Undergraduate
      research generally requires a faculty PI; students cannot be PI.
- [ ] All team members complete **CITI training** (human subjects research, social &
      behavioral track). Do this first — it takes hours and is a hard prerequisite for
      submission. Certificates attach to the protocol.
- [ ] Draft protocol in PSU's IRB submission system
- [ ] Consent form (use the PSU template, don't write your own)
- [ ] Recruitment materials — email text, flyer, any in-class announcement script
- [ ] Attach interview protocol / survey instruments
- [ ] Data management plan — see below
- [ ] Submit
- [ ] Determination letter received and filed → **unblocks section A**

## Data management — decide before submission

The IRB will ask. We should have answers we actually intend to follow.

| Question | Our answer |
|---|---|
| What identifiers do we collect? | |
| Where is raw data stored? | Not this repo. Not a personal laptop. PSU-managed storage. |
| Who has access? | |
| When is audio destroyed? | Proposal: after transcription and verification |
| How is data de-identified? | |
| Retention period? | |
| Is data shared outside the team? | |

**Repo rule, restated:** `thermo-tutor` is a **public repository**. No raw interview data,
no transcripts, no identifiable quotes, no screenshots containing student work ever get
committed. De-identified synthesis only, and only after review.

## The LLM vendor problem

Distinct from IRB and easy to miss.

If a pilot sends student work, names, IDs, or grades to a commercial LLM API, that data
leaves the institution. Under FERPA the usual basis is the **"school official"
exception**, which requires that the vendor's use be limited to the educational purpose
and — critically — that **student data not be used to train the vendor's models**.

Institutions have paused AI rollouts after discovering their vendor agreements referenced
FERPA generally but never addressed whether the model trained on inputs.

**Design mitigation that avoids most of this:** pseudonymize at the boundary. The tutor
service maps a student to an opaque ID; the LLM never receives a name, an email, a PSU
ID, or a grade. Student-authored text still leaves, so this is mitigation, not
elimination — but it removes the sharpest edge.

> ## ✅ PARTIALLY RESOLVED — 2026-08-29
>
> **Penn State already runs AI Studio**, an enterprise generative AI platform providing
> **Claude, ChatGPT, and Gemini** to all students, with published terms stating that
> **"personal information is not used to train AI Studio or its underlying AI models."**
> That is precisely the condition the FERPA "school official" exception requires of a vendor,
> and it is the clause whose absence caused other institutions to pause AI rollouts.
>
> This does **not** eliminate the IRB requirement — that is about human subjects research and
> is untouched. It may eliminate the *vendor agreement* problem entirely.
>
> **Remaining question, and it decides the architecture: does AI Studio expose an API, or
> only a chat interface?** A chat-only tool cannot back a custom application.
>
> Details and sources: [PSU AI landscape](../knowledge/practice/psu-ai-landscape.md)

**Action items:**
- [x] ~~Check whether PSU has an enterprise agreement with an LLM vendor~~ — **yes, AI
      Studio.** See above.
- [ ] **Confirm AI Studio exposes an API.** Blocking for the architecture.
- [ ] Read the actual AI Studio terms and first-login acknowledgement, not the press release
- [ ] Confirm whether AI Studio is an approved channel for a research pilot handling student
      coursework, and who approves that
- [ ] Confirm the API terms for whatever we use prohibit training on inputs
- [ ] Note the local-model option: **Stan (U. Delaware) ran on Ollama specifically so
      nothing left the machine.** If the compliance path gets ugly, that's the escape
      hatch, at a real cost in model quality.

## Things that bite student teams

- Starting interviews "informally" before approval, then trying to use the data. You
  can't. It's unusable and it's a compliance problem.
- Discovering CITI training is required the week you wanted to submit.
- Not having a faculty PI lined up.
- Changing the protocol mid-study without filing an amendment.
- Assuming a class project is automatically exempt from everything. It isn't, especially
  once you intend to publish or present outside the course.

## Links to fill in

- [ ] PSU IRB office / submission system URL
- [ ] CITI training portal
- [ ] PSU consent form template
- [ ] Faculty advisor contact
