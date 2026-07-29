# Coping with errors in binary search procedures

*Summary [RMKWS80] · R. L. Rivest, A. R. Meyer, D. J. Kleitman, K. Winklmann, and J. Spencer, Journal of Computer and System Sciences 20(3) (1980), 396–404.*

*Tags: black-box evaluation · complexity theory · combinatorics · probability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Binary search survives lies. To identify an unknown value by comparison questions when up to $E$ of the answers may be false, roughly $\log_2 n + E\log_2\log_2 n$ questions are necessary and sufficient: each tolerated lie costs an additive $\log\log n$, not a multiplicative factor. The lies are persistent, not channel noise — re-asking a question can draw the same false answer — so repetition buys nothing, and the searcher must instead budget for errors inside the search itself. This is the founding quantitative result on the Rényi–Ulam problem of searching with lies.

## Setting

A responder holds an unknown value $x$, either an integer in $\{1,\dots,n\}$ or a real number to be located within a prescribed tolerance. The questioner asks comparison questions "Is $x \le c$?" and the responder answers, with the guarantee only that at most $E$ answers over the whole game are erroneous, for a bound $E$ known in advance. The responder is adversarial: answers may be chosen against the questioner's strategy, subject to some value of $x$ remaining consistent with all but at most $E$ of them. The cost is the worst-case number of questions.

The state of such a game is not a single candidate interval but a list of them: the values consistent with the answers assuming $0,1,\dots,E$ lies so far. A question is useful insofar as it shrinks this whole configuration, and the design problem is to choose comparisons that make progress against every consistent lie pattern at once.

## Main results

1. **Discrete search.** The minimum worst-case number of comparison questions that identifies $x\in\{1,\dots,n\}$ despite up to $E$ erroneous answers is $\log_2 n + E\log_2\log_2 n + O(E\log E)$, with matching upper and lower bounds. For fixed $E$ the penalty over error-free binary search is thus an additive $E\log_2\log_2 n$.
2. **Continuous search.** The analogous problem of locating a real number to relative accuracy $\varepsilon$ has the same answer with $\log_2(1/\varepsilon)$ in place of $\log_2 n$.
3. **Comparisons suffice.** The bounds are matched using comparison questions only; restricting the questioner from arbitrary yes–no questions to threshold questions costs nothing at this order.

## Method

A potential argument in the style of Berlekamp's theory of error-correcting communication with feedback. Each candidate value is weighted according to how many lies the responder has already spent on it and how many questions remain, and the total weight measures how far the game is from over. The questioner asks the comparison that splits the total weight as evenly as a threshold can; whichever answer comes back, the weight roughly halves, and the game ends when the weight forces a unique candidate. The lower bound is the mirror image: an adversary who always keeps the heavier half of the weight survives the stated number of questions. The ordering of the candidates is what makes the near-even threshold split available, and is why comparison questions lose nothing.

## Why it matters for AI safety

Behavioral world-model discovery keeps reducing, in its one-dimensional core, to locating a threshold from unreliable yes–no data: the switching surface of a near-optimal policy, probed one sampled action at a time. When the deviations from optimality are adversarial and persistent rather than fresh noise, repetition is worthless and the correct model regime is exactly this paper's — a bounded budget of lies, spent by an adversary who knows the search strategy. [RMKWS80] supplies the endpoint result for that regime: recovery is still possible, at additive rather than multiplicative cost. The open question is what its analogue looks like when the object being searched for is not one threshold but a causal model coupled across many of them; that is the subject of [MAIS-A2](../agendas/A2/).

## Cited by

- [MAIS-A2](../agendas/A2/) — the lie-tolerant endpoint of the one-dimensional search engine behind its sampled-action recovery problems.
- Problems [MAIS-O2](../open-problems/MAIS-O2.md) · [MAIS-O33](../open-problems/MAIS-O33.md)
