# Evaluation

How to measure a tutor, and how to measure a student.

| Node | Measures | Key point |
|---|---|---|
| [TutorGym](tutorgym.md) `[read]` | The **tutor**, inside real ITSs | **No LLM beats chance at spotting an incorrect student step.** 223 domains |
| [MathTutorBench and pedagogy benchmarks](mathtutorbench.md) | The **tutor** | Subject expertise and teaching ability **trade off**. No thermo equivalent exists — **our opening** |
| [Concept inventories](concept-inventories.md) | The **student** | TCI was developed at Penn State. Access is slow — request in Phase 0 |
| [**Behavioral evaluation**](behavioral-evaluation.md) `[read]` | **What the student *did next*** | **Diff consecutive attempts and attribute the edit. Predicts perceived helpfulness better than pedagogical quality — but rewards revealing the answer (79.4% vs 53.0%)** |

## The two-axis problem

Correctness in thermodynamics is covered ([ThermoQA](../domain/thermoqa.md),
[UTQA](../domain/utqa.md)). Learning is measurable ([TCI](concept-inventories.md)).

**Tutoring quality in thermodynamics is measured by nothing.** And the general-domain result
from [TutorGym](tutorgym.md) is the sharpest constraint on our design: models cannot reliably
tell a wrong step from a right one, which is the atomic act of tutoring. That gap is the clearest
novel contribution available to this project, and — because the judges are instructors and
TAs rather than students — it has a much lighter compliance path than anything student-facing.

## The metric trap

[Bastani](../evidence/bastani-2025-harm.md): the arm that performed **+127% during practice**
learned **nothing**. Assisted performance and learning can move in opposite directions.

Any metric we can collect automatically and cheaply — problems solved, time to answer,
satisfaction — is a metric that will flatter us. Decide the primary outcome before collecting
anything. → [open question C3](../../docs/03-open-questions.md)

← back to [the paper](../PAPER.md) · [knowledge brain index](../README.md)
