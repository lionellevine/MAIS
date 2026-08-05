# Recovering world-models from behavior

**Claude Fable 5**, audited by **GPT 5.6 Sol** · Draft, July 2026 · MAIS-A2

**[Full text (PDF)](MAIS-A2.pdf)** · [TeX source](MAIS-A2.tex) · [Provenance](PROVENANCE.md) · expands [MAIS-O2](../../open-problems/MAIS-O2.md)

## Abstract

Two theorems of Richens and coauthors show that a sufficiently capable agent cannot keep its picture of the world to itself: any policy that stays near-optimal across a rich family of interventions on its environment determines an approximate causal model of that environment, and any policy that achieves long multi-step goals determines an approximate transition model. Both proofs are constructive, but their extraction algorithms assume oracle access to an entire policy family. This note develops the finite-sample side of the story, as posed in the Open Problem "Recovering world-models from behavior" of Lionel Levine's survey [*Math for AI Safety*](../../papers/P1/). I set up the framework from scratch for the simplest nontrivial case — finite causal influence diagrams with binary variables and known utility — reduce the extraction theorems there to the inversion of an explicit finite "behavioral transform," and state precise open problems on: replacing the theorems' measure-zero genericity by explicit margin conditions; the query complexity of extraction when each experiment returns an action sampled from a stochastic policy; the error floor imposed by an agent's regret (its shortfall from the best achievable score); what restricted intervention sets identify; and finite-sample and corruption-robust versions of the multi-step-goal theorem. A starter case is specified in full, together with a computational project. The final section explains what an activation-intervention theorem would still need to define.

---

Problems posed here are registered as [MAIS-O2](../../open-problems/MAIS-O2.md) and [MAIS-O23–O35](../../open-problems/README.md).
