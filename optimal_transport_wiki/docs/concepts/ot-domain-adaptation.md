---
title: OT for domain adaptation
type: concept
status: done
date: 2026-07-11
tags:
  - concept
  - domain/ml
  - topic/domain-adaptation
  - topic/wasserstein
  - method/sinkhorn
distilled_from:
  - "[[2017-courty-optimal-transport-domain-adaptation]]"
  - "[[2013-cuturi-sinkhorn-distances]]"
  - "[[2019-peyre-computational-optimal-transport]]"
---

# OT for domain adaptation

Use a **transport plan** to move labeled source samples onto the target feature distribution,
then learn the classifier in the adapted geometry — domain shift as an optimal-transport problem.

## Why it matters / where it shows up

Many DA methods match means, covariances, or subspaces globally. OTDA instead learns a
**sample-wise** coupling that respects geometry even when supports barely overlap, and can encode
class structure in the plan. It is the root of a large applied-OT thread (visual DA, remote
sensing, speech) and a standard example in computational-OT surveys.

## Details

- Pipeline: estimate discrete measures → solve (regularized) Kantorovich OT → barycentric map of
  source onto target → train on transported labeled points
  ([[2017-courty-optimal-transport-domain-adaptation]]).
- Scalability comes from **entropic Sinkhorn** ([[2013-cuturi-sinkhorn-distances]]); class
  group-lasso / Laplacian terms keep same-label mass coherent.
- Requires a shared ambient feature space and ground cost; when domains are only relationally
  comparable, prefer Gromov–Wasserstein-style alignment instead.
- Covered as an ML application of computational OT in
  [[2019-peyre-computational-optimal-transport]].

## Related

- introduces [[2017-courty-optimal-transport-domain-adaptation]] — canonical OTDA formulation and class-regularized plans
- applies [[2013-cuturi-sinkhorn-distances]] — entropic OT supplies the fast coupling
- background-for [[2019-peyre-computational-optimal-transport]] — survey placement of OTDA in the OT toolbox
- extends [[wasserstein-distance]] — DA objective is alignment under Wasserstein geometry
- applies [[monge-kantorovich-formulations]] — Kantorovich plan + barycentric Monge-like map
- contrasts [[gromov-wasserstein-distance]] — GW drops the shared-feature-cost assumption
