---
title: "Tybalt — VAE latent space from cancer transcriptomes"
type: source
status: done
date: 2026-06-17
source_kind: paper
tier: B
source_path: "sources/raw/vae-scrna-effectiveness/way-2018-tybalt.pdf"
authors: ["Way", "Greene"]
year: 2018
venue: "PLOS Computational Biology"
doi: "10.1371/journal.pcbi.1006508"
approx_citations: 400
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/transcriptomics
  - topic/hyperparameters
---

# Tybalt — variational autoencoder for transcriptome latent space

Way & Greene, *PLOS Computational Biology* 2018. Introduces **Tybalt** VAE for bulk RNA; follow-on work applies to single-cell.

## Summary

Tybalt learns a **low-dimensional latent space** from high-dimensional gene expression using a VAE, enabling visualization and interpretation of transcriptomic variation.

## Key claims

- VAE latent spaces can capture **biologically meaningful** axes of variation.
- **Hyperparameters and architecture matter critically** — companion work shows performance can collapse with wrong settings.

## Methodology

- MLP encoder/decoder with ELBO training on expression matrices.
- Evaluated via **k-means NMI/ARI**, **kNN** label transfer, **silhouette** width on simulated and real data.

## Relevance to your question

- Directly motivates [[hyperparameter-sensitivity-vae-scrna]] — Tybalt's scRNA follow-up (*Parameter tuning is a key part…*, PMC6417816) shows **no DR method wins all cases** and VAE quality depends on tuning.
- Provides concrete **evaluation metrics** you can reuse on your HVG→latent pipeline.

## Related

- extends [[2013-kingma-vae]] — applies the VAE directly to transcriptome expression matrices
- [[2026-06-17-002-vae-scrna-effectiveness-synthesis]]
- [[hyperparameter-sensitivity-vae-scrna]]
- [[evaluating-vae-scrna-metrics]]
- [[autoencoder-hidden-layer-width-scrna]]
- [[Sources MOC]]
