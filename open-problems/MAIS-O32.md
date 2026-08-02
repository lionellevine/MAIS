# Tightness of the 1/n rate for depth-n goal agents

*Open problem MAIS-O32 · posed in [MAIS-A2](../agendas/A2/) as [Problem 4.11](../agendas/A2/MAIS-A2.tex#L351) · Status: open.*

*Tags: interpretability · world-model discovery · eliciting latent knowledge · black-box evaluation · probability · combinatorics. Difficulty: ★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

A theorem of Richens, Abel, Bellot, and Everitt [[RABE25]](../references/RABE25.md) extracts an environment's transition probabilities from an agent that achieves multi-step goals, using no interventions at all: an optimal agent's *first action*, on goals of the form "achieve this transition at most $k$ times in $n$ tries, or else more than $k$ times," reveals binomial medians, and sweeping $k$ pins each transition probability to a window of width $O(1/n)$, where $n$ is the depth of the goals the agent can handle. Is $1/n$ the true resolution limit of goal-based tomography, or an artifact of reading only binomial medians?

The environment is a finite communicating stationary controlled Markov process $E=(\mathbf{S},\mathbf{A},P)$ with $|\mathbf{A}|\ge2$: states $\mathbf{S}$, actions $\mathbf{A}$, transition probabilities $P_{ss'}(a)$, every state reachable from every other. A *composite goal* of depth at most $n$ is a finite disjunction of sequences of up to $n$ sub-goals, each demanding that a designated set of state–action pairs be hit now, next, or eventually, in order; $\boldsymbol{\Psi}_n$ is the (finite) set of these, and the problem is insensitive to the exact temporal-logic convention. A deterministic goal-conditioned agent $\pi$ is *$(\delta,n)$-bounded* if for every goal $\psi\in\boldsymbol{\Psi}_n$ and start state its success probability is at least $(1-\delta)$ times the best achievable; $A(E,n,\delta)$ is the set of such agents. All information available to any analyst is the first-action map $f_\pi\colon\mathbf{S}\times\boldsymbol{\Psi}_n\to\mathbf{A}$; writing $\mathcal F(E,n,\delta)=\lbrace f_\pi:\pi\in A(E,n,\delta)\rbrace $ and $d_\infty(P,P')=\max_{s,a,s'}|P'_{ss'}(a)-P_{ss'}(a)|$, the resolution limit is

$$\varepsilon^\ast (E,n,\delta):=\sup\bigl\lbrace d_\infty(P,P'):\ E'=(\mathbf{S},\mathbf{A},P')\ \text{communicating},\ \mathcal F(E,n,\delta)\cap\mathcal F(E',n,\delta)\neq\emptyset\bigr\rbrace ,$$

the error no analyst can beat however many first actions it inspects. The Richens–Abel–Bellot–Everitt theorem [[RABE25]](../references/RABE25.md) gives $\varepsilon^\ast (E,n,0)=O(1/n)$; myopic agents give $\varepsilon^\ast (E,1,0)=1$ for suitable $E$, when the depth-one class is defined by *next* goals alone.

**Problem ([MAIS-A2, Problem 4.11](../agendas/A2/MAIS-A2.tex#L351)).** Determine the asymptotics of $\varepsilon^\ast (E,n,0)$ as $n\to\infty$ for fixed $E$: is $n\ \varepsilon^\ast (E,n,0)$ bounded away from $0$ and $\infty$ whenever some transition probability of $E$ lies strictly between $0$ and $1$? A positive answer to the lower half means constructing, for each $n$, a single depth-$n$ optimal goal-conditioned policy shared by two environments whose transition probabilities differ by $c/n$; a negative one would mean that the full lattice of composite goals pins the model more tightly than the binomial medians the known extractor reads.

The certification framework of Lu, Wu, Lu, and Li [[LWLL26]](https://arxiv.org/abs/2606.24842) (*World models in pieces*) certifies transition by transition which entries of a general agent's world model are reliable, and proves a matching per-transition tightness result for its own small-$\delta$ bound; whether that tightness construction gives $\liminf_n n\ \varepsilon^\ast (E,n,0)>0$ here is the first thing for a solver to check. For the goal formalism and the Richens–Abel–Bellot–Everitt theorem, see [MAIS-A2](../agendas/A2/).

## References

- [[RABE25]](../references/RABE25.md) J. Richens, D. Abel, A. Bellot, and T. Everitt, *General agents contain world models*, Proc. 42nd International Conference on Machine Learning (ICML), 2025. [arXiv:2506.01622](https://arxiv.org/abs/2506.01622)
- [LWLL26] Y. Lu, Y. Wu, X. Lu, and T. Li, *World models in pieces: structural certification for general agents*, preprint, 2026. [arXiv:2606.24842](https://arxiv.org/abs/2606.24842)

*Related: [MAIS-O33](MAIS-O33.md) (corruption-robust extraction in the same setting) · [MAIS-O2](MAIS-O2.md) (the interventional counterpart) · [MAIS-O28](MAIS-O28.md) (average-case regret, where goal-based extraction has advanced first).*
