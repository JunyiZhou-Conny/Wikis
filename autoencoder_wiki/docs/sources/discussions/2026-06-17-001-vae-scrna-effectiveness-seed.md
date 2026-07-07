---
title: VAE effectiveness on scRNA-seq — user seed
type: source
status: done
date: 2026-06-17
source_kind: discussion
source_path: ""
authors: ["Conny (oral seed)"]
year: 2026
tags:
  - source
  - domain/ml
  - topic/scrna
  - topic/vae
  - topic/dimensionality-reduction
---

# VAE effectiveness on scRNA-seq — user seed

Raw learning intent captured before research and paper ingest (2026-06-17).

## What I want to understand

How **effective** is an autoencoder — specifically a **variational autoencoder (VAE)** — for **single-cell RNA-seq** dimensionality reduction?

## My current mental model

Typical scRNA pipeline:

1. Start from full gene expression matrix.
2. **Shrink to highly variable genes (HVGs)** — first dimensionality reduction step.
3. Feed HVG matrix into a model; often compress further to a **latent space** (e.g. **50 dimensions**).
4. Use latent representation for downstream tasks (clustering, visualization, other models).

This is a standard **dimensionality reduction** technique in single-cell analysis.

## Architecture assumption

From prior exposure, autoencoders in this setting often look like:

- **Two hidden layers**, commonly **512 → 512** (encoder/decoder MLP).
- Relatively shallow compared to vision models.

**Open question:** Is that architecture actually justified, or just a common default?

## Core questions

1. **How effective is a VAE** vs simpler baselines (PCA, t-SNE, UMAP) for scRNA DR?
2. **How do you evaluate** whether an autoencoder / VAE is *useful* — not just whether it trains?
3. What metrics and benchmarks should I trust?

## What I want from this sprint

- Five **high-standard, heavily cited** papers selected and ingested.
- Structured concepts I can interact with in Obsidian + Cursor.

## Related

- [[2026-06-17-002-vae-scrna-effectiveness-synthesis]]
- [[Autoencoder MOC]]
