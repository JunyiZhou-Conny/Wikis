---
title: "Single-cell RNA-seq denoising using a deep count autoencoder (DCA)"
type: source
status: done
date: 2026-06-17
source_kind: paper
tier: A
source_path: "sources/raw/vae-scrna-effectiveness/eraslan-2019-dca.pdf"
authors: ["Eraslan", "Simon", "Mircea", "Mueller", "Theis"]
year: 2019
venue: "Nature Communications"
doi: "10.1038/s41467-018-07931-2"
approx_citations: 1076
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/scrna
  - topic/autoencoder
  - method/dca
---

# Single-cell RNA-seq denoising using a deep count autoencoder (DCA)

Eraslan et al., *Nature Communications* 2019.

## Summary

**DCA** is a **deep count autoencoder** (not full VAE in the variational sense) using **ZINB / NB loss** to denoise and impute scRNA-seq counts. It models overdispersion, sparsity, and gene-gene dependencies; scales to large datasets.

## Key claims

- Denoising improves downstream clustering, DE, and trajectory inference.
- **Default architecture:** three hidden layers **64 → 32 → 64** (not 512×512).
- Linear scaling with cell count; GPU-optional acceleration.

## Methodology

- Standard autoencoder bottleneck; specialized **count noise model** in the loss.
- Trains on raw/normalized counts depending on pipeline version.
- Evaluated against other imputation/denoising methods on diverse datasets.

## Relevance to your question

- Shows **count-aware autoencoders** are highly effective for **denoising** — a distinct notion of "useful" from clustering-only metrics.
- Contrasts with your **512×512** assumption: published default is **much narrower**.

## Related

- background-for [[2026-06-17-002-vae-scrna-effectiveness-synthesis]] — anchor paper for the effectiveness synthesis
- introduces [[probabilistic-vae-vs-count-autoencoder]] — defines the deterministic count-AE side of that split
- introduces [[autoencoder-hidden-layer-width-scrna]] — its 64-32-64 default anchors the width discussion
- contrasts [[2018-lopez-scvi]] — count autoencoder (denoising) vs full VAE (latent inference)
- applies [[2008-vincent-denoising-autoencoders]] — same reconstruct-clean-from-noise spirit; DCA's "noise" is biological count sparsity with a ZINB/NB loss
- applies [[denoising-autoencoder-corruption-robustness]] — domain-specific instance of DAE-style denoising
- [[Sources MOC]]
