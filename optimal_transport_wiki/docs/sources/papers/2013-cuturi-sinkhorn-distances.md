---
title: "Sinkhorn Distances: Lightspeed Computation of Optimal Transport"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "NeurIPS 2013"
year: 2013
authors: ["Cuturi"]
approx_citations: 6700
doi: "10.5555/2999792.2999868"
source_path: "sources/raw/cuturi-2013-sinkhorn.pdf"
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/wasserstein
  - method/sinkhorn
  - method/entropic-ot
---

# Sinkhorn Distances: Lightspeed Computation of Optimal Transport

Cuturi, *NeurIPS 2013*. The paper that made OT practical for machine learning — entropic
regularization + Sinkhorn scaling. Foundational for essentially every applied OT paper here.

## Summary

Exact discrete OT is a linear program whose cost is prohibitive once histograms exceed a few
hundred bins. Cuturi adds an **entropic regularization** term −λH(Γ) to the transport objective.
The regularized optimum is still a valid distance (the "Sinkhorn distance") and, crucially, has
the closed form Γ* = diag(u) K diag(v) with K = exp(−C/λ), so it can be computed by **Sinkhorn–
Knopp matrix scaling** — a few matrix–vector products — orders of magnitude faster than LP
solvers and trivially GPU-parallel.

## Key claims / results

- Entropic smoothing turns OT into a **strictly convex, differentiable** problem solvable by
  iterative row/column rescaling.
- Several orders of magnitude faster than exact transport solvers; scales OT to ML-sized problems.
- The regularized distance **improves classification** over exact OT on MNIST (regularization acts
  as useful smoothing, not just an approximation).
- As λ → 0 it recovers exact OT; as λ → ∞ the plan → outer product of marginals.

## Methodology

- Regularized primal: min⟨Γ, C⟩ − λH(Γ) over the coupling polytope U(a, b).
- Solved by Sinkhorn iterations a ← p ⊘ Kb, b ← q ⊘ Kᵀa; O(n²) per iteration.

## Related

- introduces [[entropic-regularization-sinkhorn]] — the entropic-OT / Sinkhorn scheme itself
- background-for [[wasserstein-distance]] — a fast smoothed surrogate for the Wasserstein distance
- applies [[monge-kantorovich-formulations]] — regularizes the Kantorovich primal
- background-for [[2019-peyre-computational-optimal-transport]] — the algorithmic core that monograph systematizes
- background-for [[2018-genevay-sinkhorn-divergences]] — Genevay et al. turn Sinkhorn into a debiased generative loss
- background-for [[sinkhorn-divergence]] — entropic OT is the quantity that debiasing corrects
- benchmarks [[2018-alvarez-melis-gromov-wasserstein-alignment]] — used there as the inner solver for GW
- [[Sources MOC]]
- [[Optimal Transport MOC]]
