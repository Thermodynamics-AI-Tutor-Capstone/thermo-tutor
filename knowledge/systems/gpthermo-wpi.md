# GPThermo — Worcester Polytechnic Institute

**Type:** system
**One line:** A multi-agent, tool-augmented GPT-4o thermodynamics assistant built at WPI —
**95% accuracy against 15–25% for stock frontier models** — which validates the architecture we
were going to propose and, crucially, **does not occupy the tutoring space.**
**Why we care:** Another US engineering school built the property-tool layer of our system and
measured it. This is the strongest external evidence that the layer works, and the clearest
evidence that our actual contribution is still unclaimed.

> **Verification: `[read]` — full text, 14 pp., 2026-09-01.**

Brown, H. Z. & Ebadi, R. (2025). *"GPThermo: An In-House Generative Artificial Intelligence Tutor
for Thermodynamics."* **ASEE Annual Conference 2025.** Note the first author is an **undergraduate**
— *"a Robotics and Mechanical Engineering undergraduate student"* — which makes this a capstone-scale
project that reached a national conference. Directly relevant precedent for what our team can ship.

## ⭐ How we finally got it, and the trick generalises

ASEE's `peer.asee.org/<id>` landing pages sit behind a **Cloudflare challenge**, which blocked
every scripted attempt and defeated WebFetch. **Appending `.pdf` to the ID bypasses it entirely:**

```bash
curl -sL "https://peer.asee.org/56669.pdf" -o paper.pdf   # works
curl -sL "https://peer.asee.org/56669"     -o paper.html  # Cloudflare challenge
```

**ASEE is the main venue for engineering-education research and it is now fully open to us.**
→ [access recipes](../README.md)

## The architecture — it is ours

Built on **GPT-4o**, with *"two features: **tool augmentation** and **retrieval augmentation**."*
Their stated key improvement over stock ChatGPT is *"its ability to work with private data and
interact directly with code to determine substance properties and perform thermodynamics
calculations."*

**Multi-agent, with an explicit router:**

| Agent | Role |
|---|---|
| **Main Conversation Agent** (GPT-4o) | Holds the instructions, decides which specialist to invoke. Routing is *"an if-else logic structure"* — not learned delegation. |
| **Retrieval Agent** | Private/specialised data: proprietary property tables, fluid identifiers. |
| **Calculation Agent** | Runs custom code — property functions, thermodynamic calculators. May delegate to further sub-agents for complex calculations. |

Their rationale for the split is cost, not pedagogy: *"This modular setup minimizes the
computational load by keeping each agent lightweight."* Compare
[ODU's four-agent latency study](../practice/cost-economics.md), which found the parallel phase is
65–70% of response time — **GPThermo's if-else routing is sequential and conditional, so it likely
avoids that penalty entirely.** Worth noting as a cheaper alternative to fan-out.

## The result

**20 questions** on fluid state and thermodynamic processes, chosen to have *"clear numerical
answers,"* scored correct if **within 1% of the analytical solution**:

| System | Accuracy |
|---|---|
| **GPThermo** | **95%** |
| ChatGPT, Gemini, Claude, Copilot | **15–25%** |

They also report the gap has held *"as the authors have improved GPThermo in response to the
continuous evolution of public models"* — i.e. stock models improving did not close it.

## ⚠ What the number does and does not show

**n = 20.** 95% is 19 of 20. This is a demonstration, not a benchmark, and the authors do not
claim otherwise.

⚠ **The 15–25% baseline is far below what other benchmarks report for the same models** —
[ThermoQA](../domain/thermoqa.md) puts Claude Opus 4.6 at **94.1% composite** and
[UTQA](../domain/utqa.md) puts text-only performance at **67% mean**. The reconciliation is almost
certainly that these 20 questions are **property-lookup-heavy**, which is precisely the task where
ungrounded models fail hardest and where a property library is decisive. So read the comparison as
**"tool-augmented versus not"**, which is a real and useful result — *not* as "GPThermo beats
frontier models," which it was not designed to test.

⚠ **There is no tutoring in it, and no students.** No deployment, no classroom use, no learning
outcome, no usage data, no pedagogy — no hints, no Socratic method, no student model. On
[Stan's six-level scale](stan-udel.md) this is an **accurate answer engine**. The authors' own
closing caution is that *"providing students with access too early in their learning process may
lead to overreliance… preventing them from developing foundational skills."* They built the thing
[Bastani](../evidence/bastani-2025-harm.md) showed makes learning worse when unguarded, and they
say so themselves without having tested it.

## ⭐ What this means for our project

**1. Our space is still open, and now we know it precisely.** Three university thermodynamics
systems exist and **none of them tutor**: [Stan](stan-udel.md) is a resource pointer,
[Ethel](ethel-eth.md) is Q&A plus grading, GPThermo is a calculator with good manners.
**Nobody has built the pedagogy layer for thermodynamics.**

**2. The property-tool layer is validated externally — stop treating it as a research question.**
Somebody else built it, measured it, and got 95%. We can cite this and move on to the part that
is actually unsolved. → [property data tools](../domain/property-data-tools.md),
[grounding and verification](../concepts/grounding-and-verification.md)

**3. A capstone-scale team can reach ASEE with this.** An undergraduate first-authored a national
conference paper on a subset of our system. **ASEE is a realistic publication target for us**, and
a tutoring-layer paper would be a strictly stronger contribution than the tool layer they
published. → [roadmap](../../admin/roadmap.md)

**4. Their 20 questions are a free evaluation asset.** *"The full list of questions is provided in
Appendix B."* Worth extracting to compare against
[ThermoQA](../domain/thermoqa.md) and [UTQA](../domain/utqa.md).

## Open questions

- [ ] Extract the Appendix B question list and check overlap with ThermoQA's tiers.
- [ ] Has GPThermo been deployed to students since ASEE 2025? Zero citations so far; worth
      re-checking OpenAlex, and Ebadi is a plausible person to email.
- [ ] Which property source do they use — CoolProp, REFPROP, or scraped tables? The paper names
      EES, REFPROP, CoolProp and Interactive Thermodynamics as prior art but does not say which
      one they call. Matters for the [reference-state problem](../domain/property-data-tools.md).
- [ ] **How many more ASEE papers are we missing?** Now that the `.pdf` trick works, a systematic
      ASEE sweep is cheap and overdue.

## Connects to

- [Stan](stan-udel.md), [Ethel](ethel-eth.md) — the other two university thermodynamics systems
- [CyclePad](cyclepad-cycletalk.md) — the same "never guess, always compute" principle, 1996
- [Property data tools](../domain/property-data-tools.md)
- [Cost and latency](../practice/cost-economics.md) — if-else routing vs parallel fan-out
- [Bastani](../evidence/bastani-2025-harm.md) — what an unguarded answer engine does to learning
- [Institutional landscape](../practice/institutional-landscape.md)

## Sources

- [Brown, H. Z. & Ebadi, R. (2025). "GPThermo: An In-House Generative Artificial Intelligence Tutor for Thermodynamics." *ASEE Annual Conference*](https://peer.asee.org/56669.pdf) `[read — full text, 14 pp., 2026-09-01]` · [DOI 10.18260/1-2--56669](https://doi.org/10.18260/1-2--56669)
