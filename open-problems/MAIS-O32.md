# Tightness of the 1/n rate for depth-n goal agents

*Open problem MAIS-O32 · posed in [MAIS-A2](../agendas/A2/MAIS-A2.pdf) as [Problem 4.11](../agendas/A2/MAIS-A2.tex#L350) · Status: open.*

*Safety: interpretability — world-model extraction · eliciting latent knowledge · black-box evaluation. Mathematics: probability · combinatorics. Difficulty: ★★ project.*

A theorem of Richens, Abel, Bellot, and Everitt extracts an environment's transition probabilities from an agent that achieves multi-step goals, using no interventions at all: an optimal agent's *first action*, on goals of the form "achieve this transition at most $k$ times in $n$ tries, or else more than $k$ times," reveals binomial medians, and sweeping $k$ pins each transition probability to a window of width $O(1/n)$, where $n$ is the depth of the goals the agent can handle. Is $1/n$ the true resolution limit of goal-based tomography, or an artifact of reading only binomial medians?

The environment is a finite communicating stationary controlled Markov process $E=(\mathbf{S},\mathbf{A},P)$ with $|\mathbf{A}|\ge2$: states $\mathbf{S}$, actions $\mathbf{A}$, transition probabilities $P_{ss'}(a)$. A *composite goal* of depth at most $n$ is a finite disjunction of sequences of up to $n$ sub-goals, each demanding that a designated set of state–action pairs be hit now, next, or eventually, in order; $\boldsymbol{\Psi}_n$ is the (finite) set of these. A deterministic goal-conditioned agent $\pi$ is *$(\delta,n)$-bounded* if for every goal $\psi\in\boldsymbol{\Psi}_n$ and start state its success probability is at least $(1-\delta)$ times the best achievable; $A(E,n,\delta)$ is the set of such agents. All information available to any analyst is the first-action map $f_\pi\colon\mathbf{S}\times\boldsymbol{\Psi}_n\to\mathbf{A}$; writing $\mathcal F(E,n,\delta)=\{f_\pi:\pi\in A(E,n,\delta)\}$ and $d_\infty(P,P')=\max_{s,a,s'}|P'_{ss'}(a)-P_{ss'}(a)|$, the resolution limit is

$$\varepsilon^*(E,n,\delta):=\sup\bigl\{d_\infty(P,P'):\ E'=(\mathbf{S},\mathbf{A},P')\ \text{communicating},\ \mathcal F(E,n,\delta)\cap\mathcal F(E',n,\delta)\neq\emptyset\bigr\},$$

the error no analyst can beat however many first actions it inspects. The extraction theorem gives $\varepsilon^*(E,n,0)=O(1/n)$; myopic agents give $\varepsilon^*(E,1,0)=1$ for suitable $E$, when the depth-one class is defined by *next* goals alone.

**Problem ([MAIS-A2, Problem 4.11](../agendas/A2/MAIS-A2.tex#L350)).** Determine the asymptotics of $\varepsilon^*(E,n,0)$ as $n\to\infty$ for fixed $E$: is $n\,\varepsilon^*(E,n,0)$ bounded away from $0$ and $\infty$ whenever some transition probability of $E$ lies strictly between $0$ and $1$? A positive answer to the lower half means constructing, for each $n$, a single depth-$n$ optimal goal-conditioned policy shared by two environments whose transition probabilities differ by $c/n$; a negative one would mean that the full lattice of composite goals pins the model more tightly than the binomial medians the known extractor reads.

The certification framework of Lu, Wu, Lu, and Li proves a matching per-transition tightness result for its own small-$\delta$ bound; whether its construction gives $\liminf_n n\,\varepsilon^*(E,n,0)>0$ here is the first thing for a solver to check. For the goal formalism and the extraction theorem, see [MAIS-A2](../agendas/A2/MAIS-A2.pdf).

*Related: [MAIS-O33](MAIS-O33.md) (corruption-robust extraction in the same setting) · [MAIS-O2](MAIS-O2.md) (the interventional counterpart) · [MAIS-O28](MAIS-O28.md) (average-case regret, where goal-based extraction has advanced first).*
