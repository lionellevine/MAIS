# Bisection attains optimal query complexity for causal model extraction

*Open problem MAIS-O26 · posed in [MAIS-A2](../agendas/A2/MAIS-A2.pdf) as [Conjecture 4.4](../agendas/A2/MAIS-A2.tex#L283) · Status: open.*

*Safety: interpretability — world-model extraction · eliciting latent knowledge · black-box evaluation. Mathematics: complexity theory · statistics. Difficulty: ★★ project.*

How many yes-or-no questions does it take to read a causal model out of an optimal agent's behavior? Information theory sets the floor: a model with $K$ free table entries, each to be recovered to accuracy $\varepsilon$, costs $\Omega(K\log(1/\varepsilon))$ queries by a packing argument (the agenda's Remark 3.3). The natural algorithm bisects: each query asks for the agent's action in a mixture of two intervened environments, the action switches at a critical mixing weight, and the weight encodes an interventional probability. The conjecture is that this simple scheme is optimal up to constants.

The setting is the agenda's query-complexity problem (its Problem 4.3, page [MAIS-O25](MAIS-O25.md)): models are binary causal influence diagrams $(G,\theta)$ in a margin class $\mathcal{M}(\mathsf{s},\lambda)$, further restricted to the subclass $\mathcal{M}(\mathsf{s},\lambda,\mu)$ on which explicit polynomial margins of size $\mu$ guarantee that behavior determines the model with Lipschitz constant $L$ (the agenda's Problem 4.2); the analyst queries the exact action probabilities of an optimal policy family, and $N(\varepsilon)$ is the minimax budget for recovering graph and tables to error $\varepsilon$. Here $m$ is the number of chance variables.

**Conjecture ([MAIS-A2, Conjecture 4.4](../agendas/A2/MAIS-A2.tex#L283)).** For $\mathcal{N}=\mathcal{M}(\mathsf{s},\lambda,\mu)$ with $\mu$ fixed, $N(\varepsilon)=\Theta\bigl(K\log(1/\varepsilon)\bigr)$ as $\varepsilon\to0$, with the implied constants polynomial in $1/\lambda$, $1/\mu$, and $L$ and independent of $m$ otherwise: bisection along the one-parameter mixture segments of the agenda's Proposition 3.2 achieves the information-theoretic floor of its Remark 3.3 up to constants.

The doubtful half is the upper bound: the known reconstruction solves for table entries recursively outward from the utility parents, and errors compound through quotients whose denominators are the margin quantities. The conjecture asserts the compounding is polynomial; a proof that it is necessarily exponential in the diagram's depth for some skeletons would refute the constant-degree form and be equally welcome. For the subclass, the transform, and the floor, see [MAIS-A2](../agendas/A2/MAIS-A2.pdf).

*Related: [MAIS-O25](MAIS-O25.md) (the problem this answers) · [MAIS-O24](MAIS-O24.md) (the polynomial margins assumed) · [MAIS-O2](MAIS-O2.md) (the sampled-action version) · [MAIS-O35](MAIS-O35.md) (test the conjecture on two variables).*
