# Math for AI Safety: Master list of open problems

Each open problem here opens with its AI safety motivation, with a link into the [research agenda](../agendas/) that carries its full context.

Problems listed here are open unless their row says otherwise. First resolution: MAIS-O60, resolved in the negative in August 2026 — nine days after the registry launched. Have you solved one of them? Have a promising line of attack? Want to correct a problem statement? [Open an issue](https://github.com/lionellevine/MAIS/issues/new/choose).

Note: Some of these problems sit deliberately on the easier side, to give mathematicians an entry point into AI safety. That means AI may get you most of the way to a solution. I see this as a feature, not a bug: the goal is to advance AI safety, not to curate problems that resist automation.

Stars indicate estimated difficulty. Problems whose deliverable is a computation rather than a proof are tagged *empirical*.

| # | Problem | Safety | Mathematics | ★ |
|---|---------|--------|-------------|---|
| <a id="mais-o1"></a>MAIS-O1 | [Quantitative bounded Löb](MAIS-O1.md) | cooperative AI, agent foundations | logic, complexity theory | ★★★ |
| <a id="mais-o2"></a>MAIS-O2 | [Behavioral tomography of world-models](MAIS-O2.md) | interpretability | statistics, probability, complexity theory | ★★ |
| <a id="mais-o3"></a>MAIS-O3 | [The geometry and identifiability of superposition](MAIS-O3.md) | interpretability | statistics, optimization, probability | ★★★ |
| <a id="mais-o4"></a>MAIS-O4 | [Training for interpretability](MAIS-O4.md) | interpretability | optimization, convex geometry, probability | ★★★ |
| <a id="mais-o5"></a>MAIS-O5 | [Representation theory of learned circuits](MAIS-O5.md) | interpretability | dynamical systems, probability, representation theory | ★★★ |
| <a id="mais-o6"></a>MAIS-O6 | [Does geometric simplicity force a legible mechanism?](MAIS-O6.md) | interpretability, generalization | algebraic geometry, harmonic analysis | ★★★ |
| <a id="mais-o7"></a>MAIS-O7 | [Opposing staircases](MAIS-O7.md) | generalization | algebraic geometry | ★★ |
| <a id="mais-o8"></a>MAIS-O8 | [A predictive theory of out-of-distribution generalization](MAIS-O8.md) | generalization | probability, optimization, dynamical systems | ★★★ |
| <a id="mais-o9"></a>MAIS-O9 | [Steering Conway's Life from a small seed](MAIS-O9.md) | control | probability, dynamical systems, complexity theory | ★★★ |
| <a id="mais-o10"></a>MAIS-O10 | [Polynomial overhead for Löb's theorem](MAIS-O10.md) | cooperative AI, agent foundations | logic, complexity theory | ★★ |
| <a id="mais-o11"></a>MAIS-O11 | [Does Löb's rule shorten proofs?](MAIS-O11.md) | cooperative AI, agent foundations | logic, complexity theory | ★★★ |
| <a id="mais-o12"></a>MAIS-O12 | [Expansion and diagonalization costs in Peano arithmetic](MAIS-O12.md) | cooperative AI, agent foundations | logic, complexity theory | ★★ |
| <a id="mais-o13"></a>MAIS-O13 | [Provable comparisons between exp-log terms in arithmetic](MAIS-O13.md) | cooperative AI, agent foundations | logic | ★★ |
| <a id="mais-o14"></a>MAIS-O14 | [Bounded Löb at logarithmic proof budgets](MAIS-O14.md) | cooperative AI, agent foundations | logic | ★★★ |
| <a id="mais-o15"></a>MAIS-O15 | [Explicit thresholds in parametric bounded Löb](MAIS-O15.md) | cooperative AI, agent foundations | logic, complexity theory | ★★ |
| <a id="mais-o16"></a>MAIS-O16 | [The FairBot cooperation threshold](MAIS-O16.md) | cooperative AI | logic, computational | ★★ |
| <a id="mais-o17"></a>MAIS-O17 | [Cooperation thresholds over families of bounded agents](MAIS-O17.md) | cooperative AI | logic, complexity theory | ★★ |
| <a id="mais-o18"></a>MAIS-O18 | [Admissible budgets for a bounded Löb axiom](MAIS-O18.md) | cooperative AI, agent foundations | logic | ★★★ |
| <a id="mais-o19"></a>MAIS-O19 | [Soundness of Gödel–Löb logic under polynomial budgets](MAIS-O19.md) | cooperative AI, agent foundations | logic | ★★★ |
| <a id="mais-o20"></a>MAIS-O20 | [A bounded Payor lemma and its cooperation threshold](MAIS-O20.md) | cooperative AI, agent foundations | logic | ★★ |
| <a id="mais-o21"></a>MAIS-O21 | [Is the Löb overhead invariant under polynomial simulation?](MAIS-O21.md) | cooperative AI, agent foundations | logic, complexity theory | ★★ |
| <a id="mais-o22"></a>MAIS-O22 | [A bounded analogue of Solovay's completeness theorem](MAIS-O22.md) | cooperative AI, agent foundations | logic | ★★★ |
| <a id="mais-o23"></a>MAIS-O23 | [Do margins imply behavioral identifiability of causal models?](MAIS-O23.md) | interpretability | algebraic geometry, probability | ★★★ |
| <a id="mais-o24"></a>MAIS-O24 | [Explicit polynomial margins replacing generic causal identifiability](MAIS-O24.md) | interpretability | algebraic geometry, probability, complexity theory | ★★ |
| <a id="mais-o25"></a>MAIS-O25 | [Query complexity of causal model extraction from optimal policies](MAIS-O25.md) | interpretability | complexity theory, statistics | ★★ |
| <a id="mais-o26"></a>MAIS-O26 | [Bisection attains optimal query complexity for causal model extraction](MAIS-O26.md) | interpretability | complexity theory, statistics | ★★ |
| <a id="mais-o27"></a>MAIS-O27 | [How agent regret limits causal model identifiability](MAIS-O27.md) | interpretability | statistics, probability | ★★★ |
| <a id="mais-o28"></a>MAIS-O28 | [Causal model identifiability under average-case regret](MAIS-O28.md) | interpretability | probability, statistics | ★★ |
| <a id="mais-o29"></a>MAIS-O29 | [Estimation rates and query design for Boltzmann agents](MAIS-O29.md) | interpretability | statistics, optimization | ★★ |
| <a id="mais-o30"></a>MAIS-O30 | [Which interventions identify which parts of the causal graph?](MAIS-O30.md) | interpretability | combinatorics, probability | ★★★ |
| <a id="mais-o31"></a>MAIS-O31 | [What one intervenable variable reveals about a causal chain](MAIS-O31.md) | interpretability | probability | ★★ |
| <a id="mais-o32"></a>MAIS-O32 | [Tightness of the 1/n rate for depth-n goal agents](MAIS-O32.md) | interpretability | probability, combinatorics | ★★ |
| <a id="mais-o33"></a>MAIS-O33 | [Tolerable corruption fraction for goal-based model extraction](MAIS-O33.md) | interpretability | complexity theory, combinatorics, probability | ★★★ |
| <a id="mais-o34"></a>MAIS-O34 | [Exact identified set for two-variable causal models](MAIS-O34.md) | interpretability | algebraic geometry, computational | ★ |
| <a id="mais-o35"></a>MAIS-O35 | [Finite-sample recovery of two-variable causal models](MAIS-O35.md) | interpretability | statistics, probability | ★ |
| <a id="mais-o36"></a>MAIS-O36 | [Global ℓ¹ dictionary recovery under independent supports](MAIS-O36.md) | interpretability | probability, optimization, statistics | ★★★ |
| <a id="mais-o37"></a>MAIS-O37 | [Two smeared features: recover, merge, or split](MAIS-O37.md) | interpretability | optimization, probability, convex geometry | ★★★ |
| <a id="mais-o38"></a>MAIS-O38 | [Polynomial sample complexity for dictionary uniqueness with growing sparsity](MAIS-O38.md) | interpretability | combinatorics, statistics | ★★★ |
| <a id="mais-o39"></a>MAIS-O39 | [Does the amortized encoder change the learned dictionary?](MAIS-O39.md) | interpretability | optimization, statistics | ★★★ |
| <a id="mais-o40"></a>MAIS-O40 | [Regular pentagon as global minimizer of a ReLU autoencoder](MAIS-O40.md) | interpretability | optimization, harmonic analysis | ★★★ |
| <a id="mais-o41"></a>MAIS-O41 | [Two-feature phase diagram for ℓ¹ dictionary learning](MAIS-O41.md) | interpretability | optimization, convex geometry | ★ |
| <a id="mais-o42"></a>MAIS-O42 | [Pentagon optimality for a pure ReLU packing energy](MAIS-O42.md) | interpretability | optimization, harmonic analysis | ★★ |
| <a id="mais-o43"></a>MAIS-O43 | [Measure the sparse-autoencoder recovery–merging phase diagram](MAIS-O43.md) | interpretability | computational, statistics | ★ *empirical* |
| <a id="mais-o44"></a>MAIS-O44 | [Does penalizing average interference lower worst-case coherence?](MAIS-O44.md) | interpretability | optimization, harmonic analysis, probability | ★★ |
| <a id="mais-o45"></a>MAIS-O45 | [Does penalizing interference make features recoverable by dictionary learning?](MAIS-O45.md) | interpretability | statistics, optimization, probability | ★★ |
| <a id="mais-o46"></a>MAIS-O46 | [Does lower coherence imply better dictionary recovery?](MAIS-O46.md) | interpretability | statistics, harmonic analysis | ★★ |
| <a id="mais-o47"></a>MAIS-O47 | [Uniqueness of ReLU toy-model minimizers up to symmetry](MAIS-O47.md) | interpretability | optimization, convex geometry | ★★★ |
| <a id="mais-o48"></a>MAIS-O48 | [Loss frontier for neuron-feature alignment under a bottleneck](MAIS-O48.md) | interpretability | optimization, probability | ★★ |
| <a id="mais-o49"></a>MAIS-O49 | [Exact cost of weight sparsity in the ReLU toy model](MAIS-O49.md) | interpretability | optimization, probability, combinatorics | ★★ |
| <a id="mais-o50"></a>MAIS-O50 | [Which minima does gradient flow select from random initialization?](MAIS-O50.md) | interpretability, generalization | dynamical systems, probability, optimization | ★★★ |
| <a id="mais-o51"></a>MAIS-O51 | [The regularized phase diagram of the smallest model](MAIS-O51.md) | interpretability | optimization, probability | ★ |
| <a id="mais-o52"></a>MAIS-O52 | [How many Fourier frequencies do modular-addition networks use?](MAIS-O52.md) | interpretability | probability, dynamical systems, harmonic analysis | ★★★ |
| <a id="mais-o53"></a>MAIS-O53 | [Law of large numbers for neuron representation multiplicities](MAIS-O53.md) | interpretability | probability, representation theory, dynamical systems | ★★★ |
| <a id="mais-o54"></a>MAIS-O54 | [Are selection probabilities proportional to squared representation dimension?](MAIS-O54.md) | interpretability | representation theory, probability | ★★★ |
| <a id="mais-o55"></a>MAIS-O55 | [Neuron purity and representation selection for S_3 networks](MAIS-O55.md) | interpretability | dynamical systems, representation theory, probability | ★★★ |
| <a id="mais-o56"></a>MAIS-O56 | [Vanishing weight decay selects both S_3 representations](MAIS-O56.md) | interpretability | dynamical systems, representation theory, optimization | ★★★ |
| <a id="mais-o57"></a>MAIS-O57 | [Does gradient flow on S_5 select randomly among representation sets?](MAIS-O57.md) | interpretability | probability, dynamical systems, representation theory | ★★★ |
| <a id="mais-o58"></a>MAIS-O58 | [Exchangeability of learned frequencies beyond multiplicative symmetry](MAIS-O58.md) | interpretability | probability, harmonic analysis, dynamical systems | ★★★ |
| <a id="mais-o59"></a>MAIS-O59 | [Two neurons learning mod-5 addition: which frequencies win?](MAIS-O59.md) | interpretability | dynamical systems, probability, harmonic analysis | ★★ |
| <a id="mais-o60"></a>MAIS-O60 | [Does a single ReLU neuron align to one frequency?](MAIS-O60.md) — **resolved** (negative, Aug 2026) | interpretability | dynamical systems, probability, harmonic analysis | ★★ |
| <a id="mais-o61"></a>MAIS-O61 | [Pilot measurement of representation selection in small trained networks](MAIS-O61.md) | interpretability | computational, statistics | ★ *empirical* |
| <a id="mais-o62"></a>MAIS-O62 | [Minimal network width for exact modular addition](MAIS-O62.md) | interpretability, generalization | complexity theory, algebraic geometry, harmonic analysis | ★★ |
| <a id="mais-o63"></a>MAIS-O63 | [Learning coefficients of modular addition](MAIS-O63.md) | interpretability, generalization | algebraic geometry, statistics | ★★★ |
| <a id="mais-o64"></a>MAIS-O64 | [Marginal cost of width for modular-addition networks](MAIS-O64.md) | interpretability, generalization | algebraic geometry, statistics | ★★★ |
| <a id="mais-o65"></a>MAIS-O65 | [Learning coefficients of modular addition under cross-entropy](MAIS-O65.md) | interpretability, generalization | algebraic geometry, statistics | ★★★ |
| <a id="mais-o66"></a>MAIS-O66 | [Generic constancy of learning coefficients over attention teachers](MAIS-O66.md) | interpretability, generalization | algebraic geometry, statistics | ★★★ |
| <a id="mais-o67"></a>MAIS-O67 | [Learning coefficients of one-head softmax attention](MAIS-O67.md) | interpretability, generalization | algebraic geometry, statistics | ★★★ |
| <a id="mais-o68"></a>MAIS-O68 | [Learning coefficients of linear attention](MAIS-O68.md) | interpretability, generalization | algebraic geometry, statistics, computational | ★★ |
| <a id="mais-o69"></a>MAIS-O69 | [When does the localized posterior estimate the local learning coefficient?](MAIS-O69.md) | interpretability, generalization | statistics, probability | ★★ |
| <a id="mais-o70"></a>MAIS-O70 | [Local learning coefficients of reduced-rank regression](MAIS-O70.md) | interpretability, generalization | algebraic geometry, statistics | ★★ |
| <a id="mais-o71"></a>MAIS-O71 | [Free energy asymptotics for continuous-input ReLU networks](MAIS-O71.md) | interpretability, generalization | algebraic geometry, probability, statistics | ★★★ |
| <a id="mais-o72"></a>MAIS-O72 | [Finiteness and frontier condition for learning-coefficient strata](MAIS-O72.md) | generalization | algebraic geometry | ★★★ |
| <a id="mais-o73"></a>MAIS-O73 | [Eyring–Kramers law for singular wells](MAIS-O73.md) | generalization | probability, algebraic geometry | ★★★ |
| <a id="mais-o74"></a>MAIS-O74 | [Eyring–Kramers prefactor for a singular well and Morse gate](MAIS-O74.md) | generalization | probability, algebraic geometry | ★★ |
| <a id="mais-o75"></a>MAIS-O75 | [Entropic selection between two flat strata on the torus](MAIS-O75.md) | generalization | probability | ★★ |
| <a id="mais-o76"></a>MAIS-O76 | [SGD limit diffusions on a singular set of minimizers](MAIS-O76.md) | generalization | probability, algebraic geometry | ★★★ |
| <a id="mais-o77"></a>MAIS-O77 | [Learning coefficients on the matrix factorization fiber and saddles](MAIS-O77.md) | generalization | algebraic geometry | ★★ |
| <a id="mais-o78"></a>MAIS-O78 | [A time-sample correspondence for the deep linear network](MAIS-O78.md) | generalization | statistics, probability | ★★★ |
| <a id="mais-o79"></a>MAIS-O79 | [Saddles as effective minima under coarse-graining](MAIS-O79.md) | generalization | dynamical systems, algebraic geometry | ★★★ |
| <a id="mais-o80"></a>MAIS-O80 | [Is leap complexity determined by singularity data?](MAIS-O80.md) | generalization | algebraic geometry, combinatorics | ★★★ |
| <a id="mais-o81"></a>MAIS-O81 | [Does a saddle have a well-defined free energy?](MAIS-O81.md) | generalization | statistics, algebraic geometry | ★★★ |
| <a id="mais-o82"></a>MAIS-O82 | [Wide networks select the proxy policy with probability one](MAIS-O82.md) | generalization | probability, optimization | ★★★ |
| <a id="mais-o83"></a>MAIS-O83 | [Does some finite-width network favor the intended goal?](MAIS-O83.md) | generalization | probability, optimization | ★★★ |
| <a id="mais-o84"></a>MAIS-O84 | [The crossover time and its asymptotics](MAIS-O84.md) | generalization | dynamical systems, optimization, probability | ★★★ |
| <a id="mais-o85"></a>MAIS-O85 | [Which feature maps make the max-margin classifier misgeneralize?](MAIS-O85.md) | generalization | convex geometry, optimization | ★★ |
| <a id="mais-o86"></a>MAIS-O86 | [Does gradient descent match the Gaussian process posterior?](MAIS-O86.md) | generalization | probability, statistics | ★★★ |
| <a id="mais-o87"></a>MAIS-O87 | [Does policy gradient stay misgeneralized despite training diversity?](MAIS-O87.md) | generalization | dynamical systems, probability | ★★ |
| <a id="mais-o88"></a>MAIS-O88 | [Misgeneralization versus diversity for reinforcement learning](MAIS-O88.md) | generalization | probability, dynamical systems | ★★★ |
| <a id="mais-o89"></a>MAIS-O89 | [Boundary-state residual of max-margin gradient descent](MAIS-O89.md) | generalization | optimization, dynamical systems | ★ |
| <a id="mais-o90"></a>MAIS-O90 | [Does finite-width training inherit the kernel flow's selection?](MAIS-O90.md) | generalization | probability, optimization | ★★ |
| <a id="mais-o91"></a>MAIS-O91 | [Numerical atlas of misgeneralization across widths and diversity](MAIS-O91.md) | generalization | computational, probability | ★ *empirical* |
| <a id="mais-o92"></a>MAIS-O92 | [The outcome law of one rectifier neuron](MAIS-O92.md) | interpretability | dynamical systems, probability, harmonic analysis | ★★★ |
