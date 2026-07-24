# Opposing staircases

*Open problem MAIS-O7 · headline problem 7 of the survey [MAIS-P1](../papers/P1/) · canonically formalized in [MAIS-A7](../agendas/A7/) as [Conjecture 3.10](../agendas/A7/MAIS-A7.tex#L366) · Status: open.*

*Safety: generalization — developmental interpretability · singular learning theory · training dynamics. Mathematics: algebraic geometry. Difficulty: ★★ project.*

Gradient flow on a deep linear network descends a staircase: it lingers at a saddle where only the $k$ strongest modes of the target are fitted, then drops to the next. Watanabe's free-energy asymptotics assign a complexity invariant to each stage — the local learning coefficient $\lambda$, which controls generalization on the Bayesian side. The conjecture: as the loss falls down its staircase, $\lambda$ climbs an opposing one, step for step. Proved, it would let singular geometry predict the stages of training in advance — the central hope of developmental interpretability.

The setting: a deep linear network trained on a target of rank $r$, hidden width $H>r$. Gradient flow from a small aligned initialization visits saddle sets $C_0, C_1,\dots$, where $C_k$ consists of parameters realizing only the $k$ strongest modes; the losses along the chain fall, $L_0>L_1>\dots>L_r$. At a saddle the usual learning coefficient is undefined (a saddle has descent directions), so the agenda uses the **two-sided** exponent: the volume of nearby parameters whose loss lies within $\varepsilon$ of the saddle's, above or below, shrinks like $\varepsilon^{\lambda}$. Let $\lambda_k=\inf_{w\in C_k}\lambda(w)$.

**Conjecture ([MAIS-A7, Conjecture 3.10](../agendas/A7/MAIS-A7.tex#L366)).** In this setting, $\lambda_0<\lambda_1<\dots<\lambda_r$ while $L_0>L_1>\dots>L_r$: along the saddle chain that gradient flow visits, the loss falls and the learning coefficient rises, step for step. ($C_k$ is noncompact, so attainment of the infimum is part of the claim.)

In transformer experiments the estimated local learning coefficient climbs as the loss falls through most training stages — most, not all — and on the Bayesian side, exact free-energy asymptotics for the deep linear model give the nonnegative increments the conjecture demands. The deep linear network is the one model where both staircases are explicit, so it is where the correspondence should first be proved or refuted. For the two-sided definition and the time–sample dictionary the conjecture would calibrate, see [MAIS-A7](../agendas/A7/).

*Related: [MAIS-O77](MAIS-O77.md) (the λ-stratification it presupposes) · [MAIS-O78](MAIS-O78.md) (training time versus sample size) · [MAIS-O63](MAIS-O63.md) (learning coefficients of a real task).*
