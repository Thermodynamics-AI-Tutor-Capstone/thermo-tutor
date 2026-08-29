# Domain — Thermodynamics

What is specifically true about LLMs and *our* subject. The most immediately actionable
directory in the knowledge base.

## Start here

**→ [LLM capability in thermodynamics](llm-thermodynamics-capability.md)** — the synthesis
that reconciles four apparently contradictory results.

## The benchmarks

| Node | What it is | Headline |
|---|---|---|
| [ThermoQA](thermoqa.md) | 293 open-ended problems, 3 tiers, CoolProp ground truth, 6 models | Composite **94.1%**, but **R-134a 44–63%** for every model |
| [UTQA](utqa.md) | 50 items incl. diagrams, 19 models | Best **82%**; **no model** clears the 95% tutoring bar |
| [Superstudent](superstudent-thermodynamics.md) | o3 zero-shot on a real university exam | Solved **everything** — better than every student since 1985 |
| [Hoffmann et al.](thermo-problem-benchmark.md) | 22 problems, 5 models, 3 runs | **Every model** assumed reversibility where unstated, **every time** |

## The two walls

| Node | The problem |
|---|---|
| [Diagram reading](diagram-reading.md) | **32%** on thermodynamic diagrams vs. 67% text. Often chance |
| [Property data tools](property-data-tools.md) | Models memorize steam tables and can't interpolate. Use CoolProp. **Watch the reference state** |

## The three things to remember

1. **Peak capability is superhuman; reliability is not.** o3 aces the exam and every model
   fails a third of R-134a problems. Tutoring is a worst-case discipline.
2. **The deepest failure is unstated assumptions**, not arithmetic. Every model conflates
   adiabatic with isentropic. It's the same error our students make, and it's the most
   valuable thing a tutor could teach.
3. **Models are good at thermodynamic computation and bad at thermodynamic seeing.** That
   single sentence reconciles the whole benchmark literature.

← back to [the paper](../PAPER.md) · [knowledge brain index](../README.md)
