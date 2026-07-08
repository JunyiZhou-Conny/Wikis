---
title: "Scaling Algorithms for Unbalanced Transport Problems"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "Mathematics of Computation"
year: 2018
authors: ["Chizat", "Peyré", "Schmitzer", "Vialard"]
approx_citations: 500
doi: "10.1090/mcom/3303"
source_path: "sources/raw/chizat-2018-scaling-algorithms.pdf"
tags:
  - source
  - domain/math
  - domain/literature
  - topic/unbalanced-ot
  - method/sinkhorn
  - method/unbalanced-ot
---

# Scaling Algorithms for Unbalanced Transport Problems

Chizat, Peyré, Schmitzer & Vialard, *Mathematics of Computation* 2018. The **algorithmic**
companion to the unbalanced-OT theory: generalizes Sinkhorn to unequal-mass measures.

## Summary

Extends the entropic-regularization / Sinkhorn scheme to the **unbalanced** setting. The hard
marginal constraints of classical OT are replaced by soft **divergence penalties** (e.g. KL),
and the resulting problems are solved by fast, highly parallelizable **diagonal-scaling
iterations** — generalizations of the Sinkhorn algorithm. The same machinery handles unbalanced
transport, unbalanced gradient flows, and unbalanced barycenters.

## Key claims / results

- A single scaling-iteration framework solves a **generic class** of unbalanced problems by only
  pointwise multiplications on the coupling.
- Recovers standard Sinkhorn as the balanced special case; changing the marginal-penalty
  function (KL, TV, range constraints) changes the problem within one algorithm.
- Applications: 2-D shape modification, color transfer, growth models, barycenters.

## Methodology

- Entropic regularization + proximal/diagonal scaling; marginal fidelity via convex divergence
  penalties instead of equality constraints.

## Related

- extends [[2018-chizat-unbalanced-ot-formulations]] — turns the static unbalanced formulation into fast solvers
- applies [[entropic-regularization-sinkhorn]] — generalizes Sinkhorn scaling to soft marginals
- introduces [[balanced-vs-unbalanced-ot]] — the marginal-relaxation mechanism, algorithmically
- applies [[wasserstein-fisher-rao-metric]] — its scaling iterations compute this metric's transport
- extends [[2013-cuturi-sinkhorn-distances]] — unbalanced generalization of entropic OT
- benchmarks [[2019-sejourne-unbalanced-sinkhorn-divergences]] — later debiases these unbalanced Sinkhorn costs
- [[Sources MOC]]
- [[Optimal Transport MOC]]
