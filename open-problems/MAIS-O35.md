# Finite-sample recovery of two-variable causal models

*Open problem MAIS-O35 · posed in [MAIS-A2](../agendas/A2/) as [Problem 5.3](../agendas/A2/MAIS-A2.tex#L382) · Status: open.*

*Tags: interpretability · world-model discovery · eliciting latent knowledge · black-box evaluation · statistics · probability. Difficulty: ★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Radon's inversion formula became tomography when it acquired error bars and dose budgets. For world-model discovery — reading a causal model out of an agent's near-optimal behavior — the inversion step is a theorem of Richens and Everitt [[RE24]](https://arxiv.org/abs/2402.10877): any policy that stays near-optimal across a rich family of interventions on its environment determines an approximate causal model of that environment. The two-variable environment is a scanner small enough to build first: how many sampled actions determine whether $X$ causes $Y$ or $Y$ causes $X$, and to how many digits?

The **two-variable family** $\mathcal{M}_2(\lambda)$, exactly quantified in the agenda's [Definition 5.1](../agendas/A2/MAIS-A2.tex#L372): chance variables $X,Y$; the agent observes nothing, chooses a binary action $d$, and is paid a known utility $u(d,x,y)$ whose action gap $u(1,x,y)-u(0,x,y)$ is bounded away from zero, takes both signs, and is sensitive to each variable; the model is either $X\to Y$ (parameters $a=P(X{=}1)$, $b_x=P(Y{=}1\mid X{=}x)$) or $Y\to X$, with all parameters in $[\lambda,1-\lambda]$ and edge strength at least $\lambda$. A query names a rational mixture $\sigma$ of the sixteen intervention profiles; the adversary has pre-committed a regret-$\delta$ policy for each mixture, and the answer is one action sampled from it; corruption at level $\zeta$ flips each returned action independently with probability $\zeta$. Two quantities from the companion problem [MAIS-O34](MAIS-O34.md): $r_M(\delta)$, the radius of the set of models sharing a regret-$\delta$ policy family with $M$ (the ambiguity no budget removes), and the switching surfaces, the mixtures at which an optimal agent is indifferent. $H$ denotes binary entropy.

**Problem ([MAIS-A2, Problem 5.3](../agendas/A2/MAIS-A2.tex#L382)).** For $\mathcal{M}_2(\lambda)$ restricted to a compact locus on which $r_M(\delta)\le L\delta$ for all sufficiently small $\delta$, prove matching upper and lower bounds for the sampled-action budget $N(\varepsilon,\delta)$ needed to output the graph and all three parameters within $\varepsilon$. Begin at $\delta=0$, where only queries exactly on a switching surface can randomize, and then determine the crossover at positive regret between sampling error and the radius $\sup_M r_M(\delta)$. Finally add independent response corruption at level $\zeta$ and determine whether its sharp cost is the capacity factor $1/(1-H(\zeta))$.

Here "within $\varepsilon$" is minimax and in expectation: $N(\varepsilon,\delta)$ is the least budget at which some analyst strategy guarantees expected error at most $\varepsilon$ against every model in the locus and every admissible adversary. The one-dimensional core interpolates between binary search and Bernoulli regression: at $\delta=0$ every answer off a switching surface is a deterministic bit; positive regret lets the agent randomize on a band around each surface, so estimation error competes with the irreducible radius $r_M(\delta)$; and the corrupted channel carries at most $1-H(\zeta)$ bits per action, whence the conjectured factor — the same capacity cost that governs noisy binary search [KK07].

The agenda pairs this with a fully specified computational project: sample a thousand models from $\mathcal{M}_2(0.1)$, run the bisection extractor against optimal, adversarially $\delta$-optimal, and Boltzmann agents at budgets $2^4$ through $2^{14}$, with corruption at $\zeta\in\lbrace 0,0.05,0.2\rbrace $, and fit the error exponents — the empirical shape of the curves this problem asks to prove, and the problem family's first data. For the family, the query models, and the project specification, see [MAIS-A2](../agendas/A2/).

## References

- [RE24] J. Richens and T. Everitt, *Robust agents learn causal world models*, ICLR 2024. [arXiv:2402.10877](https://arxiv.org/abs/2402.10877)
- [KK07] R. M. Karp and R. Kleinberg, *Noisy binary search and its applications*, SODA 2007, 881–890.

*Related: [MAIS-O34](MAIS-O34.md) (the exact identified set this problem samples toward) · [MAIS-O2](MAIS-O2.md) (the general problem this grounds) · [MAIS-O29](MAIS-O29.md) (Boltzmann agents in general).*
