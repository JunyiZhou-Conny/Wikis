---
title: VAE and ELBO for scRNA count data
type: concept
status: draft
date: 2026-06-17
tags:
  - concept
  - domain/ml
  - topic/vae
  - topic/scrna
source_doc: "[[2018-lopez-scvi]]"
distilled_from:
  - "[[2018-lopez-scvi]]"
  - "[[2026-06-17-002-vae-scrna-effectiveness-synthesis]]"
---

# VAE and ELBO for scRNA count data

A scRNA **VAE** optimizes the **ELBO**: reconstruction of counts under a **count noise model** (e.g. ZINB) plus a KL penalty on latent **z**.

## Why it matters

Plain MSE autoencoders treat expression as Gaussian — a poor match for sparse counts. scVI-style VAEs align loss with **sequencing physics**.

## Details

- Encoder: `q(z | x)`; decoder: `p(x | z)` with gene-specific dispersion/dropout.
- KL regularizes latent geometry; too weak → overfit; too strong → blur biology.
- Library size / batch often modeled as additional latent or covariates.

## Related

- [[probabilistic-vae-vs-count-autoencoder]]
- [[2018-lopez-scvi]]
- [[2021-xu-scanvi]]
- background-for [[2013-kingma-vae]] — SGVB/AEVB ELBO the count models adapt
- background-for [[2014-rezende-stochastic-backpropagation]] — free-energy / recognition-model ELBO at the DLGM root
- applies [[amortized-variational-inference]] — encoder that supplies \(q(z\mid x)\) in the ELBO
