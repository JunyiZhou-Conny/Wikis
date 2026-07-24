---
title: "Gromov–Wasserstein Distances and the Metric Approach to Object Matching"
type: source
status: done
date: 2026-07-24
source_kind: paper
tier: A
venue: "Foundations of Computational Mathematics"
year: 2011
authors: ["Mémoli"]
approx_citations: 780
doi: "10.1007/s10208-011-9093-5"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/math
  - domain/literature
  - topic/gromov-wasserstein
  - method/gromov-wasserstein
---

# Gromov–Wasserstein Distances and the Metric Approach to Object Matching

Mémoli, *Foundations of Computational Mathematics* 2011. The canonical theory paper that
defines **Gromov–Wasserstein** distances on metric measure spaces — the foundation for every
relational OT note in this wiki.

## Summary

Classical Gromov–Hausdorff (GH) comparison of metric spaces is theoretically clean but hard to
compute: correspondences are combinatorial, and practical estimators were limited to smooth
shapes. This paper **relaxes** GH by treating objects as **metric measure spaces** (mm-spaces)
and replacing correspondences / \(L^\infty\) with **measure couplings** / \(L^p\), yielding
Gromov–Wasserstein distances \(D_p\) (and Sturm's related \(S_p\)). The resulting metric lives on
isomorphism classes of mm-spaces, admits polynomial-time **lower bounds** via classical shape
invariants, and supports numerical matching without smoothness assumptions.

## Key claims / results

- Objects = compact mm-spaces \((X,d_X,\mu_X)\) with full-support probability \(\mu_X\); equality
  is mm-space isomorphism (isometry pushing \(\mu_X\) to \(\mu_Y\)).
- \(D_p\) is obtained from the GH expression \(\tfrac12\inf_R\|\Gamma_{X,Y}\|_{L^\infty(R\times R)}\)
  by substituting couplings \(\mu\in\mathcal{M}(\mu_X,\mu_Y)\) for correspondences \(R\) and
  \(L^p\) for \(L^\infty\); Sturm's \(S_p\) is the parallel relaxation of the other GH form.
- **Theorem:** for each \(p\in[1,\infty]\), \(D_p\) is a **metric** on isomorphism classes of
  mm-spaces; \(d_{\mathrm{GH}}\le D_\infty\); \(S_p\ge D_p\) with equality at \(p=\infty\);
  \(D_p\) is monotone in \(p\).
- Stability under changing measures or metrics on a fixed space, and consistency under empirical
  sampling of \(\mu_X\).
- Polynomial-time lower bounds via mm-space invariants (\(p\)-diameters, eccentricities,
  global/local distance distributions / shape contexts), linking signature-based shape matching
  into a common metric framework; computational examples on ultrametric spaces and 3D shapes.

## Methodology

- Start from several equivalent GH formulas; “gromovize” Wasserstein–Kantorovich–Rubinstein
  proximity instead of Hausdorff proximity.
- Discrete matching becomes continuous optimization over couplings (softer than combinatorial
  correspondences / QAP); lower bounds reduce to standard transportation problems with costs
  built from invariants.
- Numerical section solves for couplings that realize the distance / matching on toy ultrametrics
  and 3D object pairs.

## Related

- introduces [[gromov-wasserstein-distance]] — canonical definition of GW on metric measure spaces
- extends [[monge-kantorovich-formulations]] — replaces point correspondences by Kantorovich-style
  couplings, then compares intra-space metrics rather than a cross-space cost
- background-for [[wasserstein-distance]] — Wasserstein replaces Hausdorff inside the GH
  construction to get GW
- background-for [[2018-alvarez-melis-gromov-wasserstein-alignment]] — theory root cited by the
  applied GW alignment paper
- background-for [[2019-peyre-computational-optimal-transport]] — surveyed there among OT
  extensions
- [[Sources MOC]]
- [[Optimal Transport MOC]]
