# Loss frontier for neuron-feature alignment under a bottleneck

*Open problem MAIS-O48 · posed in [MAIS-A4](../agendas/A4/) as [Problem 5.8](../agendas/A4/MAIS-A4.tex#L438) · Status: open.*

*Tags: interpretability · training for interpretability · monosemanticity · optimization · probability. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

A hidden neuron that reads a single feature can be labeled; one that mixes several cannot. What does it cost, in task loss, to demand that every neuron be almost pure — and does the first little bit of impurity buy anything at all?

The model is a two-layer autoencoder whose ReLU hidden layer makes the neuron basis privileged, in the sense of Elhage et al. [[EHOS+22]](../references/EHOS+22.md). Data $x\in\mathbb{R}^m$ has independent coordinates, each zero with probability $S$ and otherwise uniform on $[0,1]$. Parameters are $\theta=(W,\beta,V,c)$ with $W\in\mathbb{R}^{k\times m}$, $\beta\in\mathbb{R}^k$, $V\in\mathbb{R}^{m\times k}$, $c\in\mathbb{R}^m$; the network is $g_\theta(x)=\mathrm{ReLU}\bigl(V\ \mathrm{ReLU}(Wx+\beta)+c\bigr)$ with loss $L'_{m,k,S}(\theta)=\mathbb{E}\ \Vert x-g_\theta(x)\Vert _2^2$. Neuron $j$ has input row $W_{j\cdot}$ and **alignment** $M_j(W)=\max_i W_{ji}^2/\Vert W_{j\cdot}\Vert _2^2$, the fraction of its input weight on its favorite feature; the **monosemanticity index** $M(\theta)$ is the minimum of $M_j$ over nonzero rows ($M=1$ if $W=0$). The agenda proves that when neurons are plentiful ($k\ge m$) the loss is blind to $M$ — perfectly aligned and maximally scrambled networks both reach loss zero — so the question with content is the bottlenecked case $k<m$, where the fully aligned value is exactly $(m-k)\ v(S)$ with $v(S)=(1-S)(1+3S)/12$ the cost of ignoring one feature.

**Problem ([MAIS-A4, Problem 5.8](../agendas/A4/MAIS-A4.tex#L438)).** For $k<m$, $S\in(0,1)$, $\delta\in[0,1]$, define

$$P'_{m,k,S}(\delta) \ =\  \inf\bigl\lbrace \ L'_{m,k,S}(\theta)\ :\ M(\theta)\ge 1-\delta\ \bigr\rbrace ,$$

so that $P'_{m,k,S}(0)=(m-k)\ v(S)$.

1. Determine $\delta^\ast (m,k,S)=\inf\lbrace \delta\in[0,1] : P'_{m,k,S}(\delta)<P'_{m,k,S}(0)\rbrace $, with the convention $\delta^\ast =1$ when the set is empty. Is $\delta^\ast =0$ for all $S$ close to $1$ (any polysemanticity budget helps), or is there a threshold?
2. Jermyn et al. observe monosemantic and polysemantic local minima in a related architecture with randomly projected inputs and a linear unbiased output layer. For the architecture above, exhibit $(m,k,S)$ and two local minima of $L'_{m,k,S}$ with $M=1$ and $M\le\tfrac12$ respectively, whose losses differ by less than $v(S)/10$.

In words: $P'(\delta)$ is the best loss achievable when every neuron must put at least a $1-\delta$ fraction of its squared input weight on one feature, and $\delta^\ast $ is the impurity threshold at which relaxing purity first beats the fully aligned optimum. The reference in part (2) is to Jermyn, Schiefer, and Hubinger [[JSH22]](../references/JSH22.md), who find both kinds of local minima in their (differently wired) toy model and engineer monosemanticity by steering which kind training finds. Part (2) asks for nearby monosemantic and polysemantic local minima in this specific architecture, the situation in which training dynamics, not loss values, decide legibility. The closest theory so far, a rate–distortion–polysemanticity tradeoff proved by Mencattini, Montagna, and Locatello [[MML26]](https://arxiv.org/abs/2605.14694) for a post-hoc sparse autoencoder with a linear decoder, does not determine the frontier $P'_{m,k,S}$ of the jointly trained ReLU-output network here. The plentiful-regime propositions and the bottleneck computation are in [MAIS-A4](../agendas/A4/).

## References

- [[JSH22]](../references/JSH22.md) A. S. Jermyn, N. Schiefer, and E. Hubinger, *Engineering monosemanticity in toy models*, arXiv preprint (2022). [arXiv:2211.09169](https://arxiv.org/abs/2211.09169)
- [MML26] T. Mencattini, F. Montagna, and F. Locatello, *The Rate-Distortion-Polysemanticity Tradeoff in SAEs*, arXiv preprint (2026). [arXiv:2605.14694](https://arxiv.org/abs/2605.14694)
- [[EHOS+22]](../references/EHOS+22.md) N. Elhage, T. Hume, C. Olsson, N. Schiefer, et al., *Toy models of superposition*, Transformer Circuits Thread (2022). [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)

*Related: [MAIS-O4](MAIS-O4.md) (the analogous frontier with coherence in place of alignment) · [MAIS-O50](MAIS-O50.md) (part 3 asks what gradient flow selects for $M$) · [MAIS-O49](MAIS-O49.md) (wiring sparsity, a sibling legibility constraint) · [MAIS-O60](MAIS-O60.md) (single-neuron alignment in a different model organism).*
