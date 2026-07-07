---
title: Autoencoder hidden layer width in scRNA
type: concept
status: draft
date: 2026-06-17
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - topic/scrna
  - topic/hyperparameters
source_doc: "[[2019-eraslan-dca]]"
distilled_from:
  - "[[2019-eraslan-dca]]"
  - "[[2018-way-tybalt]]"
  - "[[2026-06-17-001-vae-scrna-effectiveness-seed]]"
---

# Autoencoder hidden layer width in scRNA

The common **512×512 two-layer MLP** is a **tutorial default**, not an empirical law. Published scRNA autoencoders use **smaller** widths (e.g. DCA **64–32–64**).

## Why it matters

Width and depth control capacity vs overfitting on noisy sparse counts. Wrong architecture → pretty UMAP, poor clustering.

## Details

- More neurons help nonlinear gene interactions but increase overfit risk on small N.
- scVI uses flexible `n_hidden`; Tybalt work shows **precipitous drops** when mis-tuned.
- Always sweep latent dim + hidden width on **your** dataset.

## Related

- [[hyperparameter-sensitivity-vae-scrna]]
- [[evaluating-vae-scrna-metrics]]
- [[2019-eraslan-dca]]
