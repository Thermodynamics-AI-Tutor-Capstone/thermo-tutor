# Jill Watson

**Type:** system
**One line:** Georgia Tech's virtual teaching assistant — the first AI TA deployed in a
real university course, and still the best-documented example of grounding-and-verification
beating raw model capability.
**Why we care:** Its 2024 head-to-head against OpenAI's Assistant is the cleanest evidence
in the field that architecture matters more than model choice.

## Origin (2015–2016)

Conceived in **summer 2015** by Ashok Goel's team at Georgia Tech's Design Intelligence
Lab, for **CS7637: Knowledge-Based Artificial Intelligence: Cognitive Systems (KBAI)** —
a course created in 2014 for the Online MS in Computer Science (OMSCS).

The motivating problem was scale, not intelligence: ~300 students posting roughly
**10,000 forum messages** per term, against one professor and eight human TAs.

**Build:** implemented on IBM Watson. The team collected every question asked in KBAI
since fall 2014 — approximately **40,000 postings** — and used them as training data.
Jill was gated behind a high answer-confidence threshold, so she only posted when nearly
certain and stayed silent otherwise.

## The spring 2016 deployment

Jill answered forum questions with reported **>90% accuracy** and, critically, students
did not identify her as an AI during the term. Goel revealed it at the end of the
semester. The reveal — and student reactions to it — is what made this internationally
known.

This raises a disclosure question the field still hasn't settled; see
[disclosure and ethics](../practice/disclosure-and-ethics.md).

## The 2024 LLM rebuild — the important part

DILab, with the NSF **AI-ALOE** institute, rebuilt Jill Watson on OpenAI's ChatGPT. The
design commitment: **restrict outputs to validated course material, and verify every
response using textual entailment** before it reaches a student.

Head-to-head against OpenAI's own Assistant on the same courses (Taneja et al., 2024):

| Metric | Jill Watson | OpenAI Assistant |
|---|---|---|
| Answers correctly | **78.7%** | 30.7% |
| Harmful failures | **2.7%** | 14.4% |
| Confusing failures | **54.0%** | 69.2% |
| Retrieval failures | **43.2%** | 68.3% |

Same underlying LLM. **2.5× the accuracy and one-fifth the harmful error rate**, purely
from grounding and verification.

Note the honest reading: 43.2% retrieval failure is still very high, and 54% of Jill's
errors are still "confusing." The system is much better, not good.

## Measured educational effect

Later work found Jill Watson improved **teaching presence** and correlated with better
academic performance — described by the researchers as the first documented instance of a
chatbot enhancing teaching presence in online learning for adult students.

Teaching presence, not content delivery, is the mechanism. That's a repeated theme; see
[engagement decay](../concepts/engagement-decay.md).

## What to steal

1. **Confidence gating.** Answer only when sure; escalate otherwise. Most LLM tutors
   answer always.
2. **Textual entailment verification** as a cheap, model-agnostic output check.
   → [grounding and verification](../concepts/grounding-and-verification.md)
3. **Restriction to validated course material** as a hard constraint, not a prompt
   preference.

## Open questions

- [ ] What exactly is the entailment model and threshold? Is the implementation public?
- [ ] What does the 43.2% retrieval failure consist of — missing content, bad chunking, or
      bad queries?
- [ ] Has anyone replicated the Jill-vs-Assistant comparison independently?
- [ ] What did students actually say at the 2016 reveal? Primary sources, not press.

## Connects to

- [grounding and verification](../concepts/grounding-and-verification.md) — the mechanism
  behind the results table
- [RAG in education](../concepts/rag-in-education.md) — the retrieval layer and its limits
- [CS50 Duck](cs50-duck.md) — the other large, long-running course-embedded deployment
- [disclosure and ethics](../practice/disclosure-and-ethics.md) — the 2016 reveal

## Sources

- [Goel & Polepeddi, "Jill Watson: A Virtual Teaching Assistant for Online Education" (2018)](https://dilab.gatech.edu/publications/) `[found]` — the canonical history chapter. **PDF link 404s; find a working copy.**
- [Georgia Tech News, "Artificial Intelligence Course Creates AI Teaching Assistant" (2016)](https://news.gatech.edu/news/2016/05/09/artificial-intelligence-course-creates-ai-teaching-assistant) `[skimmed]` — origin, 40,000 postings figure
- [Georgia Tech, "Jill Watson Outperforms ChatGPT in Real Classrooms" (Sept 2025)](https://news.research.gatech.edu/2025/09/02/georgia-techs-jill-watson-outperforms-chatgpt-real-classrooms) `[skimmed]` — the Taneja et al. 2024 comparison numbers
- [DILab project page](https://dilab.gatech.edu/projects/jill-watson/) `[found]`
- [AI-ALOE, "The Return of Jill Watson"](https://aialoe.org/the-return-of-jill-watson/) `[found]`
