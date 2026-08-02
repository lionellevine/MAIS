# The implicit bias of gradient descent on separable data

*Summary [SHNGS18] · D. Soudry, E. Hoffer, M. S. Nacson, S. Gunasekar, and N. Srebro, JMLR 19(70):1–57, 2018 · [arXiv:1710.10345](https://arxiv.org/abs/1710.10345).*

*Tags: generalization · simplicity bias · training dynamics · optimization · convex geometry.*

*Summarized by: Claude Fable 5 directed by Lionel Levine.*

**TL;DR.** On linearly separable data, gradient descent on unregularized logistic regression cannot converge — the loss can always be lowered by scaling the weights up — yet its *direction* converges, and to something specific: the maximum-margin (hard-margin SVM) separator, from any initialization. The optimizer, not the loss, selects the classifier; the selection is characterized by a finite convex program; and the directional convergence is only logarithmically fast, which explains why training past zero classification error keeps helping.

## Setting

A dataset $(x_i,y_i)_{i\le N}$ with $y_i\in\{\pm1\}$ is **linearly separable** if some weight vector $w$ has $y_i\,w\cdot x_i>0$ for all $i$. On such data the empirical logistic loss $\sum_i \ell(y_i\,w\cdot x_i)$, $\ell(u)=\log(1+e^{-u})$, has infimum zero but no minimizer: every separating direction drives the loss to zero as $\|w\|\to\infty$, so the loss alone is silent on which separator training produces. The question is what full-batch gradient descent, run from an arbitrary initialization with a sufficiently small constant step size, actually does.

## Main results

1. **Max-margin selection.** The norm $\|w_k\|$ diverges while the direction $w_k/\|w_k\|$ converges to $\hat w/\|\hat w\|$, where $\hat w = \operatorname{argmin}\{\|w\|^2 : y_i\,w\cdot x_i\ge1 \text{ for all } i\}$ is the hard-margin SVM solution. This holds for any initialization and extends beyond the logistic loss to smooth monotone losses with a tight exponential tail.
2. **Refined asymptotics.** The iterates grow as $w_k = \hat w\,\log k + \rho_k$ with the residual $\rho_k$ bounded, so the direction converges only at rate $O(1/\log k)$ — dramatically slower than the loss, which decays as $O(1/k)$.
3. **Why late training helps.** The slow directional convergence means the margin is still improving long after the training error hits zero, giving a precise account of the practice of continuing to optimize the logistic or cross-entropy loss past interpolation, even as validation *loss* may rise.

## Method

Guess-and-verify on the asymptotic form. The ansatz $w_k=\hat w\log k+\rho_k$ is substituted into the gradient-descent recursion; the exponential tail of the loss makes the gradient concentrate, as $\|w_k\|$ grows, on the support vectors (the points achieving the minimal margin), whose Karush–Kuhn–Tucker geometry forces the $\log k$ growth to point along $\hat w$ and confines $\rho_k$ to a bounded set. The convergence rates fall out of the same expansion.

## Why it matters for AI safety

Goal misgeneralization is partly a selection problem: when several linear classifiers fit the training data, which one does gradient descent approach? This theorem answers through the hard-margin support vector machine. [MAIS-A8](../agendas/A8/) applies that answer to a one-dimensional coin-collection model: without disambiguating examples the linear classifier selects “move right,” while any positive fraction of suitable examples changes the maximum-margin solution to “go to the coin.” Extending such predictions to nonlinear networks and finite training times remains open.

## Cited by

- [MAIS-A8](../agendas/A8/) — applies the theorem to a linear coin-collection model and uses it as a benchmark for nonlinear selection questions.
- Problems [MAIS-O8](../open-problems/MAIS-O8.md) · [MAIS-O82](../open-problems/MAIS-O82.md) · [MAIS-O84](../open-problems/MAIS-O84.md) · [MAIS-O85](../open-problems/MAIS-O85.md) · [MAIS-O89](../open-problems/MAIS-O89.md)
