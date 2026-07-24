---
title: Gromov-Wasserstein distance
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/math
  - topic/gromov-wasserstein
distilled_from:
  - "[[2011-memoli-gromov-wasserstein]]"
  - "[[2018-alvarez-melis-gromov-wasserstein-alignment]]"
  - "[[2019-peyre-computational-optimal-transport]]"
---

# Gromov-Wasserstein distance

A relational form of OT for measures living in **different / incomparable spaces**: instead of a
cross-space cost, it compares **intra-space pairwise distances**, matching pairs (i,k) to (j,l)
so that within-domain geometries align.

## Why it matters / where it shows up

When there is no shared metric between domains (word embeddings in two languages, cells in
different feature spaces, shapes), classical OT can't define a cost. GW sidesteps this by
transporting *relationships* rather than points — at the price of a quadratic, non-convex
objective.

## Details

- Theory root ([[2011-memoli-gromov-wasserstein]]): objects are metric measure spaces; \(D_p\)
  relaxes Gromov–Hausdorff by using couplings and \(L^p\) norms, and is a metric on isomorphism
  classes of mm-spaces.
- Discrete ML form: min over couplings Γ of Σ L(C_ik, C′_jl) Γ_ij Γ_kl, using within-domain cost
  matrices C, C′ ([[2018-alvarez-melis-gromov-wasserstein-alignment]]).
- Non-convex (a quadratic assignment problem), but solvable by projected gradient where each step
  is an entropic OT (Sinkhorn) solve.
- With L = L², GW½ is a genuine distance on metric-measure spaces
  ([[2011-memoli-gromov-wasserstein]]); surveyed in
  [[2019-peyre-computational-optimal-transport]].

## Related

- introduces [[2011-memoli-gromov-wasserstein]] — canonical GW metric on mm-spaces
- introduces [[2018-alvarez-melis-gromov-wasserstein-alignment]] — GW for unsupervised cross-lingual alignment
- background-for [[2019-peyre-computational-optimal-transport]] — GW among OT extensions
- extends [[monge-kantorovich-formulations]] — a quadratic relative of the Kantorovich coupling problem
- applies [[entropic-regularization-sinkhorn]] — uses Sinkhorn as the inner solver
