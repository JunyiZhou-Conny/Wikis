---
title: "Improving Sparse Decomposition of Language Model Activations with Gated Sparse Autoencoders"
type: source
status: done
date: 2026-07-21
source_kind: paper
tier: A
venue: "NeurIPS"
year: 2024
authors: ["Rajamanoharan", "Conmy", "Smith", "Lieberum", "Varma", "Kramár", "Shah", "Nanda"]
approx_citations: 180
doi: "10.52202/079017-0024"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# Improving Sparse Decomposition of Language Model Activations with Gated Sparse Autoencoders

Rajamanoharan, Conmy, Smith, Lieberum, Varma, Kramár, Shah, Nanda, *NeurIPS* 2024
(Google DeepMind). Introduces **Gated SAEs**: separate *which* features fire from *how
strongly*, so the L1 sparsity penalty no longer shrinks active magnitudes — a Pareto win
over Bricken-style L1-ReLU SAEs on models up to Gemma-7B.

## Summary

Baseline SAEs train MSE reconstruction plus an L1 penalty on encoder activations. That L1
term also **shrinks** live feature magnitudes, hurting fidelity at a given sparsity. Gated
SAEs split the encoder into a **gate** path (Heaviside on pre-activations → which features
are on) and a **magnitude** path (ReLU → how large), with weight tying so parameter/compute
overhead stays small. L1 is applied only to the gate pre-activations (plus an auxiliary
reconstruction loss through a frozen decoder copy). Across GELU-1L, Pythia-2.8B, and
Gemma-7B (MLP / attention / residual sites), Gated SAEs match or beat baseline fidelity at
half the active features in typical regimes, remove measurable shrinkage, and stay similarly
interpretable in a small blinded human study.

## Key claims / results

- **Pareto improvement** over baseline L1-ReLU SAEs on loss-recovered vs L0, holding training
  compute fixed (baselines get 50% more features to offset Gated's ~1.5× training step cost).
- **Shrinkage solved:** relative reconstruction bias \(\gamma \approx 1\) for Gated vs
  \(\gamma < 1\) (worse at higher \(\lambda\)) for baseline.
- **Half the firing features** often suffice for comparable reconstruction fidelity in typical
  hyperparameter ranges.
- **Interpretability:** blinded human ratings find Gated features comparable to baseline; not
  a clear win either way.
- Weight-tied Gated encoder is **equivalent to a JumpReLU** activation (same paper notes this
  connection; later JumpReLU SAEs train L0 directly).

## Methodology

- **Baseline (Bricken-style):** \(\mathbf{f}=\mathrm{ReLU}(W_{\mathrm{enc}}(x-b_{\mathrm{dec}})+b_{\mathrm{enc}})\),
  decode with unit-norm dictionary columns; loss \(\|x-\hat{x}\|_2^2+\lambda\|\mathbf{f}\|_1\).
- **Gated encoder:**
  \(\tilde{\mathbf{f}}=\mathbf{1}[\pi_{\mathrm{gate}}>0]\odot\mathrm{ReLU}(\pi_{\mathrm{mag}})\),
  with \(W_{\mathrm{mag}}\) a positive rescaling of shared \(W_{\mathrm{gate}}\) directions.
- **Gated loss:** main MSE on \(\tilde{\mathbf{f}}\) + \(\lambda\|\mathrm{ReLU}(\pi_{\mathrm{gate}})\|_1\)
  + auxiliary MSE reconstructing from \(\mathrm{ReLU}(\pi_{\mathrm{gate}})\) through a
  **frozen** decoder copy (so gate learns to detect without L1 biasing magnitudes).
- **Eval sites:** GELU-1L MLP neurons; Pythia-2.8B and Gemma-7B MLP outs, attention outs
  (pre-\(W_O\)), residual stream; metrics L0 and CE **loss recovered** when splicing
  reconstructions into the LM.
- **Metrics for shrinkage:** relative reconstruction bias \(\gamma\) from optimal rescale of
  reconstructions toward inputs.

## Related

- extends [[2023-bricken-towards-monosemanticity]] — same SAE-for-monosemanticity agenda; replaces L1-ReLU shrinkage with gated detection vs magnitude
- extends [[2006-hinton-deep-autoencoder]] — reconstructive AE skeleton kept; compressive bottleneck swapped for an overcomplete gated sparse code
- introduces [[gated-sae]] — gate/magnitude split + L1-on-gate-only training as the sparsity mechanism
- applies [[sparse-autoencoder-dictionary-learning]] — dictionary learning for LM activations with shrinkage-aware gating
- applies [[monosemantic-features-vs-polysemantic-neurons]] — shows fidelity/sparsity gains without clear loss of human feature interpretability vs baseline SAEs
- [[Sources MOC]]
- [[Autoencoder MOC]]
