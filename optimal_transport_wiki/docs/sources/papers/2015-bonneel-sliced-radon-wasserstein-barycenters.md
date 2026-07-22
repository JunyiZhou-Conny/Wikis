---
title: "Sliced and Radon Wasserstein Barycenters of Measures"
type: source
status: done
date: 2026-07-22
source_kind: paper
tier: A
venue: "Journal of Mathematical Imaging and Vision"
year: 2015
authors: ["Bonneel", "Rabin", "Peyré", "Pfister"]
approx_citations: 450
doi: "10.1007/s10851-014-0506-3"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/math
  - domain/literature
  - topic/wasserstein
  - topic/sliced-wasserstein
  - method/sliced-ot
---

# Sliced and Radon Wasserstein Barycenters of Measures

Bonneel, Rabin, Peyré & Pfister, *JMIV* 2015. Canonical formalization of the **sliced
Wasserstein** distance and of two projection-based Wasserstein barycenters — the computational
root of high-dimensional SW methods used across generative modeling and imaging.

## Summary

Exact Wasserstein barycenters in dimension \(d > 1\) are expensive (high-dimensional LPs or
extra-time dynamic formulations). This paper builds on Rabin et al.'s 1-D projection idea and
gives two complementary approximations that reduce multi-measure barycenters to **1-D Wasserstein
problems along directions** \(\theta \in S^{d-1}\):

1. **Radon barycenter** — take Radon projections of the inputs, compute 1-D Wasserstein barycenters
   per direction, then back-project (Eulerian / grid discretization via a discrete Radon transform).
2. **Sliced barycenter** — minimize the sum of sliced-Wasserstein distances to the inputs
   (Lagrangian / point-cloud discretization via smooth gradient descent).

Both inherit translation / scaling / rotation invariances of the true Wasserstein barycenter, at a
fraction of its cost. Applications: color transfer and texture mixing.

## Key claims / results

- Defines the **sliced Wasserstein distance**
  \(\mathrm{SW}^2(\mu_1,\mu_2) = \int_{S^{d-1}} W^2(P_{\theta\#}\mu_1, P_{\theta\#}\mu_2)\,d\theta\)
  as the integrated 1-D Wasserstein cost of projected measures.
- **Radon vs sliced** barycenters solve the same energy over measures on \(\Omega_d\), differing only
  by whether the optimizer is constrained to the range of the Radon transform (Prop. 10).
- Both approximations share the translational / scaling / orthogonal invariances of the exact
  Wasserstein barycenter (Props. 8–9, 11–12).
- For equal-weight point clouds, the sliced energy is \(C^1\) with a Lipschitz gradient given by
  integrating 1-D sorted-matching residuals (Thm. 1) — enabling projected gradient descent.
- Empirically competitive with exact dynamic OT geodesics on simple 2-D examples; practical for
  color harmonization and Gaussian / non-parametric texture mixing.

## Methodology

- 1-D barycenters via inverse cumulative distribution functions (closed form).
- Radon path: Fast Slant Stack discrete Radon + per-angle 1-D barycenters + pseudo-inverse
  back-projection on a fixed grid.
- Sliced path: stochastic / finite-direction Monte Carlo over \(\Theta \subset S^{d-1}\); gradient
  step moves particles by the integrated 1-D assignment residual along each direction.
- Compared against Benamou–Brenier-style proximal geodesic solvers for reference.

## Related

- introduces [[sliced-wasserstein]] — defines SW and the Radon/sliced barycenter constructions
- extends [[wasserstein-distance]] — replaces the full high-d Wasserstein cost by an integral of 1-D costs
- applies [[monge-kantorovich-formulations]] — each projected problem is a classical 1-D OT / Monge map
- background-for [[2019-peyre-computational-optimal-transport]] — Peyré coauthors; the monograph surveys this projection line
- contrasts [[2013-cuturi-sinkhorn-distances]] — projection OT vs entropic high-d Sinkhorn as competing scalability routes
- [[Sources MOC]]
- [[Optimal Transport MOC]]
