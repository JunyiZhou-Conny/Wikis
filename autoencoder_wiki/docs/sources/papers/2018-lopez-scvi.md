---
title: "Deep generative modeling for single-cell transcriptomics (scVI)"
type: source
status: done
date: 2026-06-17
source_kind: paper
tier: A
source_path: "sources/raw/vae-scrna-effectiveness/lopez-2018-scvi.pdf"
authors: ["Lopez", "Regier", "Cole", "Jordan", "Yosef"]
year: 2018
venue: "Nature Methods"
doi: "10.1038/s41592-018-0229-2"
approx_citations: 1178
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/scrna
  - topic/vae
  - method/scvi
---

# Deep generative modeling for single-cell transcriptomics (scVI)

Lopez et al., *Nature Methods* 2018. Foundational **single-cell VAE** (scVI).

## Summary

scVI models scRNA-seq counts with a **variational autoencoder** whose conditional likelihood is **zero-inflated negative binomial (ZINB)**. A low-dimensional latent **z** captures biological variation; additional variables handle library size / technical effects. The method scales via stochastic optimization and supports batch correction, visualization, clustering, and differential expression.

## Key claims

- Probabilistic modeling accounts for **technical noise, dropout, and batch effects**.
- Latent **z** is useful for downstream tasks (clustering, DE, visualization).
- scVI became the **de facto** deep generative baseline in single-cell (scvi-tools ecosystem).

## Methodology

- **Encoder:** neural net outputs variational posterior over z (and library size factor).
- **Decoder:** ZINB parameters per gene given z (and batch).
- **Training:** maximize ELBO; mini-batch scalable.
- Default latent dimension often **10** in software (tunable).

## Relevance to your question

- Defines what a **"serious" scRNA VAE** looks like (not plain MSE on Gaussian data).
- Effectiveness is demonstrated on **multiple analysis tasks**, not reconstruction loss alone.

## Related

- extends [[2013-kingma-vae]] — scVI is a VAE with a ZINB decoder for scRNA counts
- [[2019-lotfollahi-scgen]]
- [[2026-06-17-002-vae-scrna-effectiveness-synthesis]]
- [[vae-elbo-scrna-count-models]]
- [[2021-xu-scanvi]]
- [[Sources MOC]]
