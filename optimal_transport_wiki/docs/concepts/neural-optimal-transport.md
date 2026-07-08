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
---

# Neural optimal transport

Parameterize the OT solution with **neural networks** — typically the **dual potentials** — so
the transport map applies to continuous, high-dimensional measures and generalizes to unseen
samples, instead of solving a fixed discrete coupling.

## Why it matters / where it shows up

Discrete/Sinkhorn solvers return a coupling over the *training* samples and don't extrapolate.
Neural OT learns a **function** (a map), so it predicts where new points go — essential for
generative modeling and single-cell perturbation prediction.

## Details

- **Dual-potential approach:** learn convex potentials (e.g. via **input-convex neural networks**)
  and recover the Monge map as their gradient; trained as a max–min over two ICNNs
  ([[2023-bunne-cellot-neural-ot]]).
- **Adversarial approach:** learn a transport map (and, for unbalanced OT, a scaling factor) with
  GAN-style alternating updates ([[2019-yang-scalable-unbalanced-ot-gans]]).
- Both rest on OT **duality** ([[monge-kantorovich-formulations]]); stability comes from
  architectural inductive biases (convexity constraints).

## Related

- introduces [[2023-bunne-cellot-neural-ot]] — ICNN dual potentials → Monge map
- applies [[2019-yang-scalable-unbalanced-ot-gans]] — GAN-style neural solver, extended to unbalanced OT
- extends [[monge-kantorovich-formulations]] — a neural parameterization of the OT dual
