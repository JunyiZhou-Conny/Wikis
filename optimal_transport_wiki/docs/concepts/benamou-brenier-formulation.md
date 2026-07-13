---
title: Benamou–Brenier dynamic formulation
type: concept
status: done
date: 2026-07-13
tags:
  - concept
  - domain/math
  - topic/wasserstein
  - topic/dynamic-ot
  - method/benamou-brenier
distilled_from:
  - "[[2000-benamou-dynamic-formulation]]"
  - "[[2018-chizat-unbalanced-ot-formulations]]"
  - "[[2019-peyre-computational-optimal-transport]]"
---

# Benamou–Brenier dynamic formulation

The **dynamic** (fluid-mechanics) view of quadratic optimal transport: $W_2^2(\mu,\nu)$ is the
least kinetic energy of a continuum density–velocity pair that morphs $\mu$ into $\nu$ while
obeying the continuity equation — equivalently, the length of the Wasserstein geodesic.

## Why it matters / where it shows up

It supplies geodesics, displacement interpolants, and a convex computational path that avoids the
Monge–Ampère PDE. Almost every later “dynamic OT” construction — unbalanced WFR/Hellinger–
Kantorovich geodesics, gradient flows in Wasserstein space, and many neural / Schrödinger-bridge
flows — starts from this action.

## Details

- Action: minimize $\int_0^1\int \rho|v|^2$ s.t. $\partial_t\rho+\nabla\cdot(\rho v)=0$ with fixed
  endpoints ([[2000-benamou-dynamic-formulation]]).
- Optimal velocity is a pressureless potential flow; the time path $\rho_t$ is the McCann
  displacement interpolant when unique.
- **Unbalanced** extensions add a local growth / Fisher–Rao term in the action, recovering WFR
  ([[2018-chizat-unbalanced-ot-formulations]], [[wasserstein-fisher-rao-metric]]).
- Surveyed as a core computational-OT primitive alongside Sinkhorn and barycenters
  ([[2019-peyre-computational-optimal-transport]]).

## Related

- introduces [[2000-benamou-dynamic-formulation]] — original CFD / augmented-Lagrangian treatment of the dynamic $W_2$ problem
- extends [[wasserstein-distance]] — realizes $W_2$ as geodesic length in density–velocity space
- applies [[monge-kantorovich-formulations]] — equivalent dynamic path to the static Monge/Kantorovich problems
- background-for [[2018-chizat-unbalanced-ot-formulations]] — unbalanced dynamic OT generalizes the continuity-equation action
- background-for [[wasserstein-fisher-rao-metric]] — WFR is the Benamou–Brenier action plus Fisher–Rao reaction
- background-for [[2019-peyre-computational-optimal-transport]] — monograph treatment of dynamic OT
