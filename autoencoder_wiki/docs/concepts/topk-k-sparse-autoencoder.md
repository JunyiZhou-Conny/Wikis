---
title: TopK / k-sparse autoencoder for fixed L0
type: concept
status: done
date: 2026-07-17
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/sparse-autoencoder
distilled_from:
  - "[[2025-gao-scaling-evaluating-saes]]"
  - "[[2023-bricken-towards-monosemanticity]]"
---

# TopK / k-sparse autoencoder for fixed L0

A **TopK (k-sparse) SAE** replaces the usual L1+ReLU sparsity penalty with an activation that
keeps only the \(k\) largest latents and zeros the rest, so **\(L_0 = k\)** is set directly and
the training loss can be pure reconstruction MSE.

## Why it matters / where it shows up

L1-ReLU SAEs ([[2023-bricken-towards-monosemanticity]]) need a tuned \(\lambda\), shrink positive
activations, and leave many **dead latents** at large width. TopK ([[2025-gao-scaling-evaluating-saes]])
removes that trade-off knob, improves the sparsity–reconstruction frontier (especially as \(n\)
grows), and — with tied init + AuxK — keeps almost all latents alive up to tens of millions of
features on GPT-4.

## Details

- **Encoder:** \(z = \mathrm{TopK}(W_\mathrm{enc}(x - b_\mathrm{pre}))\) (often with a ReLU for
  non-negativity that barely changes training).
- **Loss:** MSE only; no L1. Multi-TopK (sum of losses at several \(k\)) can restore progressive
  codes across sparsity levels.
- **Dead-latent mitigations:** encoder initialized parallel to decoder transpose; AuxK trains
  currently dead latents to explain residual reconstruction error.
- **Scaling:** enables joint laws \(L(n,k)\) and cleaner comparisons across widths because \(L_0\)
  is matched exactly rather than interpolated from \(\lambda\).

## Related

- introduces [[2025-gao-scaling-evaluating-saes]] — TopK + AuxK recipe and GPT-4 16M-latent scale demo
- contrasts [[2023-bricken-towards-monosemanticity]] — L1-ReLU + dead-feature resampling vs TopK with exact \(L_0\)
- applies [[sparse-autoencoder-dictionary-learning]] — same overcomplete dictionary goal, different sparsity mechanism
- background-for [[monosemantic-features-vs-polysemantic-neurons]] — clamping small activations to zero can raise monosemanticity of random firing examples
