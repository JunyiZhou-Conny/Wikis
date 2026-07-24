---
title: Wasserstein autoencoder (aggregated posterior matching)
type: concept
status: done
date: 2026-07-24
tags:
  - concept
  - domain/ml
  - topic/vae
  - topic/autoencoder
  - topic/optimal-transport
  - method/ot
distilled_from:
  - "[[2018-tolstikhin-wasserstein-autoencoders]]"
  - "[[2013-kingma-vae]]"
---

# Wasserstein autoencoder (aggregated posterior matching)

A **Wasserstein autoencoder (WAE)** trains an encoder–decoder generative model by minimizing a reconstruction cost plus a penalty that matches the **aggregated** encoded distribution \(Q_Z=\mathbb{E}_{P_X}[Q(Z|X)]\) to a fixed prior \(P_Z\), motivated by a primal optimal-transport formulation of \(W_c(P_X,P_G)\). Unlike a VAE, it does **not** force each per-example \(Q(Z|x)\) onto the prior.

## Why it matters / where it shows up

This is the clean conceptual fork after [[2013-kingma-vae]]: same AE skeleton and prior-sampling generative story, different regularizer geometry. Aggregate matching lets codes of distinct inputs stay separated (better reconstruction) while still making \(z\sim P_Z\) decodable. It also justifies adversarial autoencoders as a special case (WAE-GAN with squared cost) and supplies an adversary-free MMD variant. In this wiki it bridges the VAE foundation thread to OT-flavored AE work such as [[2020-yang-cellot]].

## Details

- **OT reduction:** for deterministic decoder \(G\), transporting \(P_X\) to \(P_G=G_\#P_Z\) is equivalent to finding an encoder whose latent marginal equals \(P_Z\), then paying \(\mathbb{E}[c(X,G(Z))]\).
- **Relaxation:** enforce \(Q_Z\approx P_Z\) with GAN/JS in latent space (**WAE-GAN**) or kernel MMD (**WAE-MMD**), weighted by \(\lambda\).
- **Versus VAE ELBO:** drop the mutual-information / per-point KL pressure; deterministic encoders are allowed.
- **Failure mode:** sample quality tracks how well \(Q_Z\) actually matches \(P_Z\) — the decoder only ever sees encoded codes at train time.

## Related

- introduces [[2018-tolstikhin-wasserstein-autoencoders]] — canonical WAE-GAN / WAE-MMD paper (ICLR 2018)
- contrasts [[2013-kingma-vae]] — aggregate OT matching vs per-example KL in the ELBO
- background-for [[2020-yang-cellot]] — OT enters AE pipelines again for condition-to-condition transport
- contrasts [[vae-elbo-scrna-count-models]] — count VAEs stay on the ELBO/KL path this concept steps off
- contrasts [[probabilistic-vae-vs-count-autoencoder]] — WAE is a third generative-AE pattern (neither ELBO-VAE nor plain count AE)
