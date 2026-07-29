# The implicit bias of gradient descent on separable data

*Summary [SHNGS18] · D. Soudry, E. Hoffer, M. S. Nacson, S. Gunasekar, and N. Srebro, JMLR 19(70):1–57, 2018 · [arXiv:1710.10345](https://arxiv.org/abs/1710.10345).*

*Tags: generalization · simplicity bias · training dynamics · optimization · convex geometry.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

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

Goal misgeneralization is a selection problem: when several policies fit the training data perfectly, which one does gradient descent pick? This theorem is the one setting where the selection question has a complete answer — a finite convex program computable in advance — and the agenda's coin line is built so that the theorem applies verbatim. There it settles the entire linear chapter: the proxy ("move right") wins at zero training diversity, the intended goal wins at any positive diversity, and the verdict flips with the input encoding, each claim reduced to a max-margin computation with an explicit KKT certificate. The theorem is also the template the agenda asks to extend — to networks, where selection as a function of initialization is open, and to the crossover-time question, where the theorem's own residual asymptotics become the tool. See [MAIS-A8](../agendas/A8/).

## Cited by

- [MAIS-A8](../agendas/A8/) — applies the theorem to settle the linear coin line (proxy at $\varepsilon=0$, goal at $\varepsilon>0$, encoding-dependence), and takes it as the model for what a selection theorem should look like.
- Problems [MAIS-O8](../open-problems/MAIS-O8.md) · [MAIS-O82](../open-problems/MAIS-O82.md) · [MAIS-O84](../open-problems/MAIS-O84.md) · [MAIS-O85](../open-problems/MAIS-O85.md) · [MAIS-O89](../open-problems/MAIS-O89.md)
