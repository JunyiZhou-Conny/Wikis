---
title: "Regularized linear autoencoders recover the principal components, eventually"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "NeurIPS 2020"
year: 2020
authors: ["Bao", "Lucas", "Sachdeva", "Grosse"]
approx_citations: 80
doi: "10.48550/arXiv.2007.06731"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - topic/dimensionality-reduction
  - method/autoencoder
---

# Regularized linear autoencoders recover the principal components, eventually

Bao, Lucas, Sachdeva & Grosse, *NeurIPS 2020*. Makes precise **when** an autoencoder recovers
the *ordered, axis-aligned* principal components — the condition PCA-style latent selection needs.

## Summary

A plain linear autoencoder (LAE) with MSE loss recovers the **PCA subspace** but not the ordered,
axis-aligned components (its solution is only defined up to an invertible transform). The paper
shows that with **proper regularization** — non-uniform ℓ2 penalties on the latent weights, or a
deterministic variant of **nested dropout** — the LAE converges to the *exact* ordered principal
components. It also analyzes convergence speed and proposes a gradient fix.

## Key claims / results

- Unregularized LAE: recovers only the PC **subspace**, with rotational ambiguity (no ordering).
- **Non-uniform ℓ2** regularization breaks the symmetry so every global minimum recovers the
  ordered, axis-aligned PCs; all local minima are global minima.
- Deterministic **nested dropout** also recovers individual PCs.
- Convergence is **slow** due to ill-conditioning that worsens as latent dimension grows; a simple
  gradient-update modification greatly speeds it up.

## Methodology

- Theoretical analysis of the LAE loss landscape under each regularizer.
- Empirical convergence studies on the recovery of ordered PCs.

## Relevance to your question

- This is the precise reason a PCA "variance-explained" rule can't be applied to an ordinary
  autoencoder: **without special regularization the latent axes are unordered**, so per-axis
  variance is not a valid ranking. Architectures that *do* order axes (see PCA-AE, PCAE) build on
  exactly this result.

## Related

- extends [[2006-hinton-deep-autoencoder]] — sharpens the classic "AE generalizes PCA" claim into an exact ordered-recovery condition
- introduces [[linear-autoencoder-pca-equivalence]] — the formal LAE↔PCA correspondence and when ordering is recovered
- background-for [[choosing-latent-dimension]] — explains why variance-thresholding needs *ordered* latent axes
- benchmarks [[2019-rolinek-vae-pca-directions]] — complementary VAE-side account of the same PCA pull
- [[Sources MOC]]
- [[Autoencoder MOC]]
