---
title: Sliced Wasserstein distance
type: concept
status: done
date: 2026-07-22
tags:
  - concept
  - domain/math
  - domain/ml
  - topic/wasserstein
  - topic/sliced-wasserstein
  - method/sliced-ot
distilled_from:
  - "[[2015-bonneel-sliced-radon-wasserstein-barycenters]]"
  - "[[2019-peyre-computational-optimal-transport]]"
---

# Sliced Wasserstein distance

A projection-based surrogate for the Wasserstein distance: average (or integrate) the **1-D
Wasserstein cost** of measures after pushing them onto random lines \(\theta \in S^{d-1}\).

\[
\mathrm{SW}_2^2(\mu,\nu) = \int_{S^{d-1}} W_2^2(P_{\theta\#}\mu,\, P_{\theta\#}\nu)\,d\theta.
\]

## Why it matters / where it shows up

High-d OT is costly; 1-D OT is essentially sorting. Slicing turns that fact into a scalable
geometry for barycenters, generative modeling, and imaging — trading some metric fidelity for
closed-form 1-D maps and easy gradients on point clouds.

## Details

- Each \(P_{\theta\#}\mu\) is the law of \(\langle X,\theta\rangle\); 1-D \(W_2\) is computed from
  inverse CDFs / sorted samples ([[2015-bonneel-sliced-radon-wasserstein-barycenters]]).
- Two barycenter constructions build on SW: **Radon** (back-project 1-D barycenters) and
  **sliced** (optimize \(\sum_i \lambda_i \mathrm{SW}^2(\mu_i,\mu)\) over the unknown measure).
- Orthogonal to entropic Sinkhorn: no Gibbs kernel, but Monte Carlo over directions; surveyed
  among computational OT tools in [[2019-peyre-computational-optimal-transport]].

## Related

- introduces [[2015-bonneel-sliced-radon-wasserstein-barycenters]] — formal SW distance + Radon/sliced barycenters
- background-for [[2019-peyre-computational-optimal-transport]] — monograph treatment of projection OT
- extends [[wasserstein-distance]] — SW is an integrated family of 1-D Wasserstein distances
- applies [[monge-kantorovich-formulations]] — each slice is a 1-D Monge/Kantorovich problem
