# On the number of experiments sufficient and in the worst case necessary to identify all causal relations among N variables

*Summary [EGS05] · F. Eberhardt, C. Glymour, and R. Scheines, UAI 2005, 178–184.*

*Tags: world-model discovery · combinatorics · complexity theory · statistics.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** How many experiments does it take to pin down every causal arrow among $N$ variables? If each experiment randomizes at most one variable and the experimenter sees the full joint distribution each time, then $N-1$ experiments always suffice, and against a worst-case graph no fewer will do — adaptivity does not help. Randomizing several variables in one experiment can beat the bound. This is the founding accounting result of experimental causal discovery: not whether the graph is identifiable, but at what price.

## Setting

A causally sufficient set of $N$ variables carries an unknown causal directed acyclic graph, with the faithfulness assumption in force. An **experiment** randomizes a subset of the variables (severing the arrows into them) and returns the resulting joint distribution over all $N$ variables exactly — an idealized infinite-sample regime, so the cost being counted is experiments, not samples. The experimenter may choose each experiment adaptively, in light of everything learned so far, and purely observational data is available as the empty experiment. The question is the minimal number of experiments that guarantees identification of the complete graph: every adjacency and every orientation.

## Main results

1. **Sufficiency.** If each experiment randomizes at most one variable, $N-1$ experiments suffice to identify all causal relations among the $N$ variables.
2. **Worst-case necessity.** No procedure using single-variable experiments, adaptive or not, can guarantee identification with fewer than $N-1$; the complete graph is the obstruction.
3. **Multiple simultaneous interventions escape the bound.** When one experiment may randomize several variables at once, fewer than $N-1$ experiments can suffice, so the linear price is an artifact of the one-variable-at-a-time restriction. (The sharp logarithmic accounting for unrestricted simultaneous interventions came in later work and is not claimed here.)

## Method

Sufficiency is a direct protocol. Randomizing a variable $X$ splits the world in two: within the manipulated distribution, independence tests settle the adjacencies among the other variables, and comparing against the undisturbed distribution reveals which variables respond to $X$ — orienting every edge at $X$. After $N-1$ variables have each taken a turn under randomization, every edge has had an endpoint randomized, and all adjacencies and orientations are settled. Necessity is an adversary argument on the complete graph: all complete DAGs are Markov equivalent, so observation alone orients nothing, and any plan with fewer than $N-1$ single-variable experiments leaves two variables never randomized — the direction of the edge between them remains consistent with the data either way.

## Why it matters for AI safety

For evaluators who would read a black-box agent's world model off its behavior, this paper fixes the classical baseline: even with the enormous advantage of observing *all* variables after each intervention, identification costs a definite, graph-independent number of experiments. [MAIS-A2](../agendas/A2/) transplants the accounting question to the setting of Richens and Everitt [[RE24]](../references/RE24.md), where each experiment returns not a joint distribution but one bit — an optimal agent's action. The agenda's query-complexity problem ([MAIS-O25](../open-problems/MAIS-O25.md)) asks for the analogue of the $N-1$ theorem at that far weaker observation channel, and its restricted-intervention problem ([MAIS-O30](../open-problems/MAIS-O30.md)) echoes the paper's central discovery that *which* variables can be randomized, not just how many times, governs what is identifiable. The gap between the two channels — all variables versus one bit of behavior — is the price of interpretability-by-experiment, and [MAIS-A2](../agendas/A2/) is an attempt to compute it.

## Cited by

- [MAIS-A2](../agendas/A2/) — the classical precedent for its experiment-counting problems: full-observation experiment counts, against which the agenda's one-bit behavioral channel is measured.
- Problems [MAIS-O25](../open-problems/MAIS-O25.md) · [MAIS-O30](../open-problems/MAIS-O30.md)
