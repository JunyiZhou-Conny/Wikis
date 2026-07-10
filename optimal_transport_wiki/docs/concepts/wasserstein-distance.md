---
title: Wasserstein distance
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/math
  - topic/wasserstein
distilled_from:
  - "[[2013-cuturi-sinkhorn-distances]]"
  - "[[2014-cuturi-wasserstein-barycenters]]"
  - "[[2023-bunne-cellot-neural-ot]]"
  - "[[2019-peyre-computational-optimal-transport]]"
  - "[[2023-korotin-neural-optimal-transport]]"
---

# Wasserstein distance

The optimal-transport cost itself, viewed as a **distance between probability measures**:
W_p(μ,ν) is the minimal expected cost of transporting μ onto ν under a ground cost ‖x−y‖^p.

## Why it matters / where it shows up

Unlike KL or TV, the Wasserstein distance is **geometry-aware** — it accounts for *how far* mass
must move — so it stays meaningful between measures with disjoint support. This is why it is used
as a loss/geometry in generative modeling, alignment, and single-cell trajectory inference.

## Details

- W₂ (squared-Euclidean cost) is the case used by most ML work, including neural OT
  ([[2023-bunne-cellot-neural-ot]], [[2023-korotin-neural-optimal-transport]]).
- Computing it exactly is an LP; entropic regularization gives the fast **Sinkhorn distance**
  surrogate ([[2013-cuturi-sinkhorn-distances]]).
- The Fréchet mean under $W_p$ is the **Wasserstein barycenter**
  ([[2014-cuturi-wasserstein-barycenters]], [[wasserstein-barycenters]]).
- Full definitions, metric properties, and geodesics: [[2019-peyre-computational-optimal-transport]].

## Related

- background-for [[2013-cuturi-sinkhorn-distances]] — the smoothed, fast approximation
- background-for [[2014-cuturi-wasserstein-barycenters]] — Fréchet means under $W_p^p$
- applies [[2023-bunne-cellot-neural-ot]] — optimizes the W₂ dual with neural potentials
- applies [[2023-korotin-neural-optimal-transport]] — learns W₂ / γ-weak quadratic maps and plans
- introduces [[2019-peyre-computational-optimal-transport]] — reference definitions and properties
- extends [[monge-kantorovich-formulations]] — the distance is the optimal value of those problems
- extends [[wasserstein-barycenters]] — barycenters are Fréchet means of this distance
