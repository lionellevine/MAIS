# What one intervenable variable reveals about a causal chain

*Open problem MAIS-O31 · posed in [MAIS-A2](../agendas/A2/) as [Question 4.10](../agendas/A2/MAIS-A2.tex#L332) · Status: open.*

*Tags: interpretability · world-model discovery · eliciting latent knowledge · black-box evaluation · probability. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Take the simplest causal structure there is, a chain $C_m\to C_{m-1}\to\dots\to C_1$ of binary variables, and an agent paid to guess the far end $C_1$ while observing nothing. An analyst may tamper with the chain at a single link $C_j$ and watch how the agent's guess responds. How much of the chain's probability law does that one dial recover?

The framework: a model is the chain graph together with its conditional probability tables — the marginal of the root $C_m$ and a $2\times2$ transition table at each of the $m-1$ edges, hence $2(m-1)+1$ parameters $\theta$. The skeleton $\mathsf{s}$ records the data $(\mathbf{C},\mathbf{O},\mathbf{Z},u)$ fixed in the question below, and for a fixed $\lambda\in(0,\tfrac12)$ the margin class $\mathcal{M}(\mathsf{s},\lambda)$ consists of the models compatible with $\mathsf{s}$ in which every table entry lies in $[\lambda,1-\lambda]$ and every edge has a detectable effect: the two rows of each transition table differ by at least $\lambda$. Conditions (M2)–(M3) on the utility say the guess always matters: writing $g(c)=u(1,c)-u(0,c)$ for the advantage of guessing $1$ over guessing $0$ when $C_1=c$, condition (M2) requires $|g(c)|\ge\lambda$ for both values of $c$, and (M3) requires $g(0)$ and $g(1)$ to have opposite signs, so the optimal guess depends on the law of $C_1$. (The agenda's remaining margin conditions hold automatically on this skeleton.)

Since the agent observes nothing, a policy is a single number in $[0,1]$, the probability of guessing $1$, optimal for a given intervened environment if it maximizes the expected utility there. The intervention formalism is that of Richens and Everitt [[RE24]](https://arxiv.org/abs/2402.10877), whose theorem recovers the whole model from optimal policies for almost every parameter choice when every chance variable is intervenable. For $W\subseteq\mathbf{C}$, an analyst restricted to $W$ may apply any mixture $\sigma\in\Sigma_W$ of local interventions (fix to $0$, fix to $1$, flip, or leave each variable of $W$; for the singleton $W=\lbrace C_j\rbrace $ of the question, a mixture is a probability distribution over these four options at $C_j$) and observe an optimal policy for the resulting task. A parameter is **$\Sigma_W$-identifiable** if it is constant across all models in the class sharing an optimal-policy family with the true one: a single assignment of a policy to each mixture $\sigma\in\Sigma_W$, optimal for both models at every $\sigma$. (The agenda's definition also quantifies over observation masks, vacuous here.)

**Question ([MAIS-A2, Question 4.10](../agendas/A2/MAIS-A2.tex#L332)).** Let $\mathbf{C}=\lbrace C_1,\dots,C_m\rbrace $ with graph the directed path $C_m\to C_{m-1}\to\dots\to C_1$, observation set $\mathbf{O}=\emptyset$, utility parents $\mathbf{Z}=\lbrace C_1\rbrace $, and $u$ with margin (M2)–(M3). For $W=\lbrace C_j\rbrace $, a single intervenable variable: which of the $2(m-1)+1$ table parameters are $\Sigma_W$-identifiable for almost every $\theta$ (comparison class: the models of $\mathcal{M}(\mathsf{s},\lambda)$ carrying this chain graph, so that all the parameters are defined)?

The agenda records a heuristic, labeled as such: mixtures at $C_j$ should reveal the composite transfer map from $C_j$ to $C_1$ — a product of $2\times2$ stochastic matrices — and the observational marginal of $C_1$, but not the individual factors nor anything upstream of $C_j$. Neither half is proved, and the negative half needs a genuine indistinguishability construction: two chains, agreeing in transfer map and marginal, sharing every optimal policy. For the restricted-intervention formalism this instantiates, see [MAIS-A2](../agendas/A2/).

## References

- [RE24] J. Richens and T. Everitt, *Robust agents learn causal world models*, ICLR 2024. [arXiv:2402.10877](https://arxiv.org/abs/2402.10877)
- [EGS05] F. Eberhardt, C. Glymour, and R. Scheines, *On the number of experiments sufficient and in the worst case necessary to identify all causal relations among N variables*, UAI 2005.
- [P09] J. Pearl, *Causality: Models, Reasoning, and Inference*, 2nd ed., Cambridge University Press, 2009.

*Related: [MAIS-O30](MAIS-O30.md) (the general restricted-intervention problem) · [MAIS-O34](MAIS-O34.md) (another small exact case: two variables, all interventions) · [MAIS-O23](MAIS-O23.md) (identifiability with the full intervention set).*
