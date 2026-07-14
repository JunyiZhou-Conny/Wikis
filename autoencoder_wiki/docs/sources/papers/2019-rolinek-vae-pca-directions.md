---
title: "Variational Autoencoders Pursue PCA Directions (by Accident)"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "CVPR 2019"
year: 2019
authors: ["Rolínek", "Zietlow", "Martius"]
approx_citations: 350
doi: "10.48550/arXiv.1812.06775"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/autoencoder
  - method/vae
---

# Variational Autoencoders Pursue PCA Directions (by Accident)

Rolínek, Zietlow & Martius, *CVPR 2019*. Explains **why** VAE latent axes end up resembling
PCA directions — the theoretical backbone for any "PCA-informed" reasoning about VAE latents.

## Summary

The paper isolates an internal mechanism of the VAE (and β-VAE): the **diagonal covariance
approximation** in the encoder combined with the **stochastic sampling** of the latent forces
**local orthogonality** of the decoder. Locally promoting both reconstruction and orthogonality
mirrors how PCA chooses its embedding — so the VAE tends to align latent axes with principal
directions of the data, collapsing to PCA in the linear case.

## Key claims / results

- Diagonal posterior + injected noise ⇒ decoder columns become **locally orthogonal**.
- This local behavior **matches PCA's selection criterion**, so VAEs "accidentally" pursue PCA
  directions and use **differences in variance** to structure the latent space.
- This is an *implicit* effect: the VAE objective does not explicitly encourage factorized/aligned
  axes, which is why later β-/disentanglement variants add explicit independence terms.
- Verified with theory (including the nonlinear case via linearization) and experiments across
  architectures/datasets.

## Methodology

- Analyze the ELBO's stochastic reconstruction term; derive a "distance-to-orthogonality" measure.
- Show, both formally and empirically, that trained VAE decoders drive this measure toward local
  orthogonality.

## Relevance to your question

- Grounds the intuition behind "PCA variance → latent dim": VAE axes *relate* to PCA directions,
  **but only locally and without a canonical ordering**. This is why a naive "keep k PCs for 95%
  variance" ceiling does not transfer cleanly to standard VAE latents.

## Related

- extends [[2013-kingma-vae]] — dissects the ELBO mechanism of the original VAE to explain latent alignment
- background-for [[choosing-latent-dimension]] — the "VAE ≈ local PCA" result people cite when proposing PCA-style latent sizing
- introduces [[linear-autoencoder-pca-equivalence]] — the linear-case collapse of VAE/AE onto PCA directions
- benchmarks [[2018-way-tybalt]] — sibling VAE source in the vault where latent structure/tuning matters
- extends [[2017-higgins-beta-vae]] — explains the diagonal-posterior / sampling mechanism that β-VAE inherits and why extra independence pressure helps
- applies [[beta-vae-weighted-kl-disentanglement]] — situates β-/disentanglement variants as explicit fixes beyond accidental PCA alignment
- [[Sources MOC]]
- [[Autoencoder MOC]]
