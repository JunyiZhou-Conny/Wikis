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
  - "[[2024-kornilov-optimal-flow-matching]]"
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
- **Flow-matching / dynamic approach:** restrict FM vector fields to gradients of convex ICNN
  potentials so one FM step recovers the quadratic Benamou–Brenier OT flow
  ([[2024-kornilov-optimal-flow-matching]]).
- Both rest on OT **duality** ([[monge-kantorovich-formulations]]); stability comes from
  architectural inductive biases (convexity constraints) or saddle-point training schedules.

## Related

- introduces [[2023-bunne-cellot-neural-ot]] — ICNN dual potentials → Monge map
- applies [[2019-yang-scalable-unbalanced-ot-gans]] — GAN-style neural solver, extended to unbalanced OT
- introduces [[2023-korotin-neural-optimal-transport]] — maximin neural solver for strong/weak OT plans
- applies [[2024-kornilov-optimal-flow-matching]] — Optimal Flow Matching: ICNN + FM recovers straight \(W_2\) OT in one step
- extends [[monge-kantorovich-formulations]] — a neural parameterization of the OT dual
