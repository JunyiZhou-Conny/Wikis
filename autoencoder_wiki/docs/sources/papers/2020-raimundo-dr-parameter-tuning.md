---
title: "Tuning parameters of dimensionality reduction methods for single-cell RNA-seq analysis"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: B
venue: "Genome Biology"
year: 2020
authors: ["Raimundo", "Vallot", "Vert"]
approx_citations: 150
doi: "10.1186/s13059-020-02128-7"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/scrna
  - topic/dimensionality-reduction
  - topic/hyperparameters
  - topic/evaluation
---

# Tuning parameters of DR methods for scRNA-seq

Raimundo, Vallot & Vert, *Genome Biology* 2020. A systematic study of **which DR hyperparameters
actually matter** on single-cell data — including the **latent dimension** of autoencoder methods.

## Summary

The paper runs a factorial (ANOVA-style) analysis of the tunable parameters of many scRNA-seq DR
methods (PCA, t-SNE, UMAP, scran, Seurat, ZINB-WaVE, DCA, scVI) and measures their effect on
downstream clustering quality (AMI) and cluster separation (silhouette). It quantifies how much
each parameter helps and whether it needs **dataset-specific** tuning.

## Key claims / results

- Parameter influence is **dataset-dependent**: most parameter×dataset interactions are significant.
- **Latent-space dimension** is flagged as a parameter that benefits from **per-dataset tuning**
  for ZINB-WaVE and (for AMI) scVI.
- **scVI** benefits from dataset-specific tuning of *three* parameters: **latent dimension, number
  of hidden neurons, and training epochs**; DCA benefits from tuning scale-variance and dropout.
- Conclusion: autoencoder-based methods in particular gain from tuning on each dataset — there is
  no universal default.

## Methodology

- Factorial design over each method's parameters across multiple public datasets.
- ANOVA with interactions to attribute performance to parameters and parameter×dataset effects.
- Metrics: AMI vs known labels and silhouette width.

## Relevance to your question

- Empirical scRNA-side evidence that **latent dimension must be tuned per dataset**, not read off a
  fixed rule (PCA-variance or otherwise). Complements the vault's existing "sweep, don't default"
  stance with a formal analysis.

## Related

- benchmarks [[2018-lopez-scvi]] — quantifies which scVI parameters (incl. latent dim) need per-dataset tuning
- benchmarks [[2020-li-dr-benchmark]] — sibling large-scale scRNA DR comparison, same "no universal winner" theme
- extends [[hyperparameter-sensitivity-vae-scrna]] — puts numbers on which VAE/AE knobs matter and when
- applies [[choosing-latent-dimension]] — latent dim as a tuned hyperparameter on real scRNA data
- [[Sources MOC]]
- [[Autoencoder MOC]]
