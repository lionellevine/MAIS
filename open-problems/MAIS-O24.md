# Explicit polynomial margins replacing generic causal identifiability

*Open problem MAIS-O24 · posed in [MAIS-A2](../agendas/A2/MAIS-A2.pdf) as [Problem 4.2](../agendas/A2/MAIS-A2.tex#L265) · Status: open.*

*Safety: interpretability — world-model extraction · eliciting latent knowledge · black-box evaluation. Mathematics: algebraic geometry · probability · complexity theory. Difficulty: ★★ project.*

The theorem behind behavioral world-model extraction — near-optimal adaptation to all local interventions determines the agent's causal model — holds for almost every parameter choice, with the exceptions described only as the vanishing locus of polynomials arising in the proof. Finite-sample statements need more: an explicit, efficiently checkable hypothesis in place of "almost every." This problem asks for the polynomials by name.

The objects: a skeleton $\mathsf{s}=(\mathbf{C},\mathbf{O},\mathbf{Z},u)$ fixes $m$ binary chance variables, an observation set, utility parents, and a known utility; a model $M=(G,\theta)$ is a directed acyclic graph with conditional probability tables, and $K(G)=\sum_i 2^{|\mathrm{Pa}_G(C_i)|}$ counts the free table entries ($K$ is its maximum over the class). The margin class $\mathcal{M}(\mathsf{s},\lambda)$ imposes six explicit non-degeneracy conditions at scale $\lambda$. The behavioral transform $\boldsymbol\Delta_M$ is the finite family of $g$-weighted, observation-sliced interventional probabilities whose sign data is optimal behavior; the identified set $I_\delta(M)$ consists of the models sharing some regret-$\delta$ policy family with $M$; and the error $e(M;M')$ is $1$ if the graphs differ and otherwise the maximum entrywise table difference.

**Problem ([MAIS-A2, Problem 4.2](../agendas/A2/MAIS-A2.tex#L265)).** For each diagram shape $(\mathbf{C},\mathbf{O},\mathbf{Z})$ and each compatible graph $G$, exhibit a finite explicit list of rational polynomials $Q^G_1,\dots,Q^G_r$ in $(\theta,u)$. With $S=K(G)+2^{|\mathbf{Z}|}$, require the list length, degrees, coefficient bit lengths, and construction time to be polynomial in $S$ (using sparse monomial encoding). Find constants $a,b>0$ depending only on $(m,S)$ such that for all $\lambda,\mu\in(0,\tfrac12)$, on the subclass $\mathcal{M}(\mathsf{s},\lambda,\mu):=\{M\in\mathcal{M}(\mathsf{s},\lambda): |Q^G_j(\theta,u)|\ge\mu \text{ for all } j,\text{ where } G \text{ is } M\text{'s own graph}\}$:

1. $\boldsymbol\Delta_M=\boldsymbol\Delta_{M'}$ implies $M=M'$;
2. quantitatively, $M'\in I_\delta(M)$ implies $e(M;M')\le (K/\lambda\mu)^{a}\,\delta$ for all $\delta$ below an explicit threshold;
3. the excluded set is small: for each fixed graph $G$ and Lebesgue-almost-every $u$, $\mathrm{Leb}\bigl\{\theta: |Q^G_j(\theta,u)|<\mu \text{ for some } j\bigr\}\le S^{a}\mu^{b}$.

In words: identical behavior forces identical models on the subclass, nearly optimal behavior pins the model to within a constant times the regret, and the models sacrificed to get this are few. The rest of the agenda's finite-sample theory is posed relative to a solution. Classical causal discovery made the same move once before: strong faithfulness replaces a measure-zero assumption by an explicit margin, and Uhler, Raskutti, Bühlmann, and Yu showed the excluded set can be surprisingly large — a caution aimed directly at part 3. For the margin conditions and the transform, see [MAIS-A2](../agendas/A2/MAIS-A2.pdf).

*Related: [MAIS-O23](MAIS-O23.md) (the qualitative question the list would settle) · [MAIS-O25](MAIS-O25.md) (query complexity built on this subclass) · [MAIS-O2](MAIS-O2.md) (the sampled-action headline problem).*
