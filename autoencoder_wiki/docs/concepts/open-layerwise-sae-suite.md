---
title: Open layer-wise SAE suite
type: concept
status: done
date: 2026-07-23
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/sparse-autoencoder
distilled_from:
  - "[[2024-lieberum-gemma-scope]]"
  - "[[2023-bricken-towards-monosemanticity]]"
---

# Open layer-wise SAE suite

An **open layer-wise SAE suite** is a public release of sparse autoencoders trained at *every*
(or nearly every) layer and major sublayer site of a language model — not just one residual
stream — so circuit-style and multi-site analyses become possible without re-paying training cost.

## Why it matters / where it shows up

Early SAE demos prove monosemantic features on small or single-site setups
([[2023-bricken-towards-monosemanticity]]). Ambitious uses (circuits across depth, attention vs
MLP vs residual comparisons, IT vs PT) need **matched dictionaries everywhere**. Comprehensive
open suites ([[2024-lieberum-gemma-scope]]) turn SAEs from a lab artifact into shared
infrastructure.

## Details

- **Coverage dimensions:** model size, layer index, site (attn / MLP / residual), dictionary
  width, and sparsity (L0) — often released as a grid so users pick a point on the
  sparsity–fidelity Pareto front.
- **Why “everywhere”:** residual SAEs alone miss site-specific computation; attention and MLP
  SAEs enable finer causal graphs, but only if they exist at the layers you care about.
- **Eval that travels with the release:** delta LM loss and FVU (or equivalent) per SAE, so
  quality is comparable without re-running training.
- **Distinct from a method paper:** the suite may use an existing SAE variant (e.g. JumpReLU);
  the contribution is **breadth + openness**, not necessarily a new encoder nonlinearity.

## Related

- introduces [[2024-lieberum-gemma-scope]] — Gemma Scope as the canonical open all-layers JumpReLU suite on Gemma 2
- background-for [[2023-bricken-towards-monosemanticity]] — single-model SAE success that motivates scaling coverage to full open LMs
- applies [[sparse-autoencoder-dictionary-learning]] — the shared training recipe the suite instantiates at many sites
- applies [[monosemantic-features-vs-polysemantic-neurons]] — suite weights let others probe monosemanticity beyond the original demo model
