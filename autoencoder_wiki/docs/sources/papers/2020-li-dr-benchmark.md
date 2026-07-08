---
title: "Accuracy, robustness and scalability of DR methods for scRNA-seq"
type: source
status: done
date: 2026-06-17
source_kind: paper
tier: A
source_path: "sources/raw/vae-scrna-effectiveness/li-2020-dr-benchmark.pdf"
authors: ["Li", "Ding", "Bender", "Gjoka", "Schieren", "Lopes", "Buikema"]
year: 2020
venue: "Genome Biology"
doi: "10.1186/s13059-019-1898-6"
approx_citations: 900
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/scrna
  - topic/dimensionality-reduction
  - topic/evaluation
---

# Accuracy, robustness and scalability of dimensionality reduction methods for scRNA-seq

Li et al., *Genome Biology* 2020. Large-scale **benchmark of 18 DR methods** on **30 datasets**.

## Summary

Comprehensive comparison of dimensionality reduction for scRNA-seq across neighborhood preservation, clustering, lineage reconstruction, and **computational scalability**. Includes neural / model-based methods alongside PCA, t-SNE, UMAP, etc.

## Key claims

- **No single method wins everywhere** — performance depends on dataset and task.
- Practitioners need **guidelines** for method choice, not folklore defaults.
- Scalability and robustness differ substantially across methods.

## Methodology

- 30 public scRNA-seq datasets, multiple sequencing platforms.
- Metrics for **neighborhood recovery**, clustering accuracy, trajectory inference, runtime.
- Includes deep generative / VAE-family approaches available at time of publication.

## Relevance to your question

- Primary reference for **"how effective is VAE vs alternatives?"** — answer is **conditional**.
- Use this paper's metric families when designing your own evaluation.

## Related

- benchmarks [[2006-hinton-deep-autoencoder]] — runs the "autoencoder vs linear DR" question at scale on scRNA
- background-for [[2026-06-17-002-vae-scrna-effectiveness-synthesis]] — anchor benchmark for the synthesis
- introduces [[evaluating-vae-scrna-metrics]] — supplies the metric families for judging DR usefulness
- introduces [[vae-vs-linear-nonlinear-dr-benchmarks]] — the "no universal winner" head-to-head result
- [[Sources MOC]]
