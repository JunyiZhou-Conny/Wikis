---
title: "Learning single-cell perturbation responses using neural optimal transport (CellOT)"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "Nature Methods"
year: 2023
authors: ["Bunne", "Stark", "Gut", "Sarabia del Castillo", "Levesque", "Lehmann", "Pelkmans", "Krause", "Rätsch"]
approx_citations: 250
doi: "10.1038/s41592-023-01969-x"
source_path: "sources/raw/bunne-2023-cellot.pdf"
tags:
  - source
  - domain/ml
  - domain/literature
  - field/biology
  - topic/neural-ot
  - method/neural-ot
  - method/icnn
---

# Learning single-cell perturbation responses using neural optimal transport (CellOT)

Bunne et al., *Nature Methods* 2023. A flagship **applied neural-OT** paper: learns a
parameterized Monge map between unperturbed and perturbed single cells via input-convex neural
networks. (Provided by user.)

## Summary

Cells are destroyed when measured, so control/perturbed populations are **unpaired**. CellOT
casts perturbation response as an **optimal transport map** T pushing the control distribution
ρ_c to the perturbed distribution ρ_k under a minimal-effort (squared-Euclidean) cost. Instead
of the unstable primal map, it parameterizes the **dual potentials** (f, g) with **input-convex
neural networks (ICNNs)** and recovers the map as T = ∇g (Makkuva et al. 2020). One map is
trained per perturbation; because it is fully parameterized, it predicts responses for *unseen*
cells and patients.

## Key claims / results

- Modeling perturbation as an OT map captures **higher moments / heterogeneity** of the perturbed
  population, not just its mean — beating autoencoder baselines (scGen, cAE) and PopAlign, often
  by an order of magnitude on MMD and r² feature-mean metrics.
- Generalizes **out-of-sample** (unseen lupus patients) and **out-of-distribution** (LPS response
  across species; hematopoietic differentiation).
- Works on scRNA-seq (in a 50-D autoencoder latent) and multiplexed 4i protein imaging.
- Limitation: assumes perturbations move mass by *minimal effort* (Euclidean cost, mass
  conserving); performance drops when perturbations are very strong or involve growth/death — the
  latter motivates **unbalanced** OT extensions.

## Methodology

- **Monge (1)** and **Kantorovich (2)** OT formulations; entropic regularization (Cuturi 2013)
  noted as the standard fast solver, but CellOT instead learns the **dual** (3)–(4).
- Approximates the convex conjugate f* by a second ICNN g → max–min objective over two ICNNs
  (Makkuva et al. 2020); T* = ∇g*.
- ICNN: 4 hidden layers width 64; convexity via nonnegative hidden weights.

## Related

- applies [[monge-kantorovich-formulations]] — parameterizes the Kantorovich dual to recover a Monge map
- introduces [[neural-optimal-transport]] — ICNN dual potentials as a scalable OT-map solver
- background-for [[wasserstein-distance]] — the W₂ objective whose dual it optimizes
- benchmarks [[2019-yang-scalable-unbalanced-ot-gans]] — sibling neural-OT approach; motivates unbalanced extensions for growth/death
- contradicts [[2023-uscidda-monge-gap]] — Monge-gap MLPs drop the ICNN / Brenier constraints CellOT uses; same perturbation-map setting
- extends [[2013-cuturi-sinkhorn-distances]] — cites entropic OT as the fast discrete solver it replaces with a neural dual
- [[Sources MOC]]
- [[Optimal Transport MOC]]
