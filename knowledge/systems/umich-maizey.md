# U-M Maizey — University of Michigan

**Type:** system
**One line:** Michigan's university-built, closed generative AI platform — faculty create
course-specific tutors that appear in a Canvas side panel.
**Why we care:** The strongest *institutional-scale* numbers in this literature, and the
closest model for what a Penn State deployment could look like.

## What it is

Part of U-M's decision to build its own closed generative AI tools rather than route
students to commercial products — a data-governance choice as much as a technical one.
Maizey lets faculty and staff build retrieval-grounded assistants over their own content.

## Scale

- **3,500+ Maizey instances** in production across academic departments and operational
  offices (procurement, HR)
- **~15,000 users/day** across U-M's AI tools
- Canvas integration: when enabled in a course, students reach the tutor from the Canvas
  side panel

## The results — and how much to trust them

In a study of a **1,000-student class**:

- Students who used Maizey saw grades improve **5–9%**
- The AI tutor answered questions **94% as effectively as, or better than,** the people
  teaching the course, across qualitative and quantitative questions

**Read the first number carefully.** "Students who used it" is self-selection, not
assignment. Students who voluntarily use an optional study tool differ systematically from
those who don't — they're the same ~5% power-user population documented in
[equity](../practice/equity.md), skewing already-higher-performing. A 5–9% grade
difference between users and non-users is consistent with a real tutoring effect **and**
with the tutor doing nothing at all.

This isn't a knock on Michigan — it's the normal state of institutional evaluation, and
they reported it plainly. But it's exactly the gap between a correlational deployment
report and [Kestin's RCT](../evidence/kestin-2025-rct.md), and we should be clear which
kind of evidence we're producing.

The 94% figure is different and more defensible: that's a head-to-head answer-quality
comparison against course staff, closer to the
[CS50 TF-comparison method](cs50-duck.md).

## Why this is our institutional template

Michigan and Penn State are structurally similar: large public research universities,
Canvas, central IT with an appetite for building. PSU already has **AI Studio** offering
Claude, Gemini, and ChatGPT to all students — see
[PSU AI landscape](../practice/psu-ai-landscape.md). Maizey is roughly what the mature
version of that looks like.

## Open questions

- [ ] Which class was the 1,000-student study, and is the methodology published?
- [ ] How was the 94% effectiveness comparison actually run — who judged, how many items?
- [ ] Retention: do students keep using Maizey through the term?
- [ ] What is the underlying model, and is it swappable?
- [ ] How did they get Canvas side-panel integration approved? **Ask PSU IT the same
      question** → [LMS integration](../practice/lms-integration.md)

## Connects to

- [Cogniti](cogniti-sydney.md) — the same faculty-builds-it model, arrived at independently
- [PSU AI landscape](../practice/psu-ai-landscape.md) — our institution's version
- [LMS integration](../practice/lms-integration.md) — the Canvas side panel is the target
- [equity](../practice/equity.md) — why the 5–9% number needs a self-selection caveat

## Sources

- [EDUCAUSE Review, "How (and Why) the University of Michigan Built Its Own Closed Generative AI Tools" (Feb 2024)](https://er.educause.edu/articles/2024/2/how-and-why-the-university-of-michigan-built-its-own-closed-generative-ai-tools) `[skimmed]`
- [EdTech Magazine, "How Three Universities Developed Their Chatbots" (May 2025)](https://edtechmagazine.com/higher/article/2025/05/how-three-universities-developed-their-chatbots) `[skimmed]` — scale and grade figures
- [Michigan Ross, "U-M GPT's Maizey tool guides students to success"](https://michiganross.umich.edu/news/u-m-gpt-s-maizey-tool-guides-students-success) `[found]`
- [U-M ITS AI release notes](https://its.umich.edu/computing/ai/release-notes) `[found]`
