---
title: "Dimension Estimation Using Autoencoders"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: C
venue: "arXiv (preprint)"
year: 2019
authors: ["Bahadur", "Paffenroth"]
approx_citations: 15
doi: "10.48550/arXiv.1909.10702"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - topic/dimensionality-reduction
  - method/autoencoder
---

# Dimension Estimation Using Autoencoders

Bahadur & Paffenroth (WPI), *arXiv 2019*. **Tier C — preprint; flagged per vault contract.**
Turns an autoencoder into an intrinsic-**dimension estimator**, using PCA/SVD as the reference.

## Summary

The paper separates **dimension reduction** (project to low-d) from **dimension estimation**
(how many latent factors exist). PCA estimates ID naturally via ordered singular values / scree
plots; a plain AE does **not** — its bottleneck activations have no ordered singular-value analogue.
The authors construct **singular-value proxies (SVPs)** from AE hidden layers and threshold their
cumulative mass to estimate nonlinear intrinsic dimension.

## Key claims / results

- A linear AE with squared loss spans the same subspace as PCA, but gradient descent gives **no
  ordering guarantee** — so raw bottleneck values can't be read as a dimension estimate.
- Their **SVPs** restore an ordered, PCA-like quantity from the AE; dimensions are kept when they
  exceed a cumulative-mass cutoff (e.g. **~1%** of cumulative singular value).
- On MNIST, PCA scree plots suggest ID ≈ 30 (≪ 784); reconstruction error spikes when k drops
  below the true ID — the classic "compress below ID ⇒ information loss" signal.
- Demonstrated on MNIST and S&P 500 data.

## Methodology

- Architectural/regularization choices to make AE latents amenable to SVP extraction.
- Compare AE-based ID estimates against PCA/SVD scree analysis.

## Relevance to your question

- Frames your exact intuition — "PCA variance tells you the ceiling" — and shows **why a plain AE
  can't inherit it directly**: you must first recover an ordered, singular-value-like quantity.
  PCA scree/variance is used as the **baseline dimension estimate**, not an automatic latent cap.

## Related

- extends [[2006-hinton-deep-autoencoder]] — repurposes the AE bottleneck for dimension *estimation*, not just reduction
- introduces [[intrinsic-dimension-latent-sizing]] — singular-value proxies as an ID-based way to size the bottleneck
- background-for [[choosing-latent-dimension]] — connects PCA scree/variance to AE latent sizing and its pitfalls
- background-for [[linear-autoencoder-pca-equivalence]] — relies on the AE↔PCA subspace correspondence (and its ordering gap)
- [[Sources MOC]]
- [[Autoencoder MOC]]
