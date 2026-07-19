---
title: JumpReLU sparse autoencoder
type: concept
status: done
date: 2026-07-19
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/sparse-autoencoder
distilled_from:
  - "[[2024-rajamanoharan-jumprelu-saes]]"
  - "[[2023-bricken-towards-monosemanticity]]"
---

# JumpReLU sparse autoencoder

A **JumpReLU SAE** replaces the encoder ReLU with a discontinuous **JumpReLU**: each feature has
a learned threshold \(\theta_i\); pre-activations below \(\theta_i\) are zeroed, those above pass
through at full magnitude. Sparsity is trained with an **L0** penalty via straight-through
estimators rather than L1.

## Why it matters / where it shows up

L1-ReLU SAEs ([[2023-bricken-towards-monosemanticity]]) under-estimate active feature magnitudes
(**shrinkage**) because L1 penalizes size as well as count. JumpReLU
([[2024-rajamanoharan-jumprelu-saes]]) separates *selection* (threshold) from *magnitude*
(identity above threshold), so the sparsity term no longer pulls down live activations. That
yields a better sparsity–reconstruction Pareto frontier on Gemma 2-scale LMs while staying as
cheap to train as a vanilla SAE (elementwise activation, one forward/backward pass).

## Details

- **Activation:** \(\mathrm{JumpReLU}_{\theta}(z)=z\,H(z-\theta)\) with \(\theta>0\) per feature.
- **Loss:** MSE reconstruction + \(\lambda\|f\|_0\); STE / KDE-style pseudo-derivatives train
  \(\theta\) despite piecewise-constant loss.
- **Vs relatives:** Gated SAEs also separate gate vs magnitude (often with weight sharing
  equivalent to JumpReLU) but typically keep an L1-style penalty; TopK fixes \(L_0=k\) exactly
  via a partial sort. JumpReLU sits between: soft \(\lambda\)-controlled L0, elementwise compute.
- **Side effects:** can leave a small tail of very high-frequency features (like TopK); dead
  features stay rare without resampling.

## Related

- introduces [[2024-rajamanoharan-jumprelu-saes]] — architecture, STE training, Gemma 2 9B Pareto evals
- contrasts [[2023-bricken-towards-monosemanticity]] — L1-ReLU + dead-feature resampling vs JumpReLU + L0/STE
- applies [[sparse-autoencoder-dictionary-learning]] — same overcomplete dictionary goal, thresholded activation
- background-for [[monosemantic-features-vs-polysemantic-neurons]] — fidelity gains claimed without hurting feature interpretability ratings
