---
title: VAE effectiveness on scRNA-seq — synthesis
type: source
status: done
date: 2026-06-17
source_kind: discussion
source_path: ""
authors: ["Cursor ingest sprint"]
year: 2026
tags:
  - source
  - domain/ml
  - topic/scrna
  - topic/vae
  - topic/dimensionality-reduction
  - topic/evaluation
---

# VAE effectiveness on scRNA-seq — synthesis

Master note for topic sprint 2026-06-17. Integrates user seed + five anchor papers.

## Short answer to your question

**VAEs can be highly effective for scRNA-seq**, but they are **not uniformly best**. Benchmarks show:

- On **clustering / cell-type recovery**, VAE-based methods (scVI, Tybalt) often rank **top-tier** on several real datasets, but **t-SNE / UMAP sometimes win** depending on dataset and metrics.
- On **denoising / imputation**, count-aware autoencoders (**DCA**) are a strong, widely adopted choice.
- **Effectiveness is highly sensitive to hyperparameters** (latent dim, layer widths, depth, learning rate) — a default 512×512 two-layer MLP is **not guaranteed** optimal; Tybalt/scVI papers explicitly tune these.
- **Evaluation must be task-specific**: clustering (ARI, NMI), local structure (kNN preservation), global structure (distance correlation), silhouette separation, and denoising benchmarks (DE concordance, imputation error).

There is **no single metric** that proves a VAE is "good"; you pick metrics aligned with downstream use (clustering vs trajectory vs batch correction vs denoising).

## Your pipeline in field language

```
raw counts → (normalize / select HVGs) → encoder → latent z (e.g. 50D) → downstream
```

- **HVG selection** is still standard pre-processing; VAE does not replace it in most workflows (though model can take all genes).
- **Latent dim ~50** is plausible; scVI defaults are often **10–30** but 50 is common in practice. Too low → underfit biology; too high → overfit noise.
- **512×512** appears in blog/code examples; published models vary (**DCA** default: 64→32→64; **scVI** uses flexible MLP width). Treat 512×512 as a **hypothesis to tune**, not a law.

## Five anchor papers (why these)

| Paper | Role | ~Citations |
|-------|------|------------|
| [[2018-lopez-scvi]] | Foundational **probabilistic VAE** for scRNA (ZINB, batch, latent z) | ~1,200 |
| [[2019-eraslan-dca]] | **Count autoencoder** for denoising; concrete AE architecture & scalability | ~1,100 |
| [[2020-li-dr-benchmark]] | **Systematic benchmark** of 18 DR methods on 30 datasets | ~900 |
| [[2018-way-tybalt]] | **VAE for transcriptomes** + shows parameter tuning matters | ~400 |
| [[2021-xu-scanvi]] | scVI **ecosystem extension** (semi-supervised, harmonization) | ~600 |

See `sources/raw/vae-scrna-effectiveness/README.md` for PDF manifest.

## How to evaluate "is this VAE useful?"

| If your goal is… | Evaluate with… |
|------------------|----------------|
| Cell-type clustering | ARI, NMI vs known labels; silhouette in latent space |
| Local neighborhood fidelity | kNN preservation, Jaccard overlap of kNN graphs |
| Global geometry | Distance correlation, EMD between distance matrices |
| Denoising / imputation | DE gene recovery, MSE on held-out counts, biological plausibility |
| Batch correction | Batch mixing vs biology conservation (e.g. scIB-style metrics) |
| Downstream model input | Performance of *your* downstream task (not just DR metrics) |

**Red flags:** great UMAP plot but poor ARI; latent space collapses (all cells similar); needs heavy tuning but you use defaults.

## Correcting / enriching your seed

| Your statement | Research adjustment |
|----------------|---------------------|
| "VAE usually two layers 512×512" | Common in tutorials; **published defaults differ** (DCA 64-32-64; scVI tunable). Always ablate width/depth/latent dim. |
| "Latent dim 50" | Reasonable; scVI often uses **10–30** by default — compare sweep. |
| "How effective?" | **Task-dependent** — cite [[2020-li-dr-benchmark]]: no one-size-fits-all winner. |
| "How evaluate?" | Combine **multiple metrics** — cite [[2018-way-tybalt]] + structure-preservation literature. |

## Concepts distilled from this sprint

- [[scrna-dr-pipeline-hvg-to-latent]]
- [[vae-elbo-scrna-count-models]]
- [[autoencoder-hidden-layer-width-scrna]]
- [[evaluating-vae-scrna-metrics]]
- [[vae-vs-linear-nonlinear-dr-benchmarks]]
- [[hyperparameter-sensitivity-vae-scrna]]
- [[probabilistic-vae-vs-count-autoencoder]]

## Open questions (for your next interact session)

1. On **your** dataset, is the goal clustering, denoising, or feeding a downstream predictor?
2. Will you compare against **PCA → 50** and **UMAP** baselines on the same metrics?
3. Do you want a **concrete architecture sweep** (latent 10/30/50; hidden 128/512)?

## Related

- [[2026-06-17-001-vae-scrna-effectiveness-seed]]
- [[Sources MOC]]
- [[Autoencoder MOC]]
