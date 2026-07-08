---
title: Choosing the latent dimension of an autoencoder / VAE
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - topic/vae
  - topic/hyperparameters
distilled_from:
  - "[[2025-saha-ard-vae]]"
  - "[[2026-zhan-pcae-ordered-latent]]"
  - "[[2020-raimundo-dr-parameter-tuning]]"
  - "[[2022-bonheme-fondue]]"
---

# Choosing the latent dimension of an autoencoder / VAE

How big should the bottleneck be? There is **no universal rule**; the honest target is the data's
**intrinsic dimension**, approached either by tuning + task metrics or by model-based pruning.

## Why it matters / where it shows up

Latent dim trades **noise removal vs resolution**: too small underfits biology / collapses rare
structure; too large wastes capacity and can overfit noise. It is the single most-cited sensitive
knob for scRNA autoencoders.

## The "PCA 95% variance = ceiling" question

A common intuition: run PCA, count PCs for ~95% variance, use that as the latent ceiling. Status:

- **Standard VAE / scVI:** not valid as stated. VAE latent axes are **unordered**, so per-axis
  variance isn't a ranking — a naive PCA threshold is ill-defined ([[2025-saha-ard-vae]]), and
  low-variance axes can still encode rare cell types.
- **PCA-ordered autoencoders** (built for it): valid. [[2026-zhan-pcae-ordered-latent]] and
  [[2022-pham-pca-ae]] engineer ordered latents so a cumulative-variance cutoff (they use **99%**,
  not 95%) works.
- **As a search seed:** fine. PCA variance / scree ([[2019-bahadur-ae-dimension-estimation]]) can
  bound a sweep range, but treat it as a starting guess, not a theorem.

## Details — the practical menu

- **Sweep + task metrics** (e.g. 10/30/50) — the vault default; per-dataset tuning matters
  ([[2020-raimundo-dr-parameter-tuning]], [[hyperparameter-sensitivity-vae-scrna]]).
- **Prune automatically** — ARD prior ([[2025-saha-ard-vae]]) or IDE divergence
  ([[2022-bonheme-fondue]]) find relevant dims without full grid search.
- **Track intrinsic dimension** — size to the data's ID ([[intrinsic-dimension-latent-sizing]]);
  one preprint argues **2–3× ID** to protect rare subtypes ([[2026-ritschel-vae-knowledge-compression]]).

## Related

- applies [[2020-raimundo-dr-parameter-tuning]] — shows scVI latent dim needs per-dataset tuning
- introduces [[2026-zhan-pcae-ordered-latent]] — cumulative-variance selection when latents are PCA-ordered
- contrasts [[2025-saha-ard-vae]] — learn/prune relevant dims instead of a fixed rule
- background-for [[intrinsic-dimension-latent-sizing]] — intrinsic dimension as the underlying target
- extends [[hyperparameter-sensitivity-vae-scrna]] — the vault's existing "sweep, don't default" note
