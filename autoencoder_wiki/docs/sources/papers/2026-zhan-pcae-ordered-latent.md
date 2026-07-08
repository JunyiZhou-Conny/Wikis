---
title: "Learning Ordered Representations in Latent Space for Intrinsic Dimension Estimation via Principal Component Autoencoder"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: C
venue: "arXiv (preprint)"
year: 2026
authors: ["Zhan", "Zhou", "Wang", "Shen"]
approx_citations: 0
doi: "10.48550/arXiv.2601.19179"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - topic/dimensionality-reduction
  - method/autoencoder
---

# Principal Component Autoencoder (PCAE) — ordered latents for ID estimation

Zhan, Zhou, Wang & Shen (UPenn), *arXiv 2026*. **Tier C — preprint, 0 citations; flagged per vault
contract.** The clearest statement of "pick latent dim by cumulative variance," *if* you first
build a PCA-ordered autoencoder.

## Summary

PCAE extends PCA to the nonlinear regime while **preserving variance ordering**. It combines
**non-uniform variance regularization** (increasing weights γ₁<…<γₚ that penalize variance more in
later coordinates) with an **isometric constraint** (distance preservation), so the i-th latent
coordinate behaves like the i-th principal component. This makes post-hoc intrinsic-dimension
estimation possible without knowing the bottleneck size in advance.

## Key claims / results

- With variance-ordered latents you can estimate ID **exactly like PCA**: pick the smallest k whose
  first k coordinates explain ≥ **τ (e.g. 99%)** of total variance.
- Theorem: the weighted-variance objective recovers PCs in the correct order (linear case).
- Isometry term is **required** — without distance preservation, latent variances lose geometric
  meaning.
- For **baseline autoencoders**, latent-coordinate variance does **not** correspond to data
  variance; there they fall back on the ARD-VAE relevance score (Saha et al. 2025) to rank axes.
- Evaluated on dSprites, 3DShapes, MNIST, CelebA vs PCA-AE, HAE, ARD-VAE, IRMAE.

## Methodology

- Loss = reconstruction + β·(weighted variance) + isometry regularizer; dynamic γ schedule to
  avoid vanishing gradients.

## Relevance to your question

- **Best direct match** to "use PCA explained-variance to choose the latent dimension." The catch:
  the rule is valid **only because the model is engineered to be PCA-ordered** — it explicitly
  states the rule fails on a standard (unordered) autoencoder/VAE latent. Uses **99%**, not 95%.

## Related

- extends [[2022-pham-pca-ae]] — same goal (ordered latents) but joint (not sequential) training + isometry constraint
- applies [[choosing-latent-dimension]] — realizes the "cumulative-variance ceiling" idea for a purpose-built AE
- introduces [[intrinsic-dimension-latent-sizing]] — post-hoc ID estimation from a trained ordered latent
- background-for [[linear-autoencoder-pca-equivalence]] — nonlinear generalization of the LAE↔PCA ordering result
- applies [[2025-saha-ard-vae]] — reuses its relevance score for the non-ordered baseline case
- [[Sources MOC]]
- [[Autoencoder MOC]]
