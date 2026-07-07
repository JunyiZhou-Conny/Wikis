---
title: scRNA DR pipeline — HVG to latent
type: concept
status: draft
date: 2026-06-17
tags:
  - concept
  - domain/ml
  - topic/scrna
  - topic/dimensionality-reduction
source_doc: "[[2026-06-17-002-vae-scrna-effectiveness-synthesis]]"
distilled_from:
  - "[[2026-06-17-001-vae-scrna-effectiveness-seed]]"
  - "[[2026-06-17-002-vae-scrna-effectiveness-synthesis]]"
---

# scRNA DR pipeline — HVG to latent

Standard single-cell workflow: **full count matrix → HVG subset → nonlinear embedding (VAE/AE) → latent z (e.g. 50D) → downstream**.

## Why it matters

Most VAE papers assume this two-stage compression. Effectiveness depends on **both** HVG choice and latent model quality.

## Details

- HVG reduces genes from ~20k to ~2–4k; removes low-information features.
- Latent z targets denoised biological state for clustering or as input to other models.
- VAE can ingest all genes but compute cost grows; HVG remains common practice.

## Related

- [[vae-elbo-scrna-count-models]]
- [[autoencoder-hidden-layer-width-scrna]]
- [[2018-lopez-scvi]]
