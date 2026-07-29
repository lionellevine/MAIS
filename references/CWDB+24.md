# A is for absorption: studying feature splitting and absorption in sparse autoencoders

*Summary [CWDB+24] · D. Chanin, J. Wilken-Smith, T. Dulka, H. Bhatnagar, S. Golechha, and J. Bloom, 2024 · [arXiv:2409.14507](https://arxiv.org/abs/2409.14507).*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · empirical.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** As a sparse autoencoder's dictionary grows, hierarchical concepts split into finer latents ("math" into "algebra", "geometry", …) — the familiar *feature splitting*. This paper shows the resulting decomposition is not robust: a latent that appears to track a parent concept fails to fire precisely on the inputs where a child latent fires, the parent's direction having been **absorbed** into the child. The authors name the phenomenon *feature absorption*, argue it is a consequence of the sparsity objective whenever the underlying features form a hierarchy, introduce a metric to detect it, measure it across hundreds of language-model SAEs, and find that varying dictionary size or sparsity does not remove it.

## Setting

Sparse autoencoders decompose LLM activations into a dictionary of putatively interpretable latent directions, trained by reconstruction loss plus a sparsity penalty. The running task is first-letter identification: a probe direction for "starts with s" exists in the model, and tokens like "short" instantiate a strict hierarchy — the word-level feature never fires without the first-letter feature. The experiments use Gemma-2-2B residual-stream activations with Gemma Scope SAEs across layers, widths, and sparsity levels, with logistic-regression probes trained on the same activations as the baseline for what a single direction can achieve.

## Main results

1. **Absorption exists and is causal.** SAE latents aligned with the first-letter probe direction fail to activate on specific tokens the probe classifies correctly; ablation experiments on these false negatives show that other latents — typically token-level latents such as one for "short" — carry the first-letter direction there. The seemingly monosemantic parent latent has systematically gerrymandered exceptions.
2. **The mechanism is the sparsity objective.** When a child feature always co-occurs with its parent, folding the parent's direction into the child's latent reconstructs the same activations with fewer active latents; absorption is what optimizing for sparsity produces on hierarchical data, not an artifact of any particular architecture.
3. **It is measurable and widespread.** An absorption-rate metric (the fraction of probe true positives on which an absorbing latent, identified by probe alignment and ablation effect, is responsible for the miss) quantifies the phenomenon across hundreds of SAEs. No SAE latent matched the linear probe's classification performance, and increasing width or sparsity tended to increase absorption rather than cure it.

## Method

Empirical, with a detection pipeline: train logistic-regression probes for the first-letter task; match SAE latents to probes by cosine similarity; collect tokens where the matched latents fail but the probe succeeds; attribute each failure by ablating candidate latents and checking which ones causally carry the classification; score a latent as absorbing when its probe alignment and ablation effect clear fixed thresholds. The absorption rate is then swept across layers, dictionary widths, and sparsity levels.

## Why it matters for AI safety

Safety audits built on sparse autoencoders assume that a latent labeled "starts with s" fires when the concept is present; absorption breaks precisely that assumption, silently and in the direction an auditor cannot see. For this repository the paper supplies the named failure mode that the theory must reproduce: [MAIS-A3](../agendas/A3/) adopts "short" nested in "starts with s" as its canonical example of nested supports, proves that nesting forces merging already for two features — the smallest exact instance of absorption, as a global minimizer of the population objective — and asks for the full phase boundary between recovery and merging that would turn this paper's measurements into thresholds.

## Cited by

- [MAIS-A3](../agendas/A3/) — takes feature absorption as the documented failure mode its recovery/merging phase diagram must explain, and its nested-supports running example from this paper.
- Problems [MAIS-O3](../open-problems/MAIS-O3.md) · [MAIS-O37](../open-problems/MAIS-O37.md) · [MAIS-O41](../open-problems/MAIS-O41.md) · [MAIS-O43](../open-problems/MAIS-O43.md)
