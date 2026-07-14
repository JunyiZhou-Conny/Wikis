---
title: β-VAE weighted KL for disentanglement
type: concept
status: done
date: 2026-07-14
tags:
  - concept
  - domain/ml
  - topic/vae
  - method/beta-vae
distilled_from:
  - "[[2017-higgins-beta-vae]]"
  - "[[2013-kingma-vae]]"
  - "[[2019-rolinek-vae-pca-directions]]"
---

# β-VAE weighted KL for disentanglement

**β-VAE** multiplies the VAE's KL regularizer by a scalar **β**. When β > 1, the latent channel
is capacity-limited harder against an isotropic Gaussian prior, which (with enough reconstruction
pressure) favors **statistically independent, factor-aligned** codes — a **disentangled**
representation.

## Why it matters / where it shows up

The plain VAE ELBO ([[2013-kingma-vae]], β = 1) often yields **entangled** latents on complex
images. Higgins et al. show that a single extra hyperparameter is enough to push unsupervised
VAEs toward inverse-graphics-style factors and to score that property with a linear probe
([[2017-higgins-beta-vae]]). Later theory treats the same diagonal-posterior + noise mechanism as
part of why VAE axes behave like local PCA — and why β-/disentanglement variants add *extra*
independence pressure ([[2019-rolinek-vae-pca-directions]]).

## Details

- **Objective shape:** reconstruction − β · D_KL(q(z|x) ‖ N(0,I)). β = 1 recovers the ELBO;
  β > 1 tightens the information bottleneck and the independence prior.
- **Intended effect:** when data has (some) independent generative factors, a tight isotropic
  bottleneck prefers allocating separate latent units to separate factors.
- **Cost:** too-large β → blurry reconstructions and dropped low-pixel-impact factors; tune via
  a disentanglement metric (when labels exist) or latent-traversal inspection.
- **Readout of unused axes:** units with near-zero KL are uninformative — the same passive /
  collapsed-axis phenomenon ([[passive-latent-dimensions]]), here as a byproduct of capacity
  control.

## Related

- introduces [[2017-higgins-beta-vae]] — canonical DeepMind / ICLR formulation and metric
- extends [[2013-kingma-vae]] — reweights the KL term of the original VAE objective
- background-for [[2019-rolinek-vae-pca-directions]] — mechanism paper that situates β-VAE in the
  diagonal-posterior / local-PCA story
- applies [[passive-latent-dimensions]] — capacity-limited KL leaves unused axes near the prior
- contrasts [[monosemantic-features-vs-polysemantic-neurons]] — end-to-end factorized latents vs
  post-hoc sparse dictionary features
