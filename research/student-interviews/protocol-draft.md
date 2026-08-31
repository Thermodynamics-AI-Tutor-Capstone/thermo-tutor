# Student Interview Protocol — DRAFT

> ## ⚠️ DO NOT USE. NOT YET APPROVED.
>
> This protocol has **not** been submitted to or approved by the Penn State IRB.
> Talking to students about their coursework experience and recording what they say is
> human subjects research. Do not run a single interview — including an "informal" one
> with a friend in the class — until we have a determination letter in hand.
>
> See `admin/irb.md`. Status: **not submitted.**

---

## Purpose

Answer questions A1–A4 in `docs/03-open-questions.md`. Specifically: what students
actually do when stuck in thermodynamics, what they currently use, and what they believe
an AI tutor is for.

Not a usability test. We have nothing to test. This is discovery.

## Participants

Target: 12–15 interviews. Recruitment stops when new interviews stop producing new
categories.

Deliberately sample for variation, not convenience:

- Students currently in thermo and students who took it 1–2 semesters ago (hindsight is
  useful; memory is worse — collect both)
- Across the grade distribution, not just the students who volunteer (the students who
  volunteer for a study about learning tools are not representative)
- Both heavy and light AI users, including at least two who say they don't use AI at all
- Mix of majors if the course draws from several

## Format

45 minutes, semi-structured, one interviewer + one notetaker. Audio recorded **only with
explicit consent**, transcribed, then the audio is destroyed per the IRB protocol.

---

## Part 1 — Warm-up (5 min)

Establish that we're not evaluating them and there are no wrong answers. Say plainly that
we are not their instructor, this doesn't affect their grade, and we're interested in
what actually happens, including things they might not put in a course evaluation.

1. What year are you, what's your major?
2. When are you taking / did you take thermo?
3. In one sentence — how's it going / how did it go?

## Part 2 — The last assignment (15 min) — *the core of the interview*

Retrospective walkthrough. Concrete beats abstract; do not let this drift into generality.

4. Think about the most recent thermo problem set. Walk me through the last time you sat
   down to work on it. Where were you, what time, what did you have open?
5. Was there a problem you got stuck on? Tell me about that one specifically.
   - *Probe:* What did "stuck" feel like — did you not know what equation, or not know
     what was going on physically, or know what to do but couldn't execute it?
   - *Probe:* What was the very first thing you did after realizing you were stuck?
   - *Probe:* How long did you sit with it before doing that?
6. What did you try next? And after that?
7. Did you get unstuck? What actually unstuck you?
8. Was there a point where you decided to just get the answer and move on? What triggered
   that?

*Interviewer note: question 8 is the most important one in this protocol and the easiest
to ask badly. Ask it without any hint of judgment. If the student senses that "just
getting the answer" is the wrong answer, the rest of the interview is worthless.*

## Part 3 — Current tools (10 min)

9. What do you use when you're stuck? List everything — people included.
10. For each: when do you reach for that one specifically?
11. *(If they mention an AI tool)* Show me how you'd ask it about a thermo problem. What
    do you type?
    - *Probe:* Do you trust what it tells you? How do you check?
    - *Probe:* Has it ever been confidently wrong? What happened?
12. *(If they mention Chegg / Course Hero / similar)* What does that give you that an AI
    doesn't?
13. What about office hours, the TA, study groups? What makes those work or not work?

## Part 4 — Mental model of a tutor (10 min)

14. Imagine a tutor that knows your course — your syllabus, your assignments, everything
    you've worked on. What would you want it to do?
15. Suppose you ask it a homework question and instead of answering it asks you a
    question back. What's your honest reaction?
    - *Probe:* Under what circumstances would that be helpful rather than annoying?
    - *Probe:* What would make you close the tab?
16. Would you want your instructor to see what you asked it? Why or why not?
17. If a tool like this existed and was optional, would you still be using it in week ten?
    What would have to be true?

*Interviewer note: expect socially desirable answers to 15 and 17. Discount them. The
useful data is in the hesitations and the conditions they attach.*

## Part 5 — Close (5 min)

18. Anything about learning thermo we should have asked and didn't?
19. Anyone else we should talk to?

---

## Methodological precedent worth copying

**Amoozadeh et al., "Student-AI Interaction: A Case Study of CS1 Students" (arXiv:2407.00305)**
is the closest published analogue to what we are planning, and its design is directly
reusable:

- **15 students**, deliberately gender-balanced and majority non-white, **observed while
  solving real programming tasks** with ChatGPT available
- **Mixed methods triangulated three ways**: automated interaction logging, video analysis of
  the session, and self-reported measures
- Coded every prompt by the *information need* it served, and coded student *reactions* to AI
  answers into "acceptance categories" (accepted / partial / hybrid / rejected)
- Measured **self-efficacy before and after** — an outcome dimension our plan does not
  currently include and probably should

Their headline finding is a useful expectation-setter: participants *"extensively interacted
with Generative AI, yet successfully provided correct answers only in 65% of the cases; the
rest remained unsolved."*

**Three things to take:** n=15 with observation beats n=50 with self-report; log + video +
survey triangulation is the right instrument set; and coding *reactions* to AI output — not
just prompts — is where the interesting behaviour lives.

For transcript coding at scale, see also the LLM-open-coding pipeline in
[Socratic tutoring](../../knowledge/concepts/socratic-tutoring.md), validated at Cohen's
κ = 0.78.

## Analysis plan

- Transcribe, then open-code the first 5 interviews independently by two team members.
- Reconcile into a shared codebook before coding the rest.
- Target output: a small number of student archetypes plus a map of where in the
  problem-solving process help is actually sought.
- De-identify before anything enters `synthesis/`. **Raw transcripts never enter this
  repo** — public repository, see README.

## What we're at risk of getting wrong

- **Recall bias.** Students reconstruct a tidier process than they had. Part 2 anchors on
  a specific recent event to limit this, but it doesn't eliminate it. Think-alouds
  (question A4) are the real fix.
- **Social desirability.** Nobody wants to tell three engineering students that they
  Chegged the whole problem set. Framing in Part 1 matters more than any question here.
- **Sampling bias.** Students who agree to a 45-minute unpaid interview about study
  habits are unusual. Note this as a limitation; consider compensation if the budget and
  IRB allow.
- **Leading questions.** Question 14 in particular sells our idea to the participant.
  Consider moving it last, or splitting the sample so half never hear it.

## Still to write

- [ ] Consent form (IRB template)
- [ ] Recruitment email / flyer text
- [ ] Think-aloud protocol (separate instrument, question A4)
- [ ] Compensation decision and mechanism
