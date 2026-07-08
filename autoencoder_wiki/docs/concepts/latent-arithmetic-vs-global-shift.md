---
title: Latent arithmetic vs global shift (scGen Fig5 vs transport_scgen)
type: concept
status: draft
date: 2026-06-17
tags:
  - concept
  - domain/ml
  - topic/scrna
  - topic/vae
  - topic/perturbation
source_doc: "[[2019-lotfollahi-scgen]]"
distilled_from:
  - "[[2019-lotfollahi-scgen]]"
  - "[[2020-yang-cellot]]"
---

# Latent arithmetic vs global shift (scGen Fig5 vs transport_scgen)

Two ways to predict perturbation effects in latent space — **not interchangeable**.

## Fig5 / Stage 0 (scGen paper recipe)

- Build **delta_1** = mouse LPS − mouse unst, **delta_2** = rat unst − mouse unst.
- Predict: `0.5 × (rat_unst + delta_1 + delta_2 + mouse_LPS)` in latent space, then decode.
- Uses **mouse stimulated cells at inference**; cross-species blending.

## transport_scgen / Arm A (CellOT)

- `shift = mean(LPS6) − mean(unst)` on **train split only**.
- Per cell: `decode(encode(x) + shift)` for rat unst eval cells.
- **Single global vector**; no mouse at inference; no 0.5 blend.

## Why it matters

Same pseudobulk R² metric can compare **different prediction problems**. Stage 0 ~0.91 is tied to Fig5; Arm A measures CellOT stack under scGen **data** regime, not scGen **method**.

## Related

- introduces [[2019-lotfollahi-scgen]] — the scGen Fig5 latent-arithmetic recipe
- contrasts [[2020-yang-cellot]] — the CellOT `transport_scgen` global-shift recipe
- background-for [[vae-elbo-scrna-count-models]] — both recipes operate on a VAE/AE latent
- applies [[evaluating-vae-scrna-metrics]] — pseudobulk R² and related metrics compare the two
