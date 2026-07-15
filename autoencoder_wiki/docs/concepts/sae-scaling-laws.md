---
title: SAE scaling laws for dictionary width and training steps
type: concept
status: done
date: 2026-07-15
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/sparse-autoencoder
distilled_from:
  - "[[2024-templeton-scaling-monosemanticity]]"
  - "[[2023-bricken-towards-monosemanticity]]"
---

# SAE scaling laws for dictionary width and training steps

**SAE scaling laws** treat sparse-autoencoder training like other large ML jobs: pick dictionary
**width** and **training steps** (hence data) to minimize a proxy loss under a fixed compute
budget, rather than guessing expansion factors by hand.

## Why it matters / where it shows up

Towards Monosemanticity showed SAEs work on a tiny LM
([[2023-bricken-towards-monosemanticity]]), but production residual streams make naive sweeps
impossible. Scaling Monosemanticity ([[2024-templeton-scaling-monosemanticity]]) uses power-law
fits over (features × steps) so a 34M-feature run is compute-optimal rather than arbitrary —
the practical bridge from toy SAEs to frontier models.

## Details

- **Proxy objective:** MSE reconstruction + L1 sparsity (with a fixed L1 coefficient) stands in
  for “dictionary quality” when gold faithfulness metrics are missing.
- **Two compute axes:** number of features \(F\) and training steps; cost ≈ product when input
  dim is fixed; one epoch over activation data.
- **Observed laws:** compute-optimal loss falls roughly as a power of FLOPS; optimal \(F\) and
  steps each scale as power laws (width often rising faster than steps in the tested range);
  optimal learning rate shrinks with budget.
- **Resolution link:** rarer concepts need larger dictionaries — width is not just a
  reconstruction knob but a **feature-resolution** control (related to Bricken’s feature
  splitting).

## Related

- introduces [[2024-templeton-scaling-monosemanticity]] — scaling-law sweeps that sized the 1M/4M/34M Sonnet SAEs
- background-for [[2023-bricken-towards-monosemanticity]] — earlier expansion-factor grid (1×–256×) without compute-optimal allocation
- applies [[sparse-autoencoder-dictionary-learning]] — same overcomplete sparse AE, now budgeted like a foundation-model training run
- background-for [[monosemantic-features-vs-polysemantic-neurons]] — larger compute-optimal dictionaries resolve finer monosemantic features
