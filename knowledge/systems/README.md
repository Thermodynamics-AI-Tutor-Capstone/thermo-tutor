# Systems

One node per tutoring system. History, architecture, measured results, and what to steal.

## The modern LLM era (2023–2026)

| System | Institution | Domain | Why it matters |
|---|---|---|---|
| [CS50 Duck](cs50-duck.md) `[read]` | Harvard | CS | Largest deployment (9.4M prompts). **Hearts throttle; 88% curricular accuracy; only 3% never-users** |
| [Jill Watson](jill-watson.md) | Georgia Tech | CS (KBAI) | First AI TA; grounding+verification beats raw model 2.5× |
| [Stan](stan-udel.md) `[read]` | U. Delaware | **Thermodynamics** | Same domain — but **Level 1–2 only**; no tutoring, no evaluation |
| [PeteChat](petechat-purdue.md) `[read]` | Purdue | Python (ECE 20875) | **Eight design principles.** A design case (n=4), not an outcome study |
| [Cogniti](cogniti-sydney.md) | Sydney | All | Instructors build their own agents |
| [U-M Maizey](umich-maizey.md) | Michigan | All | 3,500 instances; strongest institutional numbers |
| [ASU + OpenAI](asu-openai.md) | Arizona State | All | Universal frontier-model access |
| [Khanmigo](khanmigo.md) | Khan Academy | K-12 math | Largest deployment; the engagement lesson |
| [LearnLM](learnlm.md) | Google DeepMind | Model | Pedagogy in the weights, not the prompt |
| [Tutor CoPilot](tutor-copilot.md) `[read]` | Stanford | K-12 math | Coaches the *tutor*. RCT, 900 tutors. **$20/tutor/yr vs $3,300 for conventional PD** |
| [CodeAid](codeaid-toronto.md) | U. Toronto | C / systems programming | **Pseudo-code instead of code** — a *structural* guardrail. 700 students, CHI 2024 |
| [**Hybrid human-AI tutoring**](hybrid-human-ai-tutoring.md) `[read]` | CMU + Stanford (Koedinger, Aleven, Brunskill) | K-8 math (IXL) | ⭐ **The only study that *tests* proactivity, and the only tutor-to-student ratio attached to an outcome — 1:4 proactive for the bottom half, 1:10 reactive for the top.** +25% time on task, +36% proficiency, +61% MAP growth. ⚠⚠ **No control group** |

## The classical ITS era (1970s–2015)

| System | Institution | Domain | Why it matters |
|---|---|---|---|
| [Andes](andes.md) `[read]` | Pitt + USNA + Rutgers | **Physics** | Step-based, 5-year evaluation. **Drawings +1.21, answers −0.08** |
| [**aiPlato**](aiplato-uta.md) | UT Arlington + Harvard | **Physics homework** | ⭐ **All 61 students used "Evaluate My Work"; hints and chat barely touched. 0.81 on a *final exam*, self-selected** |
| [**RAG + SRL engineering tutor**](rag-tutor-southeast.md) | Large public, SE US | Circuits, signals | **The closest deployed analogue to our project. 27,242 interactions, three modes, honest about causality. Guidance targeting is its top failure** |
| [**GPThermo**](gpthermo-wpi.md) | Worcester Polytechnic | **THERMODYNAMICS** | **Multi-agent GPT-4o + property tools: 95% vs 15–25% for stock models. No tutoring, no students — the tool layer, validated. Undergraduate first author** |
| [**bioTutor**](biotutor-eth.md) | ETH Zurich | Biology | **Open source. 407 students, 23 weeks, 10,000+ interactions — the longest deployment here. Instructor dashboard. ⚠ No learning outcome** |
| [**Ethel**](ethel-eth.md) | ETH Zurich | Physics / **thermodynamics** | **University-built virtual TA. Publishes its cost ($7.50/student/semester) and its failures. Grading: high precision, ~50% recall** |
| [**CyclePad / CycleTalk**](cyclepad-cycletalk.md) | Northwestern + USNA + CMU | **THERMODYNAMICS** | **Articulate thermo simulator, USNA curriculum since 1996. Dialogue layer added 2006: +0.25 SD over simulator alone, conceptual tests only.** ⚠ **And the 2005 human-tutor study underneath it tied a written script — with tutor-to-tutor variance (100% / 38% / 0%) far larger than the treatment effect.** The precedent nobody cites |
| [AutoTutor](autotutor.md) | Memphis | Various | Expectation/misconception-tailored dialogue |
| [Cognitive Tutor](cognitive-tutor.md) | CMU | Algebra | Source of knowledge tracing, KCs, the doer effect |
| [ALEKS](aleks.md) | UC Irvine → McGraw Hill | Math, chem | Knowledge space theory; state in 20–25 questions |
| [ASSISTments](assistments.md) | WPI | Math | Best-evidenced; E-TRIALS experiment platform |
| [Betty's Brain](bettys-brain.md) | Vanderbilt | Science | Learning by teaching. **Most under-exploited idea here** |
| [OATutor](oatutor-berkeley.md) | UC Berkeley | Math | Open source ITS with BKT. Forkable |

## Reading order for someone new

1. [Jill Watson](jill-watson.md) — the architecture lesson
2. [Stan](stan-udel.md) — the same domain, and what it leaves open for us
3. [CS50 Duck](cs50-duck.md) — the only deployment with good engagement, and why
4. [Khanmigo](khanmigo.md) — the engagement lesson
5. [Andes](andes.md) — what "good" looked like before LLMs
6. [Tutor CoPilot](tutor-copilot.md) and [hybrid human-AI tutoring](hybrid-human-ai-tutoring.md) — the alternative project shape, wired both ways round

← back to [the paper](../PAPER.md) · [knowledge brain index](../README.md)
