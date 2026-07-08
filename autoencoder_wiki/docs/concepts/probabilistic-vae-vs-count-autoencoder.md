---
title: Probabilistic VAE vs count autoencoder (scVI vs DCA)
type: concept
status: draft
date: 2026-06-17
tags:
  - concept
  - domain/ml
  - topic/vae
  - topic/autoencoder
  - topic/scrna
source_doc: "[[2018-lopez-scvi]]"
distilled_from:
  - "[[2018-lopez-scvi]]"
  - "[[2019-eraslan-dca]]"
---

# Probabilistic VAE vs count autoencoder (scVI vs DCA)

**scVI** is a full **variational** model (ELBO + KL + ZINB). **DCA** is a **deterministic count autoencoder** with ZINB/NB loss — no variational posterior over z.

## Why it matters

Both are "autoencoders" in the broad sense but optimize different objectives and support different claims (uncertainty, integration vs denoising).

## Details

| | scVI | DCA |
|--|------|-----|
| Variational | Yes | No |
| Primary win | Latent for DR, batch, DE | Denoising / imputation |
| Default arch | Tunable MLP | 64–32–64 |
| Ecosystem | scvi-tools | DCA package |

Pick based on whether you need **generative latent inference** or **denoised counts**.

## Related

- extends [[vae-elbo-scrna-count-models]] — the ELBO/count-likelihood objective this split turns on
- introduces [[2018-lopez-scvi]] — the variational (scVI) side of the split
- contrasts [[2019-eraslan-dca]] — the deterministic count-autoencoder (DCA) side
