---
title: VAE vs PCA, t-SNE, UMAP on scRNA benchmarks
type: concept
status: draft
date: 2026-06-17
tags:
  - concept
  - domain/ml
  - topic/scrna
  - topic/dimensionality-reduction
source_doc: "[[2020-li-dr-benchmark]]"
distilled_from:
  - "[[2020-li-dr-benchmark]]"
  - "[[2026-06-17-002-vae-scrna-effectiveness-synthesis]]"
---

# VAE vs PCA, t-SNE, UMAP on scRNA benchmarks

Large benchmarks find **no universal winner**: t-SNE/UMAP often excel at visualization; VAE/scVI-family methods are **top-tier on several clustering tasks** but dataset-dependent.

## Why it matters

Answers "how effective is a VAE?" with **it depends** — grounded in systematic comparisons, not hype.

## Details

- **PCA** is fast baseline; often competitive on simple datasets.
- **UMAP/t-SNE** optimize visualization; may distort global geometry.
- **VAE** adds generative modeling (denoising, batch, uncertainty) beyond static DR.
- Compare on **your** data with [[evaluating-vae-scrna-metrics]].

## Related

- [[evaluating-vae-scrna-metrics]]
- [[2018-lopez-scvi]]
- [[2020-li-dr-benchmark]]
