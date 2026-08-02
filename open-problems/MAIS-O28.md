# Causal model identifiability under average-case regret

*Open problem MAIS-O28 · posed in [MAIS-A2](../agendas/A2/) as [Problem 4.7](../agendas/A2/MAIS-A2.tex#L306) · Status: open.*

*Tags: interpretability · world-model discovery · eliciting latent knowledge · black-box evaluation · bounded rationality · probability · statistics. Difficulty: ★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Extraction theorems ground a safety hope: that an evaluator with only behavioral access can recover the causal world model an agent's competence presupposes. The theorem of Richens and Everitt [[RE24]](../references/RE24.md) assumes an agent that is near-optimal in *every* tampered environment: generically, a policy family with regret at most $\delta$ on every intervened, partially masked task determines an approximate causal model of the environment, with error $O(\delta)$ in the conditional probability tables. Trained agents are not like that: in the experiments of Richens, Abel, Bellot, and Everitt [[RABE25]](../references/RABE25.md), the agents fail some tasks outright, violating any worst-case regret bound — yet the models extracted from their behavior are accurate. The theory behind that observation does not yet exist in the interventional setting. What does identifiability look like when the agent is merely good on average?

The framework is a binary causal influence diagram. A skeleton $\mathsf{s}=(\mathbf{C},\mathbf{O},\mathbf{Z},u)$ fixes a finite set $\mathbf{C}$ of binary chance variables, the subset $\mathbf{O}\subseteq\mathbf{C}$ the agent observes, and a known utility $u(d,z)\in[0,1]$ of a single binary decision $d$ and the values $z$ of the utility parents $\mathbf{Z}\subseteq\mathbf{C}$; a model $M=(G,\theta)$ is a directed acyclic graph $G$ on $\mathbf{C}$ together with its conditional probability tables $\theta$. The margin class $\mathcal{M}(\mathsf{s},\lambda)$ excludes the degenerate models: every probability, utility gap, and edge strength is bounded away from zero at scale $\lambda$, with the exact conditions listed in [MAIS-A2](../agendas/A2/). A shifted task is a pair $(\sigma,\mathbf{O}')$ of a mixture $\sigma$ of local interventions (a **profile** fixes, flips, or leaves each variable; a mixture applies a random profile drawn from a fixed probability vector) and an observation mask $\mathbf{O}'\subseteq\mathbf{O}$. A policy $\pi$ maps each observed value of the visible variables $\mathbf{O}'$ to the probability that the decision is $1$; $\mathrm{reg}_M^{\mathbf{O}'}(\pi;\sigma)$ is the policy's shortfall from the best achievable expected utility on that task; and a policy family $\Pi=(\pi_{\sigma,\mathbf{O}'})$ assigns a policy to every shifted task. The identified set of $M$ under a given admissibility notion consists of the models sharing some admissible family with $M$, and its worst-case radius $\varphi$ (equal to $1$ when the graph is wrong, and otherwise to the largest absolute error in any table entry) is the reconstruction accuracy no analyst can beat.

**Problem ([MAIS-A2, Problem 4.7](../agendas/A2/MAIS-A2.tex#L306)).** Fix the probability measure $\nu$ on the shifted tasks defined by drawing two profiles uniformly, a weight $q$ uniformly from $[0,1]$, and a mask $\mathbf{O}'\subseteq\mathbf{O}$ uniformly. Call a policy family $\Pi$ *$(\kappa,\delta)$-admissible* for $M$ if

$$\nu\lbrace (\sigma,\mathbf{O}'):\mathrm{reg}_M^{\mathbf{O}'}(\pi_{\sigma,\mathbf{O}'};\sigma)>\delta\rbrace \le\kappa.$$

Define the identified set and radius $\varphi(\delta,\kappa;\mathsf{s},\lambda)$ as before with this admissibility. Determine $\varphi(\delta,\kappa)$ up to constants; in particular determine the threshold below which the exception mass still leaves the graph identified, and the rate at which $\varphi(0,\kappa)\to0$ as $\kappa\to0$.

In words: the agent may have regret above $\delta$ on a set of tasks of $\nu$-measure up to $\kappa$, with no guarantee at all there, and the problem asks how the irreducible ambiguity depends jointly on $\delta$ and $\kappa$. The measure $\nu$ is declared rather than canonical; a solution for any explicit non-degenerate $\nu$ counts as a full success, and the dependence on $\nu$ is itself part of the geometry. In the goal-based (rather than interventional) setting, Nayebi [[N26]](https://arxiv.org/abs/2603.02491) has proved a recovery theorem from low average-case regret over an explicit goal family; the interventional version posed here remains open. See [MAIS-A2](../agendas/A2/) for the formalism.

## References

- [[RE24]](../references/RE24.md) J. Richens and T. Everitt, *Robust agents learn causal world models*, ICLR 2024. [arXiv:2402.10877](https://arxiv.org/abs/2402.10877)
- [[RABE25]](../references/RABE25.md) J. Richens, D. Abel, A. Bellot, and T. Everitt, *General agents contain world models*, ICML 2025. [arXiv:2506.01622](https://arxiv.org/abs/2506.01622)
- [N26] A. Nayebi, *What capable agents must know: selection theorems for robust decision-making under uncertainty*, preprint. [arXiv:2603.02491](https://arxiv.org/abs/2603.02491)

*Related: [MAIS-O27](MAIS-O27.md) (the worst-case regret floor) · [MAIS-O29](MAIS-O29.md) (a different model of imperfection: Boltzmann noise) · [MAIS-O2](MAIS-O2.md) (the sampled-action headline problem).*
