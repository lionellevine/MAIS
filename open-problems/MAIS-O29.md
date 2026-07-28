# Estimation rates and query design for Boltzmann agents

*Open problem MAIS-O29 · posed in [MAIS-A2](../agendas/A2/) as [Problem 4.8](../agendas/A2/MAIS-A2.tex#L315) · Status: open.*

*Tags: interpretability · world-model extraction · eliciting latent knowledge · black-box evaluation · bounded rationality · statistics · optimization. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Between the optimal agent (noiseless bits) and the adversarially $\delta$-suboptimal agent (irreducible ambiguity) sits the standard model of a noisily rational one: the Boltzmann, or quantal-response, agent, which plays better actions exponentially more often. Extracting a causal model from its sampled actions is a smooth statistics problem rather than an adversarial one — and it comes with a design question: which experiments should the analyst run?

The framework is a binary causal influence diagram: models $M=(G,\theta)$ in a margin class $\mathcal{M}(\mathsf{s},\lambda)$, queried through shifted tasks $(\sigma,\mathbf{O}')$ — a mixture $\sigma$ of local interventions and an observation mask — at observations $w$. The **Boltzmann family** at inverse temperature $\beta>0$ answers with an action drawn from

$$\pi_\beta(1\mid w;\sigma,\mathbf{O}')=\frac{e^{\beta\ E_M^{\mathbf{O}'}(1,w;\sigma)}}{e^{\beta\ E_M^{\mathbf{O}'}(0,w;\sigma)}+e^{\beta\ E_M^{\mathbf{O}'}(1,w;\sigma)}},$$

where $E_M^{\mathbf{O}'}(d,w;\sigma):=\sum_z u(d,z)\ P_M(\mathbf{Z}=z\mid \mathbf{O}'=w;\sigma)$ is the expected utility of action $d$; as $\beta\to\infty$ this recovers optimal play. The minimax risk at budget $N$ is the best worst-case expected error in graph and tables over the class after $N$ sampled actions.

**Problem ([MAIS-A2, Problem 4.8](../agendas/A2/MAIS-A2.tex#L315)).** Under the Boltzmann channel with known $\beta$: (a) decide whether the map from models to Boltzmann behavior is injective on $\mathcal{M}(\mathsf{s},\lambda)$; (b) for each fixed finite $\beta$, determine the minimax risk at budget $N$ up to constants, including the deterioration as $\beta\to0$; then characterize the joint $(N,\beta)$ crossover from the smooth local rate (typically proportional to $1/(\beta\sqrt N)$) to the noiseless adaptive-search regime as $\beta\to\infty$; (c) solve the design problem: which distribution over queries $(\sigma,\mathbf{O}',w)$ maximizes the minimax rate?

For fixed $\beta$, part (b) is smooth parametric estimation, and the econometrics of quantal response (from McKelvey–Palfrey onward) supplies the local analysis. Large $\beta$ creates no regret floor: the channel tends to the noiseless sign oracle, and information near a switching surface initially grows like $\beta^2$. The open content is the non-uniform crossover in (b) and the design problem (c), an optimization over mixtures, masks, and observations. For the query formalism and margin class, see [MAIS-A2](../agendas/A2/).

*Related: [MAIS-O2](MAIS-O2.md) (sampled actions from a $\delta$-optimal adversary instead) · [MAIS-O28](MAIS-O28.md) (average-case regret, another realistic-agent model) · [MAIS-O35](MAIS-O35.md) (the two-variable starter, Boltzmann case included in its computational project).*
