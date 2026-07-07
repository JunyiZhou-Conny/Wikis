---
title: Evaluating VAE usefulness on scRNA-seq
type: concept
status: draft
date: 2026-06-17
tags:
  - concept
  - domain/ml
  - topic/scrna
  - topic/vae
  - topic/evaluation
source_doc: "[[2020-li-dr-benchmark]]"
distilled_from:
  - "[[2020-li-dr-benchmark]]"
  - "[[2018-way-tybalt]]"
  - "[[2026-06-17-002-vae-scrna-effectiveness-synthesis]]"
---

# Evaluating VAE usefulness on scRNA-seq

"No single metric proves a VAE works." Match evaluation to **downstream intent**.

## Why it matters

Low reconstruction loss can coexist with useless latents for clustering or prediction.

## Details

| Goal | Metrics |
|------|-----------|
| Cell-type recovery | **ARI**, **NMI** vs labels |
| Cluster separation | **Silhouette** in latent space |
| Local structure | **kNN preservation**, Jaccard overlap |
| Global structure | Distance correlation, **EMD** |
| Denoising | DE concordance, imputation error |
| Integration | Batch mixing + biology conservation |

Use **≥2 metric families** before trusting a model.

## Related

- [[vae-vs-linear-nonlinear-dr-benchmarks]]
- [[hyperparameter-sensitivity-vae-scrna]]
- [[2020-li-dr-benchmark]]
