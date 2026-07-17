---
title: "Scaling and Evaluating Sparse Autoencoders"
type: source
status: done
date: 2026-07-17
source_kind: paper
tier: A
venue: "ICLR"
year: 2025
authors: ["Gao", "Dupré la Tour", "Tillman", "Goh", "Troll", "Radford", "Sutskever", "Leike", "Wu"]
approx_citations: 530
doi: "10.48550/arXiv.2406.04093"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# Scaling and Evaluating Sparse Autoencoders

Gao, Dupré la Tour, Tillman, Goh, Troll, Radford, Sutskever, Leike, Wu, *ICLR* 2025
(Oral; OpenAI Superalignment Interpretability). Shows that **TopK (k-sparse) SAEs** give a
cleaner sparsity–reconstruction frontier, few dead latents at scale, and measurable **scaling
laws**, culminating in a **16M-latent** SAE on GPT-4 residual streams.

## Summary

Sparse autoencoders are a leading tool for decomposing LM activations into interpretable
features, but L1-ReLU recipes are hard to tune and leave many dead latents when the dictionary
gets wide. This paper replaces the L1 penalty with a **TopK** activation that keeps exactly \(k\)
latents active, adds **tied encoder/decoder init** plus an **AuxK** loss on dead latents, and
reports clean power-law scaling in dictionary size and sparsity. Quality metrics beyond MSE
(downstream LM loss, probe recovery of hypothesized features, N2G explainability, ablation
sparsity) generally improve with more latents. The headline demo trains a 16M-feature SAE on
GPT-4 for 40B tokens and releases code, GPT-2 SAEs, and a feature visualizer.

## Key claims / results

- **TopK beats L1-ReLU (and matches/beats Gated/ProLU)** on the sparsity–reconstruction Pareto
  frontier; the gap widens as dictionary width grows.
- **Dead latents are controllable:** tied init + AuxK keeps dead rate ~7% even at 16M latents
  (vs up to ~90% with no mitigations; Templeton’s 34M SAE had only ~12M alive).
- **Scaling laws:** MSE follows power laws in compute and in \((n, k)\) jointly; larger subject
  models need larger SAEs for the same MSE at fixed \(k\).
- **Downstream substitution:** putting the 16M GPT-4 SAE reconstruction in place of the residual
  stream yields LM loss comparable to ~10% of GPT-4 pretraining compute (zero-ablation fidelity
  98.2% is reported but argued to be too lenient).
- **Interpretability metrics** (1d probe recovery of 61 binary concepts, N2G precision/recall,
  logit-diff sparsity) generally improve with more total latents; \(L_0\) has a more nuanced
  trade-off and breaks down when \(k\) approaches \(d_\mathrm{model}\).

## Methodology

- **Data:** residual-stream activations from GPT-2 small (layer 8) and a GPT-4-family stack
  (layer ~5/6 of the way); context length 64; mean-subtract and unit-normalize inputs.
- **Architecture:** baseline ReLU SAE from Bricken et al.; TopK encoder
  \(z = \mathrm{TopK}(W_\mathrm{enc}(x - b_\mathrm{pre}))\) with MSE-only training loss (no L1).
- **Dead-latent recipe:** initialize \(W_\mathrm{enc}\) parallel to \(W_\mathrm{dec}^\top\);
  AuxK reconstructs the residual error with the top-\(k_\mathrm{aux}\) currently dead latents
  (\(\alpha \approx 1/32\)).
- **Evaluation:** normalized MSE, \(L_0\), KL / ΔCE when substituting reconstructions, 1d probes,
  improved Neuron-to-Graph explanations, and ablation sparsity of logit effects.
- **Scale demo:** 16M-latent TopK SAE on GPT-4, 40B tokens; open-source training code and
  GPT-2 SAE suite.

## Related

- extends [[2023-bricken-towards-monosemanticity]] — same SAE-for-monosemanticity agenda, but replaces L1-ReLU with TopK and scales from a toy one-layer MLP to GPT-4 residuals
- extends [[2006-hinton-deep-autoencoder]] — reconstructive AE skeleton kept; bottleneck compression swapped for an overcomplete TopK sparse code
- introduces [[topk-k-sparse-autoencoder]] — direct \(L_0\) control via TopK + AuxK/tied-init dead-latent mitigations
- applies [[sparse-autoencoder-dictionary-learning]] — dictionary learning for LM activations, now with fixed sparsity and scaling laws
- applies [[monosemantic-features-vs-polysemantic-neurons]] — evaluates whether larger TopK dictionaries yield more recoverable / explainable features
- [[Sources MOC]]
- [[Autoencoder MOC]]
