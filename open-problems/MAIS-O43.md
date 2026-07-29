# Measure the sparse-autoencoder recovery–merging phase diagram

*Open problem MAIS-O43 · posed in [MAIS-A3](../agendas/A3/) as [Problem 5.3](../agendas/A3/MAIS-A3.tex#L343) · Status: open.*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · computational · statistics · empirical. Difficulty: ★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Where, quantitatively, does a sparse autoencoder stop recovering features and start absorbing them? The theory of that boundary is open ([MAIS-O3](MAIS-O3.md), [MAIS-O36](MAIS-O36.md)); this problem specifies an experiment — synthetic data with a tunable fraction of nested feature pairs — that measures it first. The protocol pins down sample counts, optimizer, and thresholds, and requires publishing seeds and checkpoints.

The data come from a superposition model in the sense of Elhage et al. [[EHOS+22]](https://arxiv.org/abs/2209.10652), $y=\Phi x$: unit feature directions as columns of $\Phi$, sparse nonnegative codes $x$, and nesting meaning a child feature that never fires without its parent — the support pattern proved to force merging in the two-feature case. The objective fit is the amortized sparse-autoencoder objective $G_\lambda(\Psi,W,b)=\mathbb{E}\bigl[\tfrac12\lVert y-\Psi c(y)\rVert^2+\lambda\lVert c(y)\rVert_1\bigr]$ with encoder $c(y)=\mathrm{ReLU}(Wy+b)$, dictionary $\Psi$ with $M$ unit columns; *centered*, in the statement below, means this objective exactly as displayed, with no learned output bias (practical autoencoders often add one).

Reported outcomes use the agenda's Definitions 4.1–4.2, with $v_i$ the columns of $\Phi$; an atom of $\Psi$ is **live** if its code coordinate under $c$ is positive with positive probability (a dead atom can sit anywhere without changing the objective). **Recovery** at tolerance $\varepsilon$: some injection assigns each feature $v_i$ its own atom $u$ with $\langle u,v_i\rangle\ge1-\varepsilon$. A **merge** at $(\varepsilon,\delta)$: a live atom $u$ with $\lVert u-\alpha v_i-\beta v_{i'}\rVert\le\varepsilon$ for some pair $i\neq i'$ and coefficients $\alpha,\beta\ge\delta$, while $\langle u,v_i\rangle$ and $\langle u,v_{i'}\rangle$ are both at most $1-\delta$ — near the positive span of two features, bounded away from each. A **split** at $\delta$: at least two live atoms each with inner product at least $1-\delta$ with the same feature.

**Problem ([MAIS-A3, Problem 5.3](../agendas/A3/MAIS-A3.tex#L343)).** Fix $n=64$, $m=256$, and draw the columns of $\Phi$ independently from $N(0,I_n)$ and normalize them. Fix one random permutation of $[m]$ and pair consecutive entries. For each $\gamma\in\lbrace 0,.1,\dots,1\rbrace $, declare the first $\lfloor128\gamma\rfloor$ pairs nested: draw independent Bernoulli$(1/32)$ variables $B_i$, then replace the child indicator in each declared pair $(i,j)$ by $B_iB_j$. Draw active coefficients independently from $\mathrm{Unif}[1,2]$. For

$$\lambda\in\lbrace 10^{-4},\ 3\cdot10^{-4},\ 10^{-3},\ 3\cdot10^{-3},\ 10^{-2}\rbrace , \qquad M\in\lbrace 128,256,512\rbrace ,$$

fit the centered objective $G_\lambda$ by full-batch Adam (learning rate $10^{-3}$, $\beta_1=.9$, $\beta_2=.999$, numerical stabilizer $10^{-8}$) on $2^{18}$ fixed training samples for $2\cdot10^5$ updates, from $20$ independent parameter initializations. Use $2^{16}$ fresh samples for evaluation; report recovery (agenda Definition 4.1) at $\varepsilon=.05$, merges at $(\varepsilon,\delta)=(.05,.1)$, and splits at $\delta=.05$. Publish the random seeds, samples, checkpoints, and bootstrap $95\%$ confidence intervals for each fraction.

In the sampling step, every feature's indicator starts as its own independent $\mathrm{Bernoulli}(1/32)$ coin $B_i$, and a feature fires exactly when its indicator equals $1$; the child of a declared pair fires only when its own coin and its parent's both come up, so it never fires without its parent.

The payoff is a measured surface: recovery, merge, and split fractions as functions of the nesting fraction $\gamma$, the penalty $\lambda$, and the dictionary size $M$ — turning "sparse autoencoders sometimes absorb features" (the absorption phenomenon documented by Chanin et al. [[CWDB+24]](https://arxiv.org/abs/2409.14507)) into thresholds that the recovery conjecture and the two-feature phase diagram must reproduce. For the model, the definitions, and the propositions the thresholds calibrate, see [MAIS-A3](../agendas/A3/).

## References

- [CWDB+24] D. Chanin, J. Wilken-Smith, T. Dulka, H. Bhatnagar, S. Golechha, and J. Bloom, *A is for absorption: studying feature splitting and absorption in sparse autoencoders*, 2024. [arXiv:2409.14507](https://arxiv.org/abs/2409.14507)
- [EHOS+22] N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread, Anthropic, 2022. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- [PB25] G. Paulo and N. Belrose, *Sparse autoencoders trained on the same data learn different features*, 2025. [arXiv:2501.16615](https://arxiv.org/abs/2501.16615)

*Related: [MAIS-O41](MAIS-O41.md) (the exact two-feature diagram this measures at scale) · [MAIS-O36](MAIS-O36.md) (the recovery conjecture the thresholds inform) · [MAIS-O39](MAIS-O39.md) (whether the amortized objective used here shifts the answer).*
