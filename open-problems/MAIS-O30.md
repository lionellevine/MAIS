# Which interventions identify which parts of the causal graph?

*Open problem MAIS-O30 · posed in [MAIS-A2](../agendas/A2/) as [Problem 4.9](../agendas/A2/MAIS-A2.tex#L325) · Status: open.*

*Safety: interpretability — world-model extraction · eliciting latent knowledge · black-box evaluation. Mathematics: combinatorics · probability. Difficulty: ★★★ hard.*

The known algorithm for extracting a causal model from an agent's behavior anchors itself with hard interventions on *every* environment variable at once. A real experimenter can usually tamper with only a few. Which arrows of the graph, and which probability tables, can still be read off the agent's behavior when the intervenable set shrinks?

The framework is a binary causal influence diagram: models $M=(G,\theta)$ — a directed acyclic graph on binary chance variables $\mathbf{C}$ with conditional probability tables — in a margin class $\mathcal{M}(\mathsf{s},\lambda)$, where the skeleton fixes the agent's observation set $\mathbf{O}$, the utility parents $\mathbf{Z}$, and a known utility; $\mathrm{Anc}(U)$ denotes the chance ancestors of the utility, the largest set any behavioral method can hope to recover. For $W\subseteq\mathbf{C}$, let $\Sigma_W$ be the mixtures of intervention profiles that act as the identity outside $W$ (so $\Sigma_\emptyset$ is pure observation); these change the environment's mechanisms, as opposed to observation masks $\mathbf{O}'\subseteq\mathbf{O}$, which change only what the agent sees. A functional $T(M)$ is **$\Sigma_W$-identifiable** at $M$ if $T$ is constant on the models of $\mathcal{M}(\mathsf{s},\lambda)$ sharing an optimal-policy family with $M$ for every $\sigma\in\Sigma_W$ and every mask $\mathbf{O}'\subseteq\mathbf{O}$.

**Problem ([MAIS-A2, Problem 4.9](../agendas/A2/MAIS-A2.tex#L325)).** For Lebesgue-almost-every parameter choice, characterize combinatorially — in terms of the graph $G$, the sets $W,\mathbf{O},\mathbf{Z}$ — which edge indicators and which table entries are $\Sigma_W$-identifiable. In particular, exhibit the minimal sets $W$ for which everything on $\mathrm{Anc}(U)$ is identifiable. Compare environmental intervention on observed variables ($W=\mathbf{O}$) with sensory masking alone ($W=\emptyset$).

With $W$ small, the all-variable hard anchors of the known reconstruction are unavailable, and it is not even clear that the set of identifiable functionals is monotone in the strength of the margin conditions. The flavor is that of the classical question — how many experiments identify a causal graph (Eberhardt, Glymour, and Scheines) — transplanted from observing all variables to observing one bit of behavior. For the intervention formalism, see [MAIS-A2](../agendas/A2/).

*Related: [MAIS-O31](MAIS-O31.md) (the chain with a single intervenable variable, the first test case) · [MAIS-O23](MAIS-O23.md) (identifiability with the full intervention set) · [MAIS-O24](MAIS-O24.md) (explicit margins replacing "almost every").*
