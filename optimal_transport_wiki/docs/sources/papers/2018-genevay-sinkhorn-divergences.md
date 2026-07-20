---
title: "Learning Generative Models with Sinkhorn Divergences"
type: source
status: done
date: 2026-07-20
source_kind: paper
tier: A
venue: "AISTATS 2018"
year: 2018
authors: ["Genevay", "Peyré", "Cuturi"]
approx_citations: 780
doi: "10.48550/arXiv.1706.00292"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/wasserstein
  - method/sinkhorn
  - method/entropic-ot
---

# Learning Generative Models with Sinkhorn Divergences

Genevay, Peyré & Cuturi, *AISTATS 2018*. Canonical introduction of the **Sinkhorn loss /
Sinkhorn divergence** as a tractable OT-based training criterion for large-scale generative
models. Tier A as the method-defining paper for debiased entropic OT losses in ML.

## Summary

Training generative models with unregularized Wasserstein distances is hard: OT is expensive,
non-smooth, and has poor high-dimensional sample complexity. This paper replaces the OT fitting
criterion with a **Sinkhorn loss** — entropically regularized OT evaluated by a fixed number of
Sinkhorn iterations and differentiated end-to-end (auto-diff through the scaling layers). The
**debiased** form
\(\overline{W}_{c,\varepsilon}(\mu,\nu)=2W_{c,\varepsilon}(\mu,\nu)-W_{c,\varepsilon}(\mu,\mu)-W_{c,\varepsilon}(\nu,\nu)\)
interpolates between pure OT (\(\varepsilon\to 0\)) and an MMD / energy-distance regime
(\(\varepsilon\to\infty\)), so one can trade OT geometry against MMD-like sample complexity and
unbiased mini-batch gradients.

## Key claims / results

- Defines the **Sinkhorn loss** (debiased entropic OT) and proves the ε-interpolation between
  Wasserstein and MMD / energy distance.
- Gives a **primal, Sinkhorn-autodiff** training scheme: L Sinkhorn scaling steps act as extra
  pooling layers; SGD + automatic differentiation yields stable gradients without differentiating
  dual OT potentials.
- Shows that moderate ε inherits OT geometry while mitigating the \(O(n^{-1/d})\) sample-complexity
  pathology of unregularized OT.
- Empirically trains deep generative models under this loss on standard image benchmarks.

## Methodology

- Discrete mini-batch Sinkhorn on cost matrix \(c(g_\theta(z_i), y_j)\); Gibbs kernel
  \(K=\exp(-c/\varepsilon)\); L alternating row/column scalings.
- Loss is the debiased Sinkhorn objective on the resulting coupling; parameters of \(g_\theta\)
  updated by backprop through the unrolled iterations.

## Related

- introduces [[sinkhorn-divergence]] — debiased entropic OT loss and its OT↔MMD interpolation
- extends [[2013-cuturi-sinkhorn-distances]] — turns Sinkhorn distances into a generative training loss via debiasing + autodiff
- applies [[entropic-regularization-sinkhorn]] — uses finite Sinkhorn iterations as differentiable layers
- background-for [[wasserstein-distance]] — recovers Wasserstein as ε→0; targets geometry-aware generative fitting
- background-for [[2019-sejourne-unbalanced-sinkhorn-divergences]] — Séjourné et al. extend this debiasing to unbalanced OT
- applies [[2019-peyre-computational-optimal-transport]] — sits in the computational-OT toolkit that monograph surveys
- [[Sources MOC]]
- [[Optimal Transport MOC]]
