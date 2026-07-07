---
title: "scANVI — harmonization and annotation with deep generative models"
type: source
status: done
date: 2026-06-17
source_kind: paper
tier: B
source_path: "sources/raw/vae-scrna-effectiveness/xu-2021-scanvi.pdf"
authors: ["Xu", "Wang", "Wolf", "Theis", "Plein"]
year: 2021
venue: "Molecular Systems Biology"
doi: "10.15252/msb.20209620"
approx_citations: 600
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/scrna
  - topic/vae
  - method/scanvi
---

# scANVI — probabilistic harmonization and annotation of scRNA-seq

Xu et al., *Molecular Systems Biology* 2021. Extends **scVI** with semi-supervised latent structure.

## Summary

**scANVI** builds on scVI to integrate datasets (batch harmonization) while using cell-type labels when available. Latent **z** remains the workhorse representation; hierarchical structure separates batch, cell type, and residual biology.

## Key claims

- Deep generative models provide a **principled** approach to integration vs ad hoc correction.
- Semi-supervision improves **latent interpretability** for annotated atlases.
- Demonstrates scVI-family models are not only for DR — also for **integration + annotation**.

## Methodology

- Extends scVI graphical model with label-conditioned mixture components.
- Trained via variational inference; uses scvi-tools stack.

## Relevance to your question

- Shows **effectiveness** of VAE-style latents on **real-world integration tasks** beyond static clustering.
- If your downstream goal is feeding latents into another model on **integrated** data, scANVI is a reference point.

## Related

- [[2018-lopez-scvi]]
- [[2026-06-17-002-vae-scrna-effectiveness-synthesis]]
- [[vae-elbo-scrna-count-models]]
- [[Sources MOC]]
