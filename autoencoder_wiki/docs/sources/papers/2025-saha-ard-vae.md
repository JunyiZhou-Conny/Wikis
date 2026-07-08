---
title: "ARD-VAE: A Statistical Formulation to Find the Relevant Latent Dimensions of Variational Autoencoders"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: B
venue: "WACV 2025"
year: 2025
authors: ["Saha", "Joshi", "Whitaker"]
approx_citations: 5
doi: "10.1109/WACV61041.2025.00096"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/hyperparameters
  - method/vae
---

# ARD-VAE: finding the relevant latent dimensions of a VAE

Saha, Joshi & Whitaker, *WACV 2025*. A data-driven way to select the VAE bottleneck size by
letting the model **prune** irrelevant latent axes instead of grid-searching.

## Summary

ARD-VAE replaces the VAE's fixed N(0, I) prior with a **hierarchical (automatic relevance
determination) prior** that gives each latent axis its own precision α. During training,
axes not supported by the data get **large α / near-zero variance** and collapse; the surviving
axes are the "relevant" latent factors. The ELBO is otherwise unchanged. A decoder-based
**relevance score** then ranks axes for a percentage-of-variance cutoff.

## Key claims / results

- The bottleneck dimension is "a crucial design choice … often treated as a hyperparameter
  estimated empirically through trial and error" — ARD-VAE removes that trial and error.
- A hierarchical prior lets the model **learn per-axis variance**; spurious axes shrink toward zero.
- Raw per-axis variance is a **poor selector** — collapsed dimensions keep small non-zero variance,
  so a naive "percentage of variance (as in PCA)" threshold is **non-trivial** on VAE latents.
- Their **weighted relevance score** σ²_w is better; a percentage cutoff (typically explaining
  **99%** of that score) recovers the relevant axes robustly.
- Validated on benchmark image datasets via FID and disentanglement metrics.

## Methodology

- Gamma hyperprior on α (conjugate to the Gaussian scale); estimate α from encoded data.
- Post-training, squash spurious-axis variance via a decoder-sensitivity relevance score, then
  threshold cumulatively.

## Relevance to your question

- Directly addresses "use a PCA-style variance threshold to pick latent dim." Verdict: the *idea*
  transfers, but **not on raw VAE latent variance** — you need a relevance-weighted score first.
  This is the paper that most clearly explains **why the naive PCA-ceiling heuristic fails** for
  standard VAEs.

## Related

- extends [[2013-kingma-vae]] — swaps the fixed VAE prior for a hierarchical ARD prior to prune latent axes
- applies [[choosing-latent-dimension]] — an automatic alternative to sweeping latent dim by hand
- introduces [[passive-latent-dimensions]] — collapses surplus axes to near-zero variance and scores relevance
- contradicts [[hyperparameter-sensitivity-vae-scrna]] — argues latent-dim can be *learned/pruned* rather than only grid-searched
- benchmarks [[2022-pham-pca-ae]] — compared against as an ordered/relevance-based latent method in the PCAE study
- [[Sources MOC]]
- [[Autoencoder MOC]]
