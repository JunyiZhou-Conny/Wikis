---
title: Neural optimal transport
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/ml
  - topic/neural-ot
  - method/neural-ot
distilled_from:
  - "[[2023-bunne-cellot-neural-ot]]"
  - "[[2019-yang-scalable-unbalanced-ot-gans]]"
  - "[[2023-korotin-neural-optimal-transport]]"
  - "[[2023-uscidda-monge-gap]]"
---

# Neural optimal transport

Parameterize the OT solution with **neural networks** — typically the **dual potentials** or a
**stochastic transport map** — so the solution applies to continuous, high-dimensional measures
and generalizes to unseen samples, instead of solving a fixed discrete coupling.

## Why it matters / where it shows up

Discrete/Sinkhorn solvers return a coupling over the *training* samples and don't extrapolate.
Neural OT learns a **function** (a map or plan), so it predicts where new points go — essential for
generative modeling, unpaired translation, and single-cell perturbation prediction.

## Details

- **Dual-potential approach:** learn convex potentials (e.g. via **input-convex neural networks**)
  and recover the Monge map as their gradient; trained as a max–min over two ICNNs
  ([[2023-bunne-cellot-neural-ot]]).
- **Adversarial / maximin map approach:** learn a transport map (and, for unbalanced OT, a scaling
  factor) with GAN-style or dual-maximin updates ([[2019-yang-scalable-unbalanced-ot-gans]],
  [[2023-korotin-neural-optimal-transport]]). Korotin et al. cover **weak** costs and stochastic
  plans \(T(x,z)\), recovering deterministic strong-cost maps as a special case.
- **Monge-gap regularization:** drop ICNN / \(c\)-concavity architecture constraints; fit any map
  \(T_\theta\) by a pushforward discrepancy plus the Monge gap
  \(\mathcal{M}^c_\rho(T)=\int c(x,T(x))\,d\rho-W_c(\rho,T\sharp\rho)\), which vanishes iff \(T\) is
  \(c\)-optimal ([[2023-uscidda-monge-gap]]). Works for general costs and finite-sample regimes
  where Brenier’s density theorem is a poor architectural prior.
- These rest on OT **duality / Monge optimality** ([[monge-kantorovich-formulations]]); stability
  comes from architectural inductive biases, saddle-point schedules, or explicit optimality
  regularizers.

## Related

- introduces [[2023-bunne-cellot-neural-ot]] — ICNN dual potentials → Monge map
- applies [[2019-yang-scalable-unbalanced-ot-gans]] — GAN-style neural solver, extended to unbalanced OT
- introduces [[2023-korotin-neural-optimal-transport]] — maximin neural solver for strong/weak OT plans
- introduces [[2023-uscidda-monge-gap]] — architecture-free Monge maps via Monge-gap regularization
- extends [[monge-kantorovich-formulations]] — a neural parameterization of the OT dual / Monge problem
