---
title: Amortized variational inference (recognition / encoder network)
type: concept
status: done
date: 2026-07-22
tags:
  - concept
  - domain/ml
  - topic/vae
  - method/variational-inference
  - method/reparameterization
distilled_from:
  - "[[2014-rezende-stochastic-backpropagation]]"
  - "[[2013-kingma-vae]]"
---

# Amortized variational inference (recognition / encoder network)

Instead of running a separate iterative approximate-inference procedure for each datapoint, train a **recognition model** (encoder) \(q_\phi(z\mid x)\) that maps observations to variational posterior parameters in one forward pass. Gradients through sampled latents use **reparameterization / stochastic backpropagation**, so encoder and generative decoder train jointly on an ELBO / free-energy objective.

## Why it matters / where it shows up

This is the inference pattern that makes modern VAEs scalable: every scVI-style count VAE, and most future ELBO autoencoders in this wiki, reuse an amortized encoder rather than per-example mean-field updates. It also explains why “VAE” feels like an autoencoder — the recognition model *is* a stochastic encoder.

## Details

- **Amortization:** one network shares variational parameters across the dataset; inference cost is a forward pass.
- **Reparameterization:** write \(z=\mu(x)+\sigma(x)\odot\varepsilon\), \(\varepsilon\sim\mathcal{N}(0,I)\) (Kingma) or equivalent Gaussian location-scale / Bonnet–Price rules (Rezende) so Monte Carlo ELBO gradients are low-variance and backprop-friendly.
- **Versus alternatives:** score-function / REINFORCE estimators apply more broadly but scale poorly with latent dimension; Laplace / EP / INLA struggle with deep nonlinear latent Gaussians at VAE scale (as Rezende et al. argue).

## Related

- introduces [[2014-rezende-stochastic-backpropagation]] — DLGM recognition model + stochastic backpropagation
- introduces [[2013-kingma-vae]] — AEVB / SGVB amortized encoder with the reparameterization trick
- background-for [[2018-lopez-scvi]] — scVI’s encoder is this pattern with a ZINB decoder
- applies [[vae-elbo-scrna-count-models]] — ELBO terms the amortized encoder is trained against in count VAEs
- contrasts [[probabilistic-vae-vs-count-autoencoder]] — amortization + KL defines the variational side vs deterministic count AEs
