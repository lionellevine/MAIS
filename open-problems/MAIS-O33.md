# Tolerable corruption fraction for goal-based model extraction

*Open problem MAIS-O33 · posed in [MAIS-A2](../agendas/A2/) as [Problem 4.12](../agendas/A2/MAIS-A2.tex#L356) · Status: open.*

*Tags: interpretability · world-model extraction · eliciting latent knowledge · black-box evaluation · complexity theory · combinatorics · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

An agent whose behavior reveals its world-model may have stable blind spots: a fixed fraction of (state, goal) pairs on which its answers are arbitrary — the same wrong answers every time, not fresh noise. Channel noise is dispatched by repetition at logarithmic cost; persistent corruption cannot be, since re-asking a corrupted question returns the same lie. How large a corrupted fraction can goal-based model extraction survive?

The setting is the goal-based extraction theorem of Richens, Abel, Bellot, and Everitt. The environment is a finite communicating stationary controlled Markov process $E=(\mathbf{S},\mathbf{A},P)$; $\boldsymbol{\Psi}_n$ is the finite set of composite goals of depth at most $n$ (disjunctions of ordered sub-goals demanding designated state–action sets be hit now, next, or eventually); $A(E,n,\delta)$ is the set of deterministic goal-conditioned agents achieving every goal in $\boldsymbol{\Psi}_n$, from every start state, with probability at least $(1-\delta)$ times the best achievable; and all analyst-visible data is the first-action map $f_\pi\colon\mathbf{S}\times\boldsymbol{\Psi}_n\to\mathbf{A}$, queried one argument at a time. Uncorrupted, roughly $|\mathbf{S}|^2|\mathbf{A}|\ n$ such queries recover every transition probability to error $O(1/\sqrt{(n-1)(1-\delta)})$.

**Problem ([MAIS-A2, Problem 4.12](../agendas/A2/MAIS-A2.tex#L356)).** Consider all finite instances $(\mathbf{S},\mathbf{A},n,\delta)$ with $|\mathbf{A}|\ge2$, $n>1$, and $(n-1)(1-\delta)>4$. An *$\eta$-corruption* of an agent $\pi\in A(E,n,\delta)$ is any function $\rho\colon\mathbf{S}\times\boldsymbol{\Psi}_n\to\mathbf{A}$ differing from $f_\pi$ on at most $\eta\ |\mathbf{S}\times\boldsymbol{\Psi}_n|$ arguments, chosen by an adversary who knows the analyst's randomized strategy but commits to $\rho$ before the interaction. Call $\eta$ *uniformly tolerable* if one randomized algorithm and one polynomial $p$ use at most $p(|\mathbf{S}|,|\mathbf{A}|,n)$ queries and achieve, for every such instance, every communicating environment $E$, every $\pi\in A(E,n,\delta)$, and every $\eta$-corruption,

$$\max_{s,a,s'}\ \bigl|\widehat P_{ss'}(a)-P_{ss'}(a)\bigr|\ \le\  \frac{2}{\sqrt{(n-1)(1-\delta)}}
\qquad\text{with probability at least } \tfrac23.$$

Determine $\eta^\ast :=\sup\lbrace \eta:\eta\text{ is uniformly tolerable}\rbrace $. Is $\eta^\ast >0$? The restriction $(n-1)(1-\delta)>4$ removes the regime in which the target error is at least $1$ and the zero-query estimator is already valid.

The problem has teeth: $|\boldsymbol{\Psi}_n|$ is astronomically larger than any polynomial budget, so a fraction-$\eta$ corruption can cover *every* query of a known deterministic analyst. Randomization is forced, and a positive answer requires exhibiting exponentially many interchangeable certificate query sets — a random-self-reducibility property of the goal space. A variant of equal interest measures the corruption budget against the sequential goals only. For the goal formalism, see [MAIS-A2](../agendas/A2/).

*Related: [MAIS-O32](MAIS-O32.md) (the uncorrupted resolution limit in the same setting) · [MAIS-O2](MAIS-O2.md) (independent response corruption in the interventional setting) · [MAIS-O35](MAIS-O35.md) (corruption at the two-variable scale).*
