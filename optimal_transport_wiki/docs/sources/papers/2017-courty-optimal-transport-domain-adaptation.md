---
title: "Optimal Transport for Domain Adaptation"
type: source
status: done
date: 2026-07-11
source_kind: paper
tier: A
venue: "IEEE TPAMI 2017"
year: 2017
authors: ["Courty", "Flamary", "Tuia", "Rakotomamonjy"]
approx_citations: 950
doi: "10.1109/TPAMI.2016.2615921"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/wasserstein
  - topic/domain-adaptation
  - method/sinkhorn
  - method/entropic-ot
---

# Optimal Transport for Domain Adaptation

Courty, Flamary, Tuia & Rakotomamonjy, *IEEE TPAMI* 2017 (online 2016). The canonical
**OT-for-domain-adaptation** paper: align source and target feature distributions with a
regularized transport plan, then train on the transported labeled source.

## Summary

Unsupervised domain adaptation is cast as finding a minimal-cost map that pushes the source
empirical measure onto the target while preserving labels. The authors solve a **Kantorovich**
problem with **entropic** (Sinkhorn) regularization, then map each source point to a
**barycentric projection** of its coupling mass onto the target support. They add
**class-aware** regularizers (group-lasso / Laplacian) so same-class source mass stays coherent
under transport, and show a simple cost-mask extension for semi-supervised DA when a few target
labels exist. On visual adaptation benchmarks (Office/Caltech, digits, PIE faces) the OTDA
variants consistently beat then-standard feature-alignment baselines.

## Key claims / results

- Domain drift can be modeled as an unknown (possibly nonlinear) push-forward; recovering a
  Wasserstein-optimal coupling plus barycentric mapping yields a usable labeled training set in
  the target geometry.
- Entropic OT (Cuturi) makes the plan dense and differentiable enough for DA, and is far cheaper
  than exact LP transport on realistic sample sizes.
- **Class regularization** matters: group-lasso (OT-GL) and Laplacian (OT-Laplace) regularizers
  keep same-label source samples from collapsing onto conflicting target points, improving
  downstream 1NN accuracy over plain OT-exact / OT-IT.
- Semi-supervised labels in the target enter as hard (infinite-cost) forbidden matches — no new
  hyperparameters beyond the cost matrix.
- Empirically strong on Office–Caltech, USPS↔MNIST, and PIE pose adaptation; also improves when
  features are already deep/domain-invariant.

## Methodology

- Discrete Kantorovich OT on empirical measures with squared-Euclidean cost; optional entropy
  term solved by Sinkhorn–Knopp.
- Source→target map: barycentric projection
  \(\hat{X}_s = \mathrm{diag}(\gamma\mathbf{1})^{-1}\gamma X_t\).
- Class terms: column-wise group \(\ell_1\)–\(\ell_2\) sparsity over label blocks, and/or graph
  Laplacian smoothness on transported points; generalized conditional gradient wraps Sinkhorn
  linear oracles.
- Classifier: typically 1NN on adapted source features (parameter-free evaluation protocol).

## Related

- introduces [[ot-domain-adaptation]] — OT as unsupervised feature alignment + label transport
- applies [[wasserstein-distance]] — adaptation cost is \(W_2\) geometry between domain measures
- applies [[monge-kantorovich-formulations]] — uses Kantorovich couplings, recovers a Monge-like map via barycentric projection
- applies [[entropic-regularization-sinkhorn]] — Sinkhorn is the scalable inner solver
- extends [[2013-cuturi-sinkhorn-distances]] — builds DA regularizers on top of entropic OT
- contrasts [[2018-alvarez-melis-gromov-wasserstein-alignment]] — OTDA needs a shared feature metric; GW aligns incomparable spaces via intra-domain relations
- background-for [[2019-peyre-computational-optimal-transport]] — monograph situates OTDA among ML applications of computational OT
- [[Sources MOC]]
- [[Optimal Transport MOC]]
