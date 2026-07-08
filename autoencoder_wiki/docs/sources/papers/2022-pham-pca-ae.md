---
title: "PCA-AE: Principal Component Analysis Autoencoder for Organising the Latent Space of Generative Networks"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: B
venue: "Journal of Mathematical Imaging and Vision"
year: 2022
authors: ["Pham", "Ladjal", "Newson"]
approx_citations: 30
doi: "10.1007/s10851-022-01077-z"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - topic/dimensionality-reduction
  - method/autoencoder
---

# PCA-AE: organising the latent space like PCA

Pham, Ladjal & Newson, *JMIV 2022*. An autoencoder trained so its latent axes are **ordered by
importance** and **statistically independent** — making a PCA-style variance criterion usable.

## Summary

Standard AEs have unordered, entangled latent axes. PCA-AE enforces two PCA-like properties:
(i) latent dimensions ordered by decreasing importance, and (ii) components statistically
independent. It achieves this by **progressively growing** the latent space during training
(train size-1, freeze, add a second unit, …) plus a **covariance loss** that decorrelates codes.
With a single linear layer it reduces exactly to PCA.

## Key claims / results

- Progressive training + covariance penalty yields a latent space where **early axes carry more
  variance** — a nonlinear analogue of PCA's ordered components.
- Components become close to statistically independent (better disentanglement than a vanilla AE).
- Extends to organising the latent space of a pre-trained GAN.
- On CelebA it separates interpretable attributes (hair/skin shade, pose, gender) unsupervised.

## Methodology

- Sequential latent-growth schedule; freeze previously learned units when adding a new one.
- Add a latent covariance loss to the reconstruction objective to enforce independence.

## Relevance to your question

- A concrete architecture where **"keep enough components to explain X% variance" becomes valid**,
  because the model *builds* an ordered latent basis. Contrast with a standard VAE/scVI where axes
  are unordered and this rule does not hold.

## Related

- extends [[2006-hinton-deep-autoencoder]] — adds PCA-like ordering + independence to the classic AE bottleneck
- applies [[linear-autoencoder-pca-equivalence]] — an explicit construction that keeps the AE↔PCA correspondence in the nonlinear regime
- background-for [[choosing-latent-dimension]] — ordered latents let you pick k by cumulative variance
- benchmarks [[2025-saha-ard-vae]] — alternative "which axes matter" method compared in the ordered-latent literature
- [[Sources MOC]]
- [[Autoencoder MOC]]
