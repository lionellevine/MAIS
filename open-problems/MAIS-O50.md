# Which minima does gradient flow select from random initialization?

*Open problem MAIS-O50 · posed in [MAIS-A4](../agendas/A4/) as [Question 5.10](../agendas/A4/MAIS-A4.tex#L483) · Status: open.*

*Tags: interpretability · generalization · training dynamics · training for interpretability · monosemanticity · superposition · simplicity bias · dynamical systems · probability · optimization. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

When a task has both a legible optimum and a scrambled one at the same loss, the network we get is decided not by minimization but by the optimizer; whether we can read the internals of the model we deploy hangs on that choice. What law does gradient flow from random weights induce on the set of minima?

Both model organisms come from the agenda: the first is the superposition model of Elhage et al. [[EHOS+22]](../references/EHOS+22.md), and the second is motivated by (but not identical to) the monosemanticity-engineering architecture of Jermyn, Schiefer, and Hubinger [[JSH22]](https://arxiv.org/abs/2211.09169). The **ReLU toy model** has data $x\in\mathbb{R}^m$ with independent coordinates, each zero with probability $S$ and otherwise uniform on $[0,1]$; network $f_{W,b}(x)=\mathrm{ReLU}(W^{\top}Wx+b)$, where $W\in\mathbb{R}^{n\times m}$ has columns $W_1,\dots,W_m$; loss $L$ the mean squared reconstruction error, optionally with the $i$th summand weighted by an importance $I_i$; interference penalty $R(W)=\sum_{i\neq j}\langle W_i,W_j\rangle^2$; coherence $\mu(W)$ the largest absolute value of the normalized inner product between distinct nonzero columns. The **privileged-basis autoencoder** is $g_\theta(x)=\mathrm{ReLU}(V\ \mathrm{ReLU}(Wx+\beta)+c)$ with $W\in\mathbb{R}^{k\times m}$, loss $L'$ again the mean squared reconstruction error, and monosemanticity index $M(\theta)\in[1/m,1]$, the minimum over active hidden neurons of the squared-weight fraction on the favorite feature. For $k\ge m$ hidden neurons the agenda proves $L'$ is blind to $M$: zero loss is attained both at a perfectly monosemantic network and at thoroughly scrambled ones, so minimization cannot tell these apart and dynamics alone decides. Since these losses are nonsmooth, "gradient flow" means a fixed Borel-measurable choice of complete Clarke trajectory from each initial condition, with nonconvergent trajectories assigned the cemetery state $\dagger$; the exact conventions and the blindness proposition are in [MAIS-A4](../agendas/A4/).

**Question ([MAIS-A4, Question 5.10](../agendas/A4/MAIS-A4.tex#L483)).** Fix $(m,n,S,\lambda,\sigma)$ and use the measurable Clarke-trajectory convention for $L+\lambda R$, from $W_{ij}\sim N(0,\sigma^2)$ independently and $b=0$. Write $\theta_\infty=\dagger$ when the selected trajectory does not converge.

1. For $(m,n)=(2,1)$ with importance weights $(1,I)$, on convergent trajectories write the limiting row as $(w_1,w_2)$. Determine the probabilities of the four disjoint events
   - $D_2=\lbrace w_2=0,\ w_1\ne0\rbrace $ — drop feature 2,
   - $A_2=\lbrace w_1=0,\ w_2\ne0\rbrace $ — dedicate the dimension to feature 2,
   - $S_{\pm}=\lbrace w_1w_2<0\rbrace $ — store the pair antipodally,
   - $O$ = the complement, including $\theta_\infty=\dagger$,

   computing them as functions of $(I,S,\lambda,\sigma)$.
2. Set $\mu(W_\infty)=+\infty$ when $\theta_\infty=\dagger$. For fixed $(m,n,S,\sigma)$ and $c\in[0,1]$, is $\lambda\mapsto \Pr[\mu(W_\infty)\le c]$ nondecreasing?
3. Fix instead $(m,k,S,\sigma)$ with $k\ge m$ and run the selected Clarke trajectory for $L'$ on $\theta=(W,\beta,V,c)$, initialized with $W_{ij},V_{ij}\sim N(0,\sigma^2)$ independently and both bias vectors zero. Determine the law of $M(\theta_\infty)$ on $[1/m,1]\cup\lbrace \dagger\rbrace $, interpreting $M(\theta_\infty)=\dagger$ on nonconvergent trajectories.

Part (1) asks, in the smallest model, for the probability that training drops the weak feature, dedicates the dimension to it, or stores the pair antipodally, as a function of the importance, sparsity, penalty, and initialization scale. Part (2) asks whether more regularization monotonically raises the chance of landing at coherence at most $c$. Part (3) is the implicit-bias question for interpretability in miniature: when the task cannot tell legible from scrambled, what distribution over monosemanticity does training induce? The closest prior study of these dynamics is Chen, Lau, Mendel, Wei, and Murfet [[CLMWM23]](../references/CLMWM23.md), who follow training of the same ReLU toy model through phase transitions between $k$-gon critical points but do not determine a limit law. The case $m=k=2$ of part (3) is already open.

## References

- [[EHOS+22]](../references/EHOS+22.md) N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread, 2022. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- [JSH22] A. S. Jermyn, N. Schiefer, and E. Hubinger, *Engineering monosemanticity in toy models*, 2022. [arXiv:2211.09169](https://arxiv.org/abs/2211.09169)
- [[CLMWM23]](../references/CLMWM23.md) Z. Chen, E. Lau, J. Mendel, S. Wei, and D. Murfet, *Dynamical versus Bayesian phase transitions in a toy model of superposition*, 2023. [arXiv:2310.06301](https://arxiv.org/abs/2310.06301)

*Related: [MAIS-O51](MAIS-O51.md) (the exact-minimizer phase diagram of the same $(2,1)$ model) · [MAIS-O8](MAIS-O8.md) (gradient descent selecting between two perfect policies) · [MAIS-O48](MAIS-O48.md) (the statics of the monosemanticity index $M$) · [MAIS-O59](MAIS-O59.md) (frequency selection dynamics in a two-neuron network).*
