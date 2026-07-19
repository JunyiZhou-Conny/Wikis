---
title: "Jumping Ahead: Improving Reconstruction Fidelity with JumpReLU Sparse Autoencoders"
type: source
status: done
date: 2026-07-19
source_kind: paper
tier: A
venue: "arXiv (Google DeepMind)"
year: 2024
authors: ["Rajamanoharan", "Lieberum", "Sonnerat", "Conmy", "Varma", "Kramár", "Nanda"]
approx_citations: 270
doi: "10.48550/arXiv.2407.14435"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# Jumping Ahead: Improving Reconstruction Fidelity with JumpReLU Sparse Autoencoders

Rajamanoharan, Lieberum, Sonnerat, Conmy, Varma, Kramár, Nanda, *arXiv* 2024
(Google DeepMind). Introduces **JumpReLU SAEs**: replace the encoder ReLU with a discontinuous
**JumpReLU** (per-feature threshold) and train **L2 + L0** via straight-through estimators,
pushing the sparsity–fidelity Pareto frontier past Gated and matching/beating TopK on Gemma 2 9B.

## Summary

Vanilla L1-ReLU SAEs trade reconstruction for sparsity badly because L1 also shrinks active
feature magnitudes. JumpReLU SAEs keep a standard encoder/decoder skeleton but add a learnable
positive threshold per feature: pre-activations below the threshold are zeroed, those above pass
through unchanged — separating *which* features fire from *how strongly*. Training uses MSE plus
an L0 penalty; both the JumpReLU and the Heaviside in L0 are non-differentiable in \(\theta\), so
the authors derive STE pseudo-derivatives equivalent to a kernel-density estimate of the expected
loss gradient. On Gemma 2 9B residual / MLP / attention sites, JumpReLU matches or beats TopK
and clearly beats Gated on delta-LM-loss and FVU at matched L0, with similar human/auto
interpretability and few dead features without resampling.

## Key claims / results

- **JumpReLU ≈ TopK ≥ Gated** on the sparsity–fidelity frontier (delta LM loss and FVU) for
  131k-width SAEs on Gemma 2 9B residual, MLP, and attention activations (layers 9/20/31).
- **Direct L0 training avoids L1 shrinkage:** magnitudes above the threshold are not pulled down
  by the sparsity term (unlike L1-ReLU and L1-gated recipes).
- **Efficiency:** single forward/backward pass and an elementwise activation (no TopK partial
  sort; cheaper than Gated's dual encoder paths).
- **High-frequency features:** JumpReLU and TopK have more features firing on >10% of tokens
  than Gated, but still <0.06% of a 131k dictionary; random-feature interpretability is
  comparable across the three architectures.
- **Dead features stay rare** without Bricken-style resampling (unlike L1 Gated; TopK needs AuxK).

## Methodology

- **Architecture:** \(f(x)=\mathrm{JumpReLU}_{\boldsymbol{\theta}}(W_{\mathrm{enc}}x+b_{\mathrm{enc}})\),
  \(\mathrm{JumpReLU}_{\theta}(z)=z\,H(z-\theta)\); linear decoder as usual.
- **Loss:** \(\|x-\hat{x}\|_2^2 + \lambda\|f(x)\|_0\); STEs with a rectangular (or other) kernel
  of bandwidth \(\varepsilon\) supply gradients w.r.t. thresholds.
- **Data / scale:** Gemma 2 9B activations; 8B training tokens; width 131k; sweep \(\lambda\)
  (JumpReLU/Gated) or \(k\) (TopK) for Pareto curves.
- **Baselines:** Gated SAE (original L1 + resampling, and RI-L1 without resampling); TopK + AuxK
  (Gao et al.); metrics on 2,048×1,024 sequences excluding special tokens.
- **Interpretability:** blinded human ratings plus automated interpretability at matched L0
  (~20 / 75 / 150).

## Related

- extends [[2023-bricken-towards-monosemanticity]] — same SAE-for-monosemanticity agenda; replaces L1-ReLU with JumpReLU + direct L0 and benchmarks fidelity on Gemma 2 9B
- extends [[2006-hinton-deep-autoencoder]] — reconstructive AE skeleton kept; compressive bottleneck swapped for an overcomplete JumpReLU sparse code
- introduces [[jumprelu-sae]] — per-feature threshold activation + STE-trained L0 as the sparsity mechanism
- applies [[sparse-autoencoder-dictionary-learning]] — dictionary learning for LM activations with a hard threshold instead of L1
- applies [[monosemantic-features-vs-polysemantic-neurons]] — shows fidelity gains do not cost human/auto feature interpretability vs Gated/TopK
- [[Sources MOC]]
- [[Autoencoder MOC]]
