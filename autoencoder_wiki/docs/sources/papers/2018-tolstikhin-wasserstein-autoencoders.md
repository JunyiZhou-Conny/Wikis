---
title: "Wasserstein Auto-Encoders"
type: source
status: done
date: 2026-07-24
source_kind: paper
tier: A
venue: "ICLR 2018"
year: 2018
authors: ["Tolstikhin", "Bousquet", "Gelly", "Schölkopf"]
approx_citations: 1500
doi: "10.48550/arXiv.1711.01558"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/autoencoder
  - topic/optimal-transport
  - method/ot
---

# Wasserstein Auto-Encoders

Tolstikhin, Bousquet, Gelly & Schölkopf, *ICLR 2018* (arXiv Nov 2017; Google Brain / MPI-IS). The **canonical Wasserstein Auto-Encoder (WAE)** paper — reframes generative autoencoders as minimizing a penalized optimal-transport cost, with a regularizer that matches the *aggregated* encoded distribution to the prior rather than each per-example posterior.

## Summary

WAE builds a latent-variable generative model by minimizing a relaxed primal OT cost \(W_c(P_X, P_G)\) between data and the decoder pushforward of a fixed prior \(P_Z\). Theorem 1 shows that for deterministic decoders this reduces to an encoder–decoder objective: reconstruct under cost \(c\), while forcing the mixture \(Q_Z := \mathbb{E}_{P_X}[Q(Z|X)]\) to match \(P_Z\). That aggregate matching is the key contrast with VAEs, which penalize \(D_{\mathrm{KL}}(Q(Z|X), P_Z)\) *for every* \(x\). Two practical penalties yield **WAE-GAN** (adversarial JS matching in latent space — recovering AAE when \(c=\|x-y\|_2^2\)) and **WAE-MMD** (adversary-free MMD with a heavy-tailed inverse-multiquadratics kernel). On MNIST and CelebA, WAEs keep VAE-like stable training, reconstructions, and latent interpolations while improving sample FID/sharpness over a matched VAE.

## Key claims / results

- **OT primal → AE form:** for deterministic \(G\), \(\inf_\Gamma \mathbb{E}[c(X,Y)] = \inf_{Q:\,Q_Z=P_Z} \mathbb{E}[c(X,G(Z))]\); relaxing \(Q_Z=P_Z\) with \(\lambda\cdot\mathcal{D}_Z(Q_Z,P_Z)\) gives the WAE objective (Eq. 4).
- **Aggregate vs per-example prior matching:** VAE forces every red ball \(Q(Z|x)\) onto \(P_Z\) (codes overlap → blurrier reconstructions); WAE only matches the green mixture \(Q_Z\), so codes of different \(x\) can stay separated.
- **Generalizes AAE:** WAE-GAN with squared cost equals Makhzani et al.’s adversarial autoencoder; WAE further allows any input cost \(c\) and any latent discrepancy (e.g. MMD).
- **Deterministic encoders allowed:** unlike standard VAEs, \(Q(Z|x)\) may be a Dirac map \(\mu_\phi(x)\).
- **Empirics (CelebA FID, lower better):** VAE 63 → WAE-MMD 55 → WAE-GAN 42 (larger “big*” models: 45 / 37 / 35); WAE-MMD trains more stably than WAE-GAN.

## Methodology

- **Objective:** \(\inf_Q \mathbb{E}_{P_X}\mathbb{E}_{Q(Z|X)}[c(X,G(Z))] + \lambda\cdot\mathcal{D}_Z(Q_Z,P_Z)\) with \(c(x,y)=\|x-y\|_2^2\) in experiments, \(\lambda=10\).
- **WAE-GAN:** latent discriminator separates \(z\sim P_Z\) from \(\tilde{z}\sim Q_Z\); encoder/decoder descend reconstruction minus \(\lambda\log D(\tilde{z})\).
- **WAE-MMD:** U-statistic MMD with inverse multiquadratics \(k(x,y)=C/(C+\|x-y\|_2^2)\), \(C=2d_z\sigma_z^2\) (RBF tails too light for outliers).
- **Architecture:** DCGAN-style conv nets, deterministic encoder–decoder, isotropic Gaussian \(P_Z\); \(d_z=8\) (MNIST) / \(64\) (CelebA); Adam \(\beta_1=0.5\).

## Related

- contrasts [[2013-kingma-vae]] — replaces per-example KL-to-prior with OT-motivated matching of the aggregated posterior \(Q_Z\) to \(P_Z\)
- extends [[2006-hinton-deep-autoencoder]] — keeps reconstructive encoder/decoder but adds an OT latent regularizer for generative sampling
- background-for [[2020-yang-cellot]] — earlier OT-cost framing of AE generative models; CellOT later couples AE latents with transport *between conditions*
- introduces [[wasserstein-autoencoder]] — aggregate-posterior WAE family (WAE-GAN / WAE-MMD)
- contrasts [[vae-elbo-scrna-count-models]] — ELBO/KL path vs WAE’s reconstruction + \(\mathcal{D}_Z(Q_Z,P_Z)\) path
- contrasts [[probabilistic-vae-vs-count-autoencoder]] — WAE sits between: generative AE with prior matching, but not an ELBO/VAE
- [[Sources MOC]]
- [[Autoencoder MOC]]
