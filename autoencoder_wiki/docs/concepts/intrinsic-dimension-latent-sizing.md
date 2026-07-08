---
title: Intrinsic dimension as the target for latent sizing
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - topic/vae
  - topic/dimensionality-reduction
distilled_from:
  - "[[2022-bonheme-fondue]]"
  - "[[2019-bahadur-ae-dimension-estimation]]"
  - "[[2025-biondo-intrinsic-dimension-expression]]"
  - "[[2026-ritschel-vae-knowledge-compression]]"
---

# Intrinsic dimension as the target for latent sizing

The principled quantity behind "how many latent dimensions do I need" is the data's **intrinsic
dimension (ID)** — the number of underlying degrees of freedom — not a fixed PCA variance cutoff.

## Why it matters / where it shows up

Compressing **below** the ID loses irrecoverable information; provisioning **far above** it just
adds passive/unused dimensions. So ID is the natural anchor for choosing the bottleneck.

## Details

- **Estimators disagree:** PCA-based counts (PCs for X% variance, eigenvalue entropy) are one
  family; geometric estimators (TwoNN) are often more robust to curvature/outliers — biology work
  prefers the latter ([[2025-biondo-intrinsic-dimension-expression]]).
- **AE-native signals:** singular-value proxies from AE layers ([[2019-bahadur-ae-dimension-estimation]]);
  divergence between mean vs sampled latent IDE flags **passive variables** in VAEs
  ([[2022-bonheme-fondue]]).
- **Over-provision for rare structure:** because rare subtypes are forgotten first at the ID
  threshold, one preprint recommends latent dim ≈ **2–3× ID** and monitoring per-dimension KL
  ([[2026-ritschel-vae-knowledge-compression]]).
- **Caveat:** three of the four sources here are tier-C preprints — treat the specific recipes as
  suggestive, not settled.

## Related

- introduces [[2022-bonheme-fondue]] — passive-variable / IDE divergence to detect the right size
- applies [[2019-bahadur-ae-dimension-estimation]] — singular-value proxies for AE dimension estimation
- background-for [[2025-biondo-intrinsic-dimension-expression]] — scRNA intrinsic-dimension estimates
- extends [[choosing-latent-dimension]] — the target quantity behind the latent-dim choice
