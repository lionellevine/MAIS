# Explicit polynomial margins replacing generic causal identifiability

*Open problem MAIS-O24 · posed in [MAIS-A2](../agendas/A2/) as [Problem 4.2](../agendas/A2/MAIS-A2.tex#L266) · Status: open.*

*Tags: interpretability · world-model discovery · eliciting latent knowledge · black-box evaluation · algebraic geometry · probability · complexity theory. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

The theorem behind behavioral world-model discovery is due to Richens and Everitt [[RE24]](https://arxiv.org/abs/2402.10877): near-optimal adaptation to all local interventions and observation masks determines the agent's causal model. Their theorem holds for almost every parameter choice, with the exceptions described only as the vanishing locus of polynomials arising in the proof. Finite-sample statements need more: an explicit, efficiently checkable hypothesis in place of "almost every." This problem asks for the polynomials by name.

The objects: a skeleton $\mathsf{s}=(\mathbf{C},\mathbf{O},\mathbf{Z},u)$ fixes $m$ binary chance variables, an observation set $\mathbf{O}\subseteq\mathbf{C}$, utility parents $\mathbf{Z}\subseteq\mathbf{C}$, and a known utility $u$; a compatible model $M=(G,\theta)$ is any directed acyclic graph on the chance variables with its conditional probability tables, and $K(G)=\sum_i 2^{|\mathrm{Pa}_G(C_i)|}$ counts the free table entries ($K$ is its maximum over the margin class). The agent sees the observed variables, picks a binary action $d$, and is scored $u(d,z)$ at the utility-parent values $z$; a policy is regret-$\delta$ if its expected score is within $\delta$ of optimal. A local intervention applies one of the four maps on $\lbrace 0,1\rbrace$ (identity, set to $0$, set to $1$, negate) to a single chance variable; a shifted task pairs a probabilistic mixture of intervention profiles, one map per variable, with a mask hiding some of the observations.

The margin class $\mathcal{M}(\mathsf{s},\lambda)$ imposes six explicit non-degeneracy conditions at scale $\lambda$: with $g(z):=u(1,z)-u(0,z)$ the utility gap, every table entry lies in $[\lambda,1-\lambda]$; $|g|\ge\lambda$ everywhere; $g$ takes both signs among the utility-parent values consistent with each observation; every edge shifts some conditional probability of its head by at least $\lambda$; every chance variable is an observation, a utility parent, or an ancestor of one, and at least one is unobserved; and each utility parent shifts $g$ by at least $\lambda$. The behavioral transform $\boldsymbol\Delta_M$ is the finite family of $g$-weighted, observation-sliced interventional probabilities $\Delta^{\mathbf{O}'}_M(\sigma,w)=\sum_{c:\,c_{\mathbf{O}'}=w} P_M(c;\sigma)\,g(c_{\mathbf{Z}})$, indexed by masks $\mathbf{O}'\subseteq\mathbf{O}$, mixtures $\sigma$, and visible observations $w$; a policy is optimal precisely when it plays $1$ where this quantity is positive and $0$ where it is negative, so the transform's sign data is optimal behavior. A policy family assigns one policy to each shifted task; the identified set $I_\delta(M)$ consists of the models $M'$ admitting a policy family that is regret-$\delta$ for $M$ and $M'$ simultaneously; and the error $e(M;M')$ is $1$ if the graphs differ and otherwise the maximum entrywise table difference.

**Problem ([MAIS-A2, Problem 4.2](../agendas/A2/MAIS-A2.tex#L266)).** For each diagram shape $(\mathbf{C},\mathbf{O},\mathbf{Z})$ and each compatible graph $G$, exhibit a finite explicit list of rational polynomials $Q^G_1,\dots,Q^G_r$ in $(\theta,u)$. With $S=K(G)+2^{|\mathbf{Z}|}$, require the list length, degrees, coefficient bit lengths, and construction time to be polynomial in $S$ (using sparse monomial encoding). Find constants $a,b>0$ depending only on $(m,S)$ such that for all $\lambda,\mu\in(0,\tfrac12)$, on the subclass $\mathcal{M}(\mathsf{s},\lambda,\mu):=\lbrace M\in\mathcal{M}(\mathsf{s},\lambda): |Q^G_j(\theta,u)|\ge\mu \text{ for all } j,\text{ where } G \text{ is } M\text{'s own graph}\rbrace $:

1. $\boldsymbol\Delta_M=\boldsymbol\Delta_{M'}$ implies $M=M'$;
2. quantitatively, $M'\in I_\delta(M)$ implies $e(M;M')\le (K/\lambda\mu)^{a}\ \delta$ for all $\delta$ below an explicit threshold;
3. the excluded set is small: for each fixed graph $G$ and Lebesgue-almost-every $u$, $\mathrm{Leb}\bigl\lbrace \theta: |Q^G_j(\theta,u)|<\mu \text{ for some } j\bigr\rbrace \le S^{a}\mu^{b}$.

In words: identical behavior forces identical models on the subclass, nearly optimal behavior pins the model to within a constant times the regret, and the models sacrificed to get this are few. The rest of the agenda's finite-sample theory is posed relative to a solution. Classical causal discovery made the same move once before: strong faithfulness replaces a measure-zero assumption by an explicit margin, and Uhler, Raskutti, Bühlmann, and Yu [URBY13] showed the excluded set can be surprisingly large — a caution aimed directly at part 3. The margin conditions and the transform appear above in compressed form; their exact quantifiers are in [MAIS-A2](../agendas/A2/).

## References

- [RE24] J. Richens and T. Everitt, *Robust agents learn causal world models*, ICLR 2024. [arXiv:2402.10877](https://arxiv.org/abs/2402.10877)
- [URBY13] C. Uhler, G. Raskutti, P. Bühlmann, and B. Yu, *Geometry of the faithfulness assumption in causal inference*, Annals of Statistics 41 (2013), no. 2, 436–463.
- [P09] J. Pearl, *Causality: Models, Reasoning, and Inference*, 2nd ed., Cambridge University Press, 2009.

*Related: [MAIS-O23](MAIS-O23.md) (the qualitative question the list would settle) · [MAIS-O25](MAIS-O25.md) (query complexity built on this subclass) · [MAIS-O2](MAIS-O2.md) (the sampled-action headline problem).*
