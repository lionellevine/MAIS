# Bisection attains optimal query complexity for causal model extraction

*Open problem MAIS-O26 · posed in [MAIS-A2](../agendas/A2/) as [Conjecture 4.4](../agendas/A2/MAIS-A2.tex#L284) · Status: open.*

*Tags: interpretability · world-model discovery · eliciting latent knowledge · black-box evaluation · complexity theory · statistics. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

How many yes-or-no questions does it take to read a causal model out of an optimal agent's behavior? The answer prices behavioral interpretability: the number of experiments an auditor must spend to learn what a black-box agent believes about its world. Information theory sets the floor: a model with $K$ free table entries, each to be recovered to accuracy $\varepsilon$, costs $\Omega(K\log(1/\varepsilon))$ queries by a packing argument (the agenda's Remark 3.3). The natural algorithm bisects: each query asks for the agent's action in a mixture of two intervened environments, the action switches at a critical mixing weight, and the weight encodes an interventional probability. The conjecture is that this simple scheme is optimal up to constants.

The setting is the agenda's query-complexity problem (its Problem 4.3, page [MAIS-O25](MAIS-O25.md)), in the framework of finite causal influence diagrams with $m$ binary chance variables and known utility: the agent observes some variables, takes a binary action, and is scored; a model is a directed acyclic graph together with its conditional probability tables. The margin class $\mathcal{M}(\mathsf{s},\lambda)$ excludes degeneracies at scale $\lambda$ — no vanishing table entry, edge effect, or utility gap, and nothing the agent sees settles its decision in advance. The conjecture restricts further to the subclass $\mathcal{M}(\mathsf{s},\lambda,\mu)$ of the agenda's Problem 4.2 (page [MAIS-O24](MAIS-O24.md)), where explicit polynomial margins of size $\mu$ make behavior determine the model with Lipschitz constant $L$: two models sharing a family of policies of regret at most $\delta$ in every intervened environment, observation masks included, agree to error $L\delta$.

A query names such an environment — a mixture of intervention profiles, with part of the agent's observation masked — and asks the exact probability that an optimal policy plays action $1$ there; exact optimality makes the answer a single bit away from ties, the opening paragraph's yes-or-no questions. The budget $N(\varepsilon)$ is the least number of queries at which some adaptive strategy guarantees expected error at most $\varepsilon$, in graph and tables, against every model of the class.

**Conjecture ([MAIS-A2, Conjecture 4.4](../agendas/A2/MAIS-A2.tex#L284)).** For $\mathcal{N}=\mathcal{M}(\mathsf{s},\lambda,\mu)$ with $\mu$ fixed, $N(\varepsilon)=\Theta\bigl(K\log(1/\varepsilon)\bigr)$ as $\varepsilon\to0$, with the implied constants polynomial in $1/\lambda$, $1/\mu$, and $L$ and independent of $m$ otherwise: bisection along the one-parameter mixture segments of the agenda's Proposition 3.2 achieves the information-theoretic floor of its Remark 3.3 up to constants.

The doubtful half is the upper bound. The known reconstruction is that of Richens and Everitt [[RE24]](https://arxiv.org/abs/2402.10877), whose theorem the agenda's margin classes make quantitative: their algorithm solves for table entries recursively outward from the utility parents, and errors compound through quotients whose denominators are exactly the quantities the margins bound below — hence the powers of $1/\lambda$ and $1/\mu$ in the constants. The conjecture asserts the compounding is polynomial; a proof that it is necessarily exponential in the diagram's depth for some skeletons would refute the conjecture as stated and be equally welcome. For the full margin conditions, the behavioral transform behind the bisection segments, and the packing floor, see [MAIS-A2](../agendas/A2/).

## References

- [RE24] J. Richens and T. Everitt, *Robust agents learn causal world models*, ICLR 2024. [arXiv:2402.10877](https://arxiv.org/abs/2402.10877)

*Related: [MAIS-O25](MAIS-O25.md) (the problem this answers) · [MAIS-O24](MAIS-O24.md) (the polynomial margins assumed) · [MAIS-O2](MAIS-O2.md) (the sampled-action version) · [MAIS-O35](MAIS-O35.md) (test the conjecture on two variables).*
