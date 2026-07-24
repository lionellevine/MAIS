# Causal model identifiability under average-case regret

*Open problem MAIS-O28 · posed in [MAIS-A2](../agendas/A2/MAIS-A2.pdf) as [Problem 4.7](../agendas/A2/MAIS-A2.tex#L305) · Status: open.*

*Safety: interpretability — world-model extraction · eliciting latent knowledge · black-box evaluation · bounded rationality. Mathematics: probability · statistics. Difficulty: ★★ project.*

The extraction theorems assume an agent that is near-optimal in *every* tampered environment. Trained agents are not like that: in the experiments of Richens, Abel, Bellot, and Everitt, the agents fail some tasks outright, violating any worst-case regret bound — yet the models extracted from their behavior are accurate. The theory behind that observation does not yet exist in the interventional setting. What does identifiability look like when the agent is merely good on average?

The framework is a binary causal influence diagram: models $M=(G,\theta)$ in a margin class $\mathcal{M}(\mathsf{s},\lambda)$ for a skeleton $\mathsf{s}=(\mathbf{C},\mathbf{O},\mathbf{Z},u)$; a shifted task is a pair $(\sigma,\mathbf{O}')$ of a mixture $\sigma$ of local interventions (a **profile** fixes, flips, or leaves each variable; a mixture applies a random profile drawn from a fixed probability vector) and an observation mask $\mathbf{O}'\subseteq\mathbf{O}$; $\mathrm{reg}_M^{\mathbf{O}'}(\pi;\sigma)$ is the policy's shortfall from the best achievable expected utility on that task; and a policy family $\Pi=(\pi_{\sigma,\mathbf{O}'})$ assigns a policy to every shifted task. The identified set of $M$ under a given admissibility notion consists of the models sharing some admissible family with $M$, and its worst-case radius $\varphi$ (measured as $1$ for a wrong graph, else maximum table error) is the reconstruction accuracy no analyst can beat.

**Problem ([MAIS-A2, Problem 4.7](../agendas/A2/MAIS-A2.tex#L305)).** Fix the probability measure $\nu$ on the shifted tasks defined by drawing two profiles uniformly, a weight $q$ uniformly from $[0,1]$, and a mask $\mathbf{O}'\subseteq\mathbf{O}$ uniformly. Call a policy family $\Pi$ *$(\kappa,\delta)$-admissible* for $M$ if

$$\nu\lbrace (\sigma,\mathbf{O}'):\mathrm{reg}_M^{\mathbf{O}'}(\pi_{\sigma,\mathbf{O}'};\sigma)>\delta\rbrace \le\kappa.$$

Define the identified set and radius $\varphi(\delta,\kappa;\mathsf{s},\lambda)$ as before with this admissibility. Determine $\varphi(\delta,\kappa)$ up to constants; in particular determine the threshold below which the exception mass still leaves the graph identified, and the rate at which $\varphi(0,\kappa)\to0$ as $\kappa\to0$.

In words: the agent may have regret above $\delta$ on a set of tasks of $\nu$-measure up to $\kappa$, with no guarantee at all there, and the problem asks how the irreducible ambiguity depends jointly on $\delta$ and $\kappa$. The measure $\nu$ is declared rather than canonical; a solution for any explicit non-degenerate $\nu$ counts as a full success, and the dependence on $\nu$ is itself part of the geometry. In the goal-based (rather than interventional) setting, Nayebi has proved a recovery theorem from low average-case regret over an explicit goal family; the interventional version posed here remains open. See [MAIS-A2](../agendas/A2/MAIS-A2.pdf) for the formalism.

*Related: [MAIS-O27](MAIS-O27.md) (the worst-case regret floor) · [MAIS-O29](MAIS-O29.md) (a different model of imperfection: Boltzmann noise) · [MAIS-O2](MAIS-O2.md) (the sampled-action headline problem).*
