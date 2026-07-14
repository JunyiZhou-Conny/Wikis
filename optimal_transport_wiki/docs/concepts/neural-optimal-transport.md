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
  - "[[2024-tong-ot-cfm-minibatch]]"
---

# Neural optimal transport

Parameterize the OT solution with **neural networks** — typically the **dual potentials**, a
**stochastic transport map**, or a **CNF vector field** trained by flow matching — so the
solution applies to continuous, high-dimensional measures and generalizes to unseen samples,
instead of solving a fixed discrete coupling.

## Why it matters / where it shows up

Discrete/Sinkhorn solvers return a coupling over the *training* samples and don't extrapolate.
Neural OT learns a **function** (a map, plan, or flow), so it predicts where new points go —
essential for generative modeling, unpaired translation, and single-cell perturbation /
trajectory prediction.

## Details

- **Dual-potential approach:** learn convex potentials (e.g. via **input-convex neural networks**)
  and recover the Monge map as their gradient; trained as a max–min over two ICNNs
  ([[2023-bunne-cellot-neural-ot]]).
- **Adversarial / maximin map approach:** learn a transport map (and, for unbalanced OT, a scaling
  factor) with GAN-style or dual-maximin updates ([[2019-yang-scalable-unbalanced-ot-gans]],
  [[2023-korotin-neural-optimal-transport]]). Korotin et al. cover **weak** costs and stochastic
  plans \(T(x,z)\), recovering deterministic strong-cost maps as a special case.
- **Flow-matching / OT-CFM approach:** regress a CNF vector field onto conditional OT interpolants
  built from (mini-batch) static couplings — simulation-free dynamic OT
  ([[2024-tong-ot-cfm-minibatch]]).
- These rest on OT **duality** or **dynamic** formulations ([[monge-kantorovich-formulations]]);
  stability comes from architectural inductive biases (convexity), saddle-point schedules, or
  straight OT-conditioned paths.

## Related

- introduces [[2023-bunne-cellot-neural-ot]] — ICNN dual potentials → Monge map
- applies [[2019-yang-scalable-unbalanced-ot-gans]] — GAN-style neural solver, extended to unbalanced OT
- introduces [[2023-korotin-neural-optimal-transport]] — maximin neural solver for strong/weak OT plans
- introduces [[2024-tong-ot-cfm-minibatch]] — OT-CFM: simulation-free CNFs from mini-batch OT plans
- extends [[monge-kantorovich-formulations]] — a neural parameterization of the OT dual / dynamic flow
