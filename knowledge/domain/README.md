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
| [UTQA](utqa.md) `[read]` | 50 items (33 text + 17 diagram), 19 models. **Dataset public** | Text mean **67%**, diagram mean **32%**; best overall **82%**; none clears 95% |
| [Superstudent](superstudent-thermodynamics.md) `[read]` | o3 zero-shot on a real German exam **with diagrams** | Outscored all **90** students; failure rate was 58%. Not flawless — see node |
| [Loubet et al.](thermo-problem-benchmark.md) | 22 problems, 5 models, 3 runs, **diagrams removed** | Advanced problems: best **55.2%**. **Every model** assumed reversibility, **every time** |

## The two walls

| Node | The problem |
|---|---|
| [Diagram reading](diagram-reading.md) | Mean **32%** vs. 67% text — but the range is **6% to 76%**. Model-specific, not a universal wall |
| [Property data tools](property-data-tools.md) | Models memorize steam tables and can't interpolate. Use CoolProp. **Watch the reference state** |

## The three things to remember

1. **Peak capability is superhuman; reliability is not.** o3 aces the exam and every model
   fails a third of R-134a problems. Tutoring is a worst-case discipline.
2. **The deepest failure is unstated assumptions**, not arithmetic. Every model conflates
   adiabatic with isentropic. It's the same error our students make, and it's the most
   valuable thing a tutor could teach.
3. **Models are good at thermodynamic computation and mostly bad at thermodynamic seeing —
   with reasoning models the exception.** That sentence reconciles the benchmark literature,
   and it means model choice matters here in a way it doesn't elsewhere.

← back to [the paper](../PAPER.md) · [knowledge brain index](../README.md)
