# Does gradient flow on S₅ select randomly among representation sets?

*Open problem MAIS-O57 · posed in [MAIS-A5](../agendas/A5/) as [Problem 5.7](../agendas/A5/MAIS-A5.tex#L296) · Status: open.*

*Safety: interpretability — mechanistic interpretability · universality of circuits · training dynamics. Mathematics: probability · dynamical systems · representation theory. Difficulty: ★★★ hard.*

Chughtai, Chan, and Nanda trained the same width-128 network on multiplication in $S_5$ from four random seeds and read off the irreducible representations visible in its outputs: two seeds gave {sign, standard}, one added a 5-dimensional representation, one added standard⊗sign and a 5-dimensional. Is that variation genuine randomness in the limiting ensemble, or a finite-training artifact that longer runs would wash out? No symmetry can force the variation: the outer automorphism group of $S_5$ is trivial, so no automorphism identifies one candidate outcome with another.

The ensemble $\mathcal{T}(S_5, \mathrm{ReLU}, 128, \lambda, \tau)$ is the fully connected setting of those experiments: one hidden layer of 128 neurons, logits $f_\theta(a,b)(c) = \sum_{i=1}^{128} \mathrm{ReLU}(u_i(a)+v_i(b))\ w_i(c)$ with $u_i,v_i,w_i \in \mathbb{R}^{S_5}$, trained by gradient flow (read as a differential inclusion, per measurable selection of Clarke trajectories) on the cross-entropy loss over the full multiplication table plus weight decay $\lambda\Vert \theta\Vert ^2$, from independent $N(0,\tau^2)$ coordinates. Write $\mathcal{R}(S_5)$ for the six nontrivial irreducible representations of $S_5$; the **key set** $K_\varepsilon(\theta)$ is the set of those whose characters, evaluated at $abc^{-1}$, carry at least an $\varepsilon$ fraction of the centered logits' $L^2$ norm, and $\mu_t$ is the distribution of $K_\varepsilon(\theta(t))$, for Lebesgue-almost every small $\varepsilon$.

**Problem ([MAIS-A5, Problem 5.7](../agendas/A5/MAIS-A5.tex#L296)).** Consider the ensembles $\mathcal{T}(S_5, \mathrm{ReLU}, 128, \lambda, \tau)$. Prove or refute: for some $\lambda, \tau > 0$ there exist two subsets $S \neq S'$ of $\mathcal{R}(S_5)$ with

$$\liminf_{t \to \infty} \mu_t(\lbrace S\rbrace ) > 0 \quad\text{and}\quad \liminf_{t \to \infty} \mu_t(\lbrace S'\rbrace ) > 0.$$

In words: at some decay strength and initialization scale, training charges at least two distinct representation sets with probability bounded away from zero for all late times. The seed data suggest the candidates $S = \lbrace \mathrm{sgn}, \mathrm{std}\rbrace $ and $S' = S \cup \lbrace \text{a 5-dimensional}\rbrace $. The static half of non-identifiability is known in a neighboring regime: for quadratic activation and squared loss on abelian tasks, Tian constructs abundant inequivalent zero-loss circuits. The dynamical half — that gradient flow from Gaussian initialization actually charges two key sets — is proved for no group and no architecture. For the surrounding definitions and results, see [MAIS-A5](../agendas/A5/).

*Related: [MAIS-O5](MAIS-O5.md) (part (b) asks whether the limiting law is a point mass) · [MAIS-O55](MAIS-O55.md) (the $S_3$ warm-up) · [MAIS-O59](MAIS-O59.md) (randomness of selection in the smallest case).*
