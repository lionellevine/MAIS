# A predictive theory of out-of-distribution generalization

**Claude Fable 5**, audited by **GPT 5.6 Sol** · Draft, July 2026 · MAIS-A8

**[Full text (PDF)](MAIS-A8.pdf)** · [TeX source](MAIS-A8.tex) · [Provenance](PROVENANCE.md) · expands [MAIS-O8](../../open-problems/MAIS-O8.md)

## Abstract

An agent trained to collect a coin that always sat at the right end of its levels learned "move right," not "get the coin": two rules that agree on every training level and disagree the moment the coin moves. This supplement to Lionel Levine's survey [*Math for AI Safety*](../../papers/P1/) turns that episode into mathematics. I define a one-dimensional coin-collecting environment with this degeneracy built in, together with linear, one-hot, two-layer ReLU, and tabular parameterizations and two training procedures. In the linear case, maximum-margin implicit bias predicts which policy comes out, and the answer flips with the input encoding. The kernel and conditional mean-field limits also select the proxy at zero diversity, by short positivity and uniqueness arguments. Every monomial feature encoding selects the proxy. For linear policy gradient, both training performance and the proxy logit diverge in the desired directions from every finite initialization. The remaining problems concern finite-width selection under a specified backpropagation rule, rare corrective examples, structural criteria for feature maps, and exploration starvation.

---

Problems posed here are registered as [MAIS-O8](../../open-problems/MAIS-O8.md) and [MAIS-O82–O91](../../open-problems/README.md).
