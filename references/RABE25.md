# General agents contain world models

*Summary [RABE25] · J. Richens, D. Abel, A. Bellot, and T. Everitt, ICML 2025 · [arXiv:2506.01622](https://arxiv.org/abs/2506.01622).*

*Tags: interpretability · world-model discovery · eliciting latent knowledge · black-box evaluation · probability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Any agent that competently achieves multi-step goals must have learned a predictive model of its environment: the transition probabilities can be recovered from the agent's policy alone, with error shrinking as the depth of the goals the agent can handle grows and degrading gracefully in its failure rate. This is the companion to Richens–Everitt [[RE24]](RE24.md) with the interventions removed — no ability to tamper with the environment is needed, only the agent's choices on a family of goals — and it comes with a sharp exemption: myopic agents, competent only at depth-one goals, reveal nothing.

## Setting

The environment is a finite communicating stationary controlled Markov process: finite state and action sets (at least two actions), transition probabilities $P_{ss'}(a)$ constant in time, every state reachable from every other. Goals are built from sub-goals demanding that a designated state–action set be hit *now*, *next*, or *eventually*; a sequential goal chains sub-goals in order, a composite goal is a finite disjunction, and its **depth** is the number of stages. A goal-conditioned agent maps history–goal pairs to actions, and it is $(\delta,n)$-bounded if it achieves every composite goal of depth at most $n$, from every start state, with probability at least $(1-\delta)$ times the best achievable — a multiplicative failure rate, not a utility difference.

## Main results

1. **Extraction (Theorem 1).** A $(\delta,n)$-bounded agent with $n>1$ and $\delta<1$ determines, from its policy alone, an estimate of every transition probability with error at most $\sqrt{2P_{ss'}(a)(1-P_{ss'}(a))/((n-1)(1-\delta))}$; for small $\delta$ and large $n$ the error refines to $O(\delta/\sqrt n)+O(1/n)$. It is goal depth, not low regret, that drives the error to zero: an agent that fails half its tasks but handles deep goals pins the model tightly.
2. **Myopic exemption (Theorem 2).** From an agent optimal for all depth-one *Next* goals, no nontrivial bound on any transition probability follows: action-independent environments realize values near either endpoint consistently with the same choices. Depth one is exactly where the theorem fails.
3. **Experiments.** Models extracted from trained agents are accurate even though those agents fail some goals outright, violating any worst-case competence bound — empirical evidence for an average-case version of the theorem that is not yet proved.

## Method

The discovery algorithm poses either–or goals: "first action $a$ commits you to achieving this transition at most $k$ times in $n$ tries; any other first action, to more than $k$." An optimal agent chooses whichever commitment is more likely to succeed, so its first action reveals whether $k$ lies above or below the median of the binomial distribution counting successes in $n$ tries; sweeping $k$ locates that median, which pins the transition probability to within $O(1/n)$. The algorithm needs roughly $n$ goals per transition, about $|\mathbf S|^2|\mathbf A|\,n$ queries in all, and only the agent's first action on each.

## Why it matters for AI safety

Together with [[RE24]](RE24.md), this is the second inversion formula behind behavioral world-model discovery — and the more deployable of the two, since an auditor can pose goals without any power to intervene on the environment. It says that generality itself is informative: an agent cannot become broadly competent at long-horizon tasks while keeping its picture of the world private, and the better it gets, the more its behavior gives away. The theorem consumes an oracle for the agent's true policy; the finite-sample theory — how many sampled actions buy how many digits, whether the $1/n$ resolution is tight, how much corruption the extraction tolerates, and what replaces the worst-case competence bound when the agent is only good on average — is the subject of [MAIS-A2](../agendas/A2/).

## Cited by

- [MAIS-A2](../agendas/A2/) — develops the finite-sample side of the extraction theorem: query complexity, rate tightness, corruption robustness.
- Problems [MAIS-O28](../open-problems/MAIS-O28.md) · [MAIS-O32](../open-problems/MAIS-O32.md) · [MAIS-O33](../open-problems/MAIS-O33.md)
