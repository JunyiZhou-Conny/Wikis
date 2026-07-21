---
title: Autoencoder MOC
type: moc
tags:
  - moc
  - domain/ml
---

# Autoencoder MOC

Single-cell VAE / autoencoder topic index.

### Foundations

- [[2006-hinton-deep-autoencoder]] — the original **deep autoencoder** (encoder/decoder/bottleneck, beats PCA). Tier A. Root of the general-AE thread.
- [[2013-kingma-vae]] — the original **VAE** (reparameterization trick, ELBO). Tier A. Root of the VAE thread below.

### Perturbation prediction stack (refs 12–14)

- [[2018-lopez-scvi]] — scVI, foundational scRNA **VAE** (Lopez et al. 2018)
- [[2019-lotfollahi-scgen]] — scGen **VAE + latent arithmetic** (Lotfollahi et al. 2019)
- [[2020-yang-cellot]] — CellOT **AE + optimal transport** (Yang et al. 2020)

Concept: [[latent-arithmetic-vs-global-shift]] — Stage 0 Fig5 vs Arm A `transport_scgen`

### Topic sprint — DR & evaluation (2026-06-17)

Master notes: [[2026-06-17-002-vae-scrna-effectiveness-synthesis]] · Seed: [[2026-06-17-001-vae-scrna-effectiveness-seed]]

### Anchor papers

- [[2018-lopez-scvi]] — scVI (~1.2k citations)
- [[2019-eraslan-dca]] — DCA (~1.1k citations)
- [[2020-li-dr-benchmark]] — DR benchmark (~900 citations)
- [[2018-way-tybalt]] — Tybalt VAE + tuning (~400 citations)
- [[2021-xu-scanvi]] — scANVI extension (~600 citations)

### Latent-dimension selection & the PCA connection (2026-07-07 batch)

*Does PCA explained variance set a ceiling for the autoencoder latent dim?* Ingested sources:

- [[2019-rolinek-vae-pca-directions]] — **why** VAE latents resemble PCA directions (CVPR 2019). Tier A.
- [[2020-bao-regularized-lae-pca]] — LAEs recover *ordered* PCs only with regularization (NeurIPS 2020). Tier A.
- [[2025-saha-ard-vae]] — ARD prior prunes irrelevant VAE latent axes (WACV 2025). Tier B.
- [[2022-pham-pca-ae]] — autoencoder with PCA-ordered, independent latents (JMIV 2022). Tier B.
- [[2020-raimundo-dr-parameter-tuning]] — scVI latent dim needs per-dataset tuning (Genome Biology 2020). Tier B.
- [[2025-biondo-intrinsic-dimension-expression]] — intrinsic dimension of scRNA expression (Nucleic Acids Research 2025). Tier B.
- [[2026-zhan-pcae-ordered-latent]] — cumulative-variance latent selection via ordered PCAE. **Tier C (preprint)**.
- [[2019-bahadur-ae-dimension-estimation]] — singular-value proxies for AE dimension estimation. **Tier C (preprint)**.
- [[2022-bonheme-fondue]] — FONDUE: intrinsic-dim divergence to size VAE latents. **Tier C (preprint)**.
- [[2026-ritschel-vae-knowledge-compression]] — what VAEs forget first under compression. **Tier C (preprint)**.

Concepts: [[choosing-latent-dimension]] · [[linear-autoencoder-pca-equivalence]] · [[intrinsic-dimension-latent-sizing]] · [[passive-latent-dimensions]]

### Concepts (draft — interact to refine)

- [[choosing-latent-dimension]]
- [[linear-autoencoder-pca-equivalence]]
- [[intrinsic-dimension-latent-sizing]]
- [[passive-latent-dimensions]]
- [[scrna-dr-pipeline-hvg-to-latent]]
- [[vae-elbo-scrna-count-models]]
- [[autoencoder-hidden-layer-width-scrna]]
- [[evaluating-vae-scrna-metrics]]
- [[vae-vs-linear-nonlinear-dr-benchmarks]]
- [[hyperparameter-sensitivity-vae-scrna]]
- [[probabilistic-vae-vs-count-autoencoder]]
- [[latent-arithmetic-vs-global-shift]]
- [[sparse-autoencoder-dictionary-learning]]
- [[monosemantic-features-vs-polysemantic-neurons]]
- [[gated-sae]]

### Sparse autoencoders & monosemantic features (2026-07-10)

*Planned "denoising / sparse autoencoders" thread — frontier interpretability use of AEs:*

- [[2023-bricken-towards-monosemanticity]] — Anthropic SAE dictionary learning on LM MLP activations (Transformer Circuits 2023). Tier A.
- [[2024-rajamanoharan-gated-saes]] — DeepMind **Gated SAE** (gate vs magnitude; L1-on-gate; NeurIPS 2024). Tier A.

Concepts: [[sparse-autoencoder-dictionary-learning]] · [[monosemantic-features-vs-polysemantic-neurons]] · [[gated-sae]]

## General topics (planned)

- Vanilla autoencoder (encoder / decoder / bottleneck)
- Denoising autoencoders (sparse AE thread started above)
- Applications beyond scRNA

## All concepts

```dataview
TABLE status, date, source_doc
FROM "concepts"
WHERE type = "concept"
SORT date DESC
```

## Sources

```dataview
TABLE source_kind, file.folder AS folder, date
FROM "sources"
WHERE type = "source"
SORT date DESC
```

## Related

- [[Home MOC]]
- [[Sources MOC]]
