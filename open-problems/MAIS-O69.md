# When does the localized posterior estimate the local learning coefficient?

*Open problem MAIS-O69 · posed in [MAIS-A6](../agendas/A6/MAIS-A6.pdf) as [Problem 6.1](../agendas/A6/MAIS-A6.tex#L470) · Status: open.*

*Safety: interpretability, generalization — singular learning theory · developmental interpretability. Mathematics: statistics · probability. Difficulty: ★★ project.*

Local learning coefficients are estimated in practice by sampling from a posterior pinned near the point of interest — inside networks with billions of parameters. But the theorem underpinning the estimator cuts the wrong way: with any fixed localization strength, the Gaussian pin is just another smooth positive prior, so the estimator converges to the global coefficient, not necessarily the local one. How fast must the pin tighten with the sample size?

The estimator (Lau et al., idealized by exact expectations): given empirical loss $L_n(w) = -\frac1n \sum_i \log p(Y_i \mid X_i, w)$, a point $w^*$, and a localization strength $\gamma > 0$, the **localized tempered posterior** is proportional to $\exp(-n\beta^* L_n(w) - \frac{\gamma}{2}\|w - w^*\|^2)$ with $\beta^* = 1/\log n$, and the estimate is $\hat\lambda_n(w^*;\gamma) = \bigl(\mathbb{E}^{\beta^*,\gamma}[\,n L_n(w)\,] - n L_n(w^*)\bigr)/\log n$. The problem poses the simplest model with two components of unequal local complexity, so that global and local answers differ.

**Problem ([MAIS-A6, Problem 6.1](../agendas/A6/MAIS-A6.tex#L470)).** Take $d = 2$, $W = \{w \in \mathbb{R}^2 : \|w\| \le 3\}$, no inputs, model $y \sim N(\mu(w), 1)$ with

$$\mu(w) = (w_1 - 1)\,(w_1^2 + w_2^2)^2,$$

and truth $y \sim N(0,1)$, so that $K(w) = \tfrac12 \mu(w)^2$ and $W_0 = \{w_1 = 1\} \cup \{(0,0)\}$, with local coefficients $\lambda(w) = \tfrac12$ on the segment and $\lambda((0,0)) = \tfrac14$ at the isolated point. Let $w^* = (1,0)$. Determine the sequences $\gamma_n \to \infty$ for which $\hat\lambda_n(w^*; \gamma_n) \to \tfrac12$ in probability, and identify the limit at the transitional scaling.

The two sides of the dichotomy are known. For fixed $\gamma$, Watanabe's WBIC theorem applies with the Gaussian factor as prior and forces $\hat\lambda_n \to \tfrac14$, the global coefficient: the estimator leaks to the more singular point at the origin. For a hard restriction to a small ball around $w^*$, WBIC gives $\hat\lambda_n \to \tfrac12$. The problem asks for the boundary between the two regimes — the growth rate of $\gamma_n$ at which Gaussian localization starts to localize — and the limit on the boundary itself. Definitions and both endpoint arguments are in [MAIS-A6](../agendas/A6/MAIS-A6.pdf).

*Related: [MAIS-O70](MAIS-O70.md) (ground-truth local pairs to calibrate the estimator against) · [MAIS-O61](MAIS-O61.md) (running the estimator on small trained networks) · [MAIS-O63](MAIS-O63.md) (the exact values the estimator would be checked against on modular addition).*
