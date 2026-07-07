---
title: Hyperparameter sensitivity of scRNA VAEs
type: concept
status: draft
date: 2026-06-17
tags:
  - concept
  - domain/ml
  - topic/vae
  - topic/scrna
  - topic/hyperparameters
source_doc: "[[2018-way-tybalt]]"
distilled_from:
  - "[[2018-way-tybalt]]"
  - "[[2019-eraslan-dca]]"
---

# Hyperparameter sensitivity of scRNA VAEs

VAE dimensionality reduction quality is **strongly sensitive** to latent dimension, layer depth/width, learning rate, and training epochs.

## Why it matters

A failed VAE run is often **mis-tuning**, not evidence that VAEs don't work.

## Details

- Tybalt/scRNA follow-ups: performance can **collapse** with wrong depth (e.g. three-layer model).
- Latent dim trades noise removal vs biological resolution.
- Treat defaults (512×512, latent=50) as **starting points for grid search**.

## Related

- [[autoencoder-hidden-layer-width-scrna]]
- [[evaluating-vae-scrna-metrics]]
- [[2018-way-tybalt]]
