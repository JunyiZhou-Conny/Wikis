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
  - "[[2020-williams-intro-optimal-transport]]"
  - "[[2013-cuturi-sinkhorn-distances]]"
  - "[[2023-bunne-cellot-neural-ot]]"
  - "[[2019-peyre-computational-optimal-transport]]"
  - "[[2023-korotin-neural-optimal-transport]]"
---

# Wasserstein distance

The optimal-transport cost itself, viewed as a **distance between probability measures**:
W_p(μ,ν) is the minimal expected cost of transporting μ onto ν under a ground cost ‖x−y‖^p.
Also called the **Earth Mover's Distance**.

## Why it matters / where it shows up

Unlike KL or TV, the Wasserstein distance is **geometry-aware** — it accounts for *how far* mass
must move — so it stays meaningful between measures with disjoint support (where KL is often +∞)
and is symmetric. This is why it is used as a loss/geometry in generative modeling, alignment,
and single-cell trajectory inference. Best intuition-first entry:
[[2020-williams-intro-optimal-transport]].

## Details

- W₂ (squared-Euclidean cost) is the case used by most ML work, including neural OT
  ([[2023-bunne-cellot-neural-ot]], [[2023-korotin-neural-optimal-transport]]). Order p=1 is
  often more robust to outliers ([[2020-williams-intro-optimal-transport]]).
- Computing it exactly is an LP; entropic regularization gives the fast **Sinkhorn distance**
  surrogate ([[2013-cuturi-sinkhorn-distances]]).
- Analytic exceptions: 1D via inverse CDFs; Gaussians via Bures — see [[closed-form-wasserstein]].
- Full definitions, metric properties, and geodesics: [[2019-peyre-computational-optimal-transport]].

## Related

- introduces [[2020-williams-intro-optimal-transport]] — intuition-first EMD picture and KL contrast
- background-for [[2013-cuturi-sinkhorn-distances]] — the smoothed, fast approximation
- applies [[2023-bunne-cellot-neural-ot]] — optimizes the W₂ dual with neural potentials
- applies [[2023-korotin-neural-optimal-transport]] — learns W₂ / γ-weak quadratic maps and plans
- introduces [[2019-peyre-computational-optimal-transport]] — reference definitions and properties
- extends [[monge-kantorovich-formulations]] — the distance is the optimal value of those problems
- extends [[closed-form-wasserstein]] — 1D and Gaussian special cases
