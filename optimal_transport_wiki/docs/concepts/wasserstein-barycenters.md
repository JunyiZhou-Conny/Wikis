---
title: Wasserstein barycenters
type: concept
status: done
date: 2026-07-10
tags:
  - concept
  - domain/ml
  - domain/math
  - topic/wasserstein
  - topic/barycenters
distilled_from:
  - "[[2014-cuturi-wasserstein-barycenters]]"
  - "[[2019-peyre-computational-optimal-transport]]"
---

# Wasserstein barycenters

The **Fréchet mean** of probability measures under the Wasserstein metric: a barycenter $\mu$
minimizes $\sum_i \lambda_i W_p^p(\mu,\nu_i)$ — an average that moves mass geometrically rather
than averaging densities pointwise.

## Why it matters / where it shows up

Euclidean / RKHS / KL-style centroids blur or invent mass where supports do not overlap.
Wasserstein barycenters interpolate shapes, histograms, and point clouds in a geometry-aware way,
so they show up in image averaging, texture mixing, clustering with transport costs, and as a
building block in computational OT toolkits.

## Details

- Theory root: Agueh & Carlier (2011) uniqueness / multi-marginal characterization; special cases
  include 1-D, two-measure McCann interpolants, and Gaussians.
- Computational breakthrough: entropic Sinkhorn gradients for fixed- and free-support discrete
  barycenters ([[2014-cuturi-wasserstein-barycenters]]).
- Surveyed as a core computational-OT primitive alongside Sinkhorn and GW
  ([[2019-peyre-computational-optimal-transport]]).
- Special case $N=1$, free support, $p=2$ recovers $k$-means; uniform weight constraints give
  balanced transport clustering.

## Related

- introduces [[2014-cuturi-wasserstein-barycenters]] — first practical entropic algorithms for discrete barycenters
- background-for [[2019-peyre-computational-optimal-transport]] — monograph treatment of barycenters in the OT toolbox
- extends [[wasserstein-distance]] — the distance whose Fréchet mean defines the barycenter
- applies [[entropic-regularization-sinkhorn]] — Sinkhorn supplies the scalable inner solves
