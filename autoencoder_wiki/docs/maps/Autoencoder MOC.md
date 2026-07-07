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

### Concepts (draft — interact to refine)

- [[scrna-dr-pipeline-hvg-to-latent]]
- [[vae-elbo-scrna-count-models]]
- [[autoencoder-hidden-layer-width-scrna]]
- [[evaluating-vae-scrna-metrics]]
- [[vae-vs-linear-nonlinear-dr-benchmarks]]
- [[hyperparameter-sensitivity-vae-scrna]]
- [[probabilistic-vae-vs-count-autoencoder]]
- [[latent-arithmetic-vs-global-shift]]

## General topics (planned)

- Vanilla autoencoder (encoder / decoder / bottleneck)
- Denoising / sparse autoencoders
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
