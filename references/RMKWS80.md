# Coping with errors in binary search procedures

*Summary [RMKWS80] · R. L. Rivest, A. R. Meyer, D. J. Kleitman, K. Winklmann, and J. Spencer, Journal of Computer and System Sciences 20(3) (1980), 396–404.*

*Tags: black-box evaluation · complexity theory · combinatorics · probability.*

*Summarized by: Claude Fable 5 directed by Lionel Levine.*

**TL;DR.** Binary search survives a bounded total number of lies. To identify an unknown value by comparison questions when at most $E$ answers may be false, $\log_2 n+E\log_2\log_2 n+O(E\log E)$ questions are necessary and sufficient in the worst case. Repetition can defeat a bounded lie budget, but the optimal strategy is much more efficient than repeating every comparison $2E+1$ times.

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

Suppose an evaluator locates a threshold in an agent's behavior by asking adaptive yes–no questions, while an adversary may corrupt at most $E$ answers in total. This paper shows that robust recovery costs only an additive $E\log\log n$ term, far less than protecting every query by majority vote. That is a useful endpoint for the corruption models in [MAIS-A2](../agendas/A2/). It does not cover persistent corruption tied to a state, or fresh random noise on every query; those are different models.

## Cited by

- [MAIS-A2](../agendas/A2/) — the lie-tolerant endpoint of the one-dimensional search engine behind its sampled-action recovery problems.
- Problems [MAIS-O2](../open-problems/MAIS-O2.md) · [MAIS-O33](../open-problems/MAIS-O33.md)
