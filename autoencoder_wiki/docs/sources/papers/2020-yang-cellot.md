---
title: "Predicting cell lineages using autoencoders and optimal transport (CellOT)"
type: source
status: done
date: 2026-06-17
source_kind: paper
tier: B
source_path: "sources/raw/scgen-cellot/yang-2020-cellot.pdf"
authors: ["Yang", "Damodaran", "Zaiman", "Ronen", "Kim", "McCall"]
year: 2020
venue: "PLOS Computational Biology"
doi: "10.1371/journal.pcbi.1007828"
approx_citations: 200
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/scrna
  - topic/autoencoder
  - topic/optimal-transport
  - topic/perturbation
  - method/cellot
---

# Predicting cell lineages using autoencoders and optimal transport (CellOT)

Yang et al., *PLOS Computational Biology* 2020 (vol. 16, e1007828).

## Summary

**CellOT** learns cell-state transitions by coupling **autoencoders** with **optimal transport** to map distributions between conditions (e.g. untreated → treated, early → late lineage). Predictions operate on latent codes or expression space depending on implementation.

## Key claims

- OT provides a principled way to transport mass between single-cell populations.
- Autoencoder bottleneck compresses high-dimensional expression before transport.
- Applicable to **lineage** and **perturbation** prediction tasks.

## Methodology

- Train AE (or related encoder) on expression profiles.
- Estimate transport plan between source and target populations.
- Map source cells toward predicted post-perturbation states.

## Bunne / CellOT codebase (your Arm A)

The PyTorch stack used in your ablation adds **`transport_scgen`**: a simplified recipe where

`shift = mean(latent | target) − mean(latent | source)`

then `decode(encode(x) + shift)`. Default AE: **512×512**, **latent 50**, **β=0** (not VAE). This is **CellOT-flavored scGen transport**, not full OT nor scGen Fig5 arithmetic.

## Relevance to your experiment

- **Arm A** = CellOT **PyTorch AE + global latent shift** (not Yang OT end-to-end in the minimal scgen arm).
- Explains why Arm A is a **framework ablation arm**, not paper replication.
- Pairs with [[2019-lotfollahi-scgen]] for the VAE-vs-AE + recipe gap analysis.

## Related

- [[2019-lotfollahi-scgen]]
- [[latent-arithmetic-vs-global-shift]]
- [[probabilistic-vae-vs-count-autoencoder]]
- [[autoencoder-hidden-layer-width-scrna]]
- [[Sources MOC]]
