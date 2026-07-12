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
  - "[[2023-shi-diffusion-schrodinger-bridge-matching]]"
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
- **Bridge / path-measure approach:** learn SDE drifts by regressing on reference bridges so the
  induced path measure solves a Schrödinger bridge ([[2023-shi-diffusion-schrodinger-bridge-matching]],
  [[schrodinger-bridge]]) — dynamic entropic OT rather than a static dual.
- Dual/map methods rest on OT **duality** ([[monge-kantorovich-formulations]]); bridge methods rest
  on reciprocal-class / Markovian projections. Stability comes from convexity constraints,
  saddle-point schedules, or iterative fitting.

## Related

- introduces [[2023-bunne-cellot-neural-ot]] — ICNN dual potentials → Monge map
- applies [[2019-yang-scalable-unbalanced-ot-gans]] — GAN-style neural solver, extended to unbalanced OT
- introduces [[2023-korotin-neural-optimal-transport]] — maximin neural solver for strong/weak OT plans
- applies [[2023-shi-diffusion-schrodinger-bridge-matching]] — neural drifts for dynamic EOT / SB
- extends [[monge-kantorovich-formulations]] — a neural parameterization of the OT dual
- contrasts [[schrodinger-bridge]] — path-space EOT vs static dual/map neural OT
