# Which interventions identify which parts of the causal graph?

*Open problem MAIS-O30 · posed in [MAIS-A2](../agendas/A2/) as [Problem 4.9](../agendas/A2/MAIS-A2.tex#L326) · Status: open.*

*Tags: interpretability · world-model discovery · eliciting latent knowledge · black-box evaluation · combinatorics · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Richens and Everitt [[RE24]](https://arxiv.org/abs/2402.10877) proved that a causal model of the environment can be read off an agent's optimal behavior, and their proof supplies an algorithm. That algorithm anchors itself with hard interventions on *every* environment variable at once. A real experimenter can usually tamper with only a few. Which arrows of the graph, and which probability tables, can still be read off the agent's behavior when the intervenable set shrinks?

The framework, from [MAIS-A2](../agendas/A2/), is a binary causal influence diagram: the unknown model $M=(G,\theta)$ is a directed acyclic graph $G$ on a finite set $\mathbf{C}$ of binary chance variables — free to vary, so edge presence is genuinely unknown — together with its conditional probability tables $\theta$. The agent observes a fixed subset $\mathbf{O}\subseteq\mathbf{C}$, makes a single binary decision $D$, and is scored by a known utility $u(D,\mathbf{Z})$ with utility-parent set $\mathbf{Z}\subseteq\mathbf{C}$; a policy maps observed values to the probability of deciding $D=1$. Models range over a margin class $\mathcal{M}(\mathsf{s},\lambda)$, where the skeleton $\mathsf{s}$ records $(\mathbf{C},\mathbf{O},\mathbf{Z},u)$ and the class bounds every degeneracy — table entries, edge effects, utility gaps — away from zero by an explicit $\lambda$. $\mathrm{Anc}(U)$ denotes the chance ancestors of the utility, the largest set any behavioral method can hope to recover (on the margin class, all of $\mathbf{C}$).

For $W\subseteq\mathbf{C}$, let $\Sigma_W$ be the mixtures of intervention profiles that act as the identity outside $W$ (so $\Sigma_\emptyset$ is pure observation); a profile hard-sets or negates the mechanisms of the variables it touches while the others keep running. These change the environment's mechanisms, as opposed to observation masks $\mathbf{O}'\subseteq\mathbf{O}$, which change only what the agent sees. A functional $T(M)$ is **$\Sigma_W$-identifiable** at $M$ if $T$ is constant on the models of $\mathcal{M}(\mathsf{s},\lambda)$ sharing an optimal-policy family with $M$ — a policy of maximal expected utility for each intervened, masked task — for every $\sigma\in\Sigma_W$ and every mask $\mathbf{O}'\subseteq\mathbf{O}$: no second model in the class exhibits the same optimal behavior on every $W$-intervened, masked task while differing in $T$.

**Problem ([MAIS-A2, Problem 4.9](../agendas/A2/MAIS-A2.tex#L326)).** For Lebesgue-almost-every parameter choice, characterize combinatorially — in terms of the graph $G$, the sets $W,\mathbf{O},\mathbf{Z}$ — which edge indicators and which table entries are $\Sigma_W$-identifiable. In particular, exhibit the minimal sets $W$ for which everything on $\mathrm{Anc}(U)$ is identifiable. Compare environmental intervention on observed variables ($W=\mathbf{O}$) with sensory masking alone ($W=\emptyset$).

With $W$ small, the all-variable hard anchors of the Richens–Everitt reconstruction [[RE24]](https://arxiv.org/abs/2402.10877) are unavailable, and it is not even clear that the set of identifiable functionals is monotone in the strength of the margin conditions. The flavor is that of the classical question — how many experiments identify a causal graph (Eberhardt, Glymour, and Scheines [EGS05]) — transplanted from observing all variables to observing one bit of behavior. The margin conditions in full ((M1)–(M6)) and the intervention formalism are in [MAIS-A2](../agendas/A2/).

## References

- [RE24] J. Richens and T. Everitt, *Robust agents learn causal world models*, ICLR 2024. [arXiv:2402.10877](https://arxiv.org/abs/2402.10877)
- [EGS05] F. Eberhardt, C. Glymour, and R. Scheines, *On the number of experiments sufficient and in the worst case necessary to identify all causal relations among N variables*, UAI 2005, 178–184.

*Related: [MAIS-O31](MAIS-O31.md) (the chain with a single intervenable variable, the first test case) · [MAIS-O23](MAIS-O23.md) (identifiability with the full intervention set) · [MAIS-O24](MAIS-O24.md) (explicit margins replacing "almost every").*
