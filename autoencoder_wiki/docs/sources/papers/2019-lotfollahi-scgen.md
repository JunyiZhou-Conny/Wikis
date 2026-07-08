---
title: "scGen predicts single-cell perturbation responses"
type: source
status: done
date: 2026-06-17
source_kind: paper
tier: A
source_path: "sources/raw/scgen-cellot/lotfollahi-2019-scgen.pdf"
authors: ["Lotfollahi", "Wolf", "Theis"]
year: 2019
venue: "Nature Methods"
doi: "10.1038/s41592-019-0494-8"
approx_citations: 900
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/scrna
  - topic/vae
  - topic/perturbation
  - method/scgen
---

# scGen predicts single-cell perturbation responses

Lotfollahi, Wolf & Theis, *Nature Methods* 2019 (vol. 16, pp. 715–721).

## Summary

**scGen** combines a **variational autoencoder** with **latent-space vector arithmetic** to predict single-cell gene expression under perturbations (drug, infection, stimulation) — including **out-of-sample** settings across cell types, studies, and **species**.

## Key claims

- Learns perturbation responses that **generalize** beyond training conditions.
- Latent arithmetic captures treatment and species shifts (e.g. unstimulated → LPS).
- Enables in silico screening of perturbation effects on atlas-scale data.

## Methodology

- **VAE backbone** (related scVI/scvi-tools ecosystem; official repo uses `VAEArith`).
- Typical architecture in reproductions: **800×800** MLP, **z_dim=100**, BN, dropout, KL term.
- **Prediction:** population-level deltas in latent space + per-cell decoding (Fig5 cross-species recipe in follow-on notebooks).

## Relevance to your experiment

- **Stage 0** targets this paper's **TF `VAEArith` + Fig5 latent arithmetic** (~0.91 pseudobulk R² gate).
- **Arm A (CellOT)** uses a **deterministic AE + `transport_scgen`** — same *family name* (scGen-style shift) but **not** the paper's VAE or Fig5 blending formula.
- Direct bridge between [[vae-elbo-scrna-count-models]] and perturbation prediction (not just DR).

## Related

- extends [[2018-lopez-scvi]] — builds perturbation prediction on the scVI-family VAE latent
- contrasts [[2020-yang-cellot]] — OT-based transport vs scGen's latent vector arithmetic
- introduces [[latent-arithmetic-vs-global-shift]] — the Fig5 latent-arithmetic recipe
- background-for [[2026-06-17-002-vae-scrna-effectiveness-synthesis]] — perturbation-stack anchor
- [[Sources MOC]]
