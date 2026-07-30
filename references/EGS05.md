# On the number of experiments sufficient and in the worst case necessary to identify all causal relations among N variables

*Summary [EGS05] · F. Eberhardt, C. Glymour, and R. Scheines, UAI 2005, 178–184.*

*Tags: world-model discovery · combinatorics · complexity theory · statistics.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** How many experiments does it take to pin down every causal arrow among $N$ variables? If each experiment randomizes at most one variable, the sharp worst-case answer is $N-1$. If any subset may be randomized simultaneously, it falls to $\lfloor\log_2 N\rfloor+1$ experiments: $\log_2N+1$ when $N$ is a power of two and $\lceil\log_2N\rceil$ otherwise. These idealized bounds assume exact knowledge of every conditional independence after each intervention.

## Setting

A causally sufficient set of $N$ variables carries an unknown causal directed acyclic graph, with the faithfulness assumption in force. An **experiment** randomizes a subset of the variables (severing the arrows into them) and returns the resulting joint distribution over all $N$ variables exactly — an idealized infinite-sample regime, so the cost being counted is experiments, not samples. The experimenter may choose each experiment adaptively, in light of everything learned so far, and purely observational data is available as the empty experiment. The question is the minimal number of experiments that guarantees identification of the complete graph: every adjacency and every orientation.

## Main results

1. **Single-variable interventions.** If each experiment randomizes at most one variable, $N-1$ experiments suffice, and the complete graph shows that no adaptive procedure can guarantee fewer.
2. **Unrestricted simultaneous interventions.** If any number of variables may be randomized independently in one experiment, the sharp worst-case count is $\lfloor\log_2 N\rfloor+1$. The intervention sets can be chosen so that every pair of variables is separated by an intervention in at least one experiment and is also observed together, or separated in the opposite direction, in another.
3. **Restricted simultaneous interventions.** If at most $k_{\max}<N/2$ variables may be randomized at once, the paper gives a matching worst-case count
   $$\left\lceil \frac{N}{k_{\max}}-1+\frac{N}{2k_{\max}}\log_2 k_{\max}\right\rceil,$$
   with the evident rounding conventions when the displayed terms are not integral.

## Method

The key bookkeeping is pairwise. To determine the relation between two variables, an experiment must intervene on one but not the other to test direction, while some experiment must also leave both passive or intervene in the opposite direction to distinguish an incoming edge from no edge. Single-variable interventions perform these tests one vertex at a time, giving the $N-1$ bound. Simultaneous interventions encode each variable by the binary pattern of experiments in which it is randomized; distinct patterns separate every pair, yielding the logarithmic construction. Complete DAGs supply the matching worst cases because observational data alone leave all their edge directions unresolved.

## Why it matters for AI safety

An evaluator may try to infer a black-box agent's world model by changing its environment and watching its choices. This paper gives a best-case baseline for the number of such interventions: it assumes the evaluator sees the entire post-intervention distribution exactly, yet the allowed size of an intervention changes the worst-case count from linear to logarithmic. [MAIS-A2](../agendas/A2/) asks for corresponding bounds when a query reveals only an agent's action, and when only some environmental variables can be changed.

## Cited by

- [MAIS-A2](../agendas/A2/) — the classical precedent for its experiment-counting problems: full-observation experiment counts, against which the agenda's one-bit behavioral channel is measured.
- Problems [MAIS-O25](../open-problems/MAIS-O25.md) · [MAIS-O30](../open-problems/MAIS-O30.md)
