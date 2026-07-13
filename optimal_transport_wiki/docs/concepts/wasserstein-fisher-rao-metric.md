---
title: Wasserstein-Fisher-Rao metric
type: concept
status: done
date: 2026-07-08
tags:
  - concept
  - domain/math
  - topic/unbalanced-ot
distilled_from:
  - "[[2018-chizat-unbalanced-ot-formulations]]"
  - "[[2018-chizat-scaling-algorithms-unbalanced]]"
  - "[[2000-benamou-dynamic-formulation]]"
---

# Wasserstein-Fisher-Rao metric

The **Wasserstein-Fisher-Rao (WFR)** metric — also called **Hellinger-Kantorovich** — is a
distance on **nonnegative measures of arbitrary mass** that interpolates optimal transport
(moving mass horizontally) with a Fisher-Rao term (creating/destroying mass vertically). It is
the distinguished member of the unbalanced-OT family.

## Why it matters / where it shows up

It gives a genuine metric geometry for problems where mass is *not* conserved — growth models,
single-cell dynamics, and any setting where measures must be compared without forcing equal total
mass. Because it combines transport with a local growth term, it stays finite and geodesic even
when supports or masses differ.

## Details

- **Two equivalent formulations:** a **dynamic** (Benamou-Brenier-type) geodesic problem over the
  space of measures, and a **static Kantorovich** problem over couplings that transport *plus*
  create and destroy mass ([[2018-chizat-unbalanced-ot-formulations]]).
- **Unifies independent constructions:** the same metric was introduced concurrently as
  Wasserstein-Fisher-Rao and as Hellinger-Kantorovich (Chizat et al.; Kondratyev et al.; Liero et
  al.) ([[2018-chizat-unbalanced-ot-formulations]]).
- **Computation:** falls inside the generic unbalanced problem class solved by Sinkhorn-type
  diagonal-scaling iterations ([[2018-chizat-scaling-algorithms-unbalanced]]).

## Related

- introduces [[2018-chizat-unbalanced-ot-formulations]] — defines WFR / Hellinger-Kantorovich as the distinguished member, via equivalent dynamic and static formulations
- applies [[2018-chizat-scaling-algorithms-unbalanced]] — its scaling iterations compute WFR-type unbalanced transport
- applies [[balanced-vs-unbalanced-ot]] — WFR is the canonical metric realizing the unbalanced (mass-changing) regime
- extends [[wasserstein-distance]] — generalizes W₂ with a Fisher-Rao growth term for unequal mass
- extends [[benamou-brenier-formulation]] — adds Fisher–Rao reaction to the Benamou–Brenier continuity-equation action
- extends [[2000-benamou-dynamic-formulation]] — unbalanced dynamic geodesics generalize that balanced kinetic-energy problem
