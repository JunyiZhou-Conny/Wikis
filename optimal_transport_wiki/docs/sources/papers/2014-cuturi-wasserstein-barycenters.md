---
title: "Fast Computation of Wasserstein Barycenters"
type: source
status: done
date: 2026-07-10
source_kind: paper
tier: A
venue: "ICML 2014"
year: 2014
authors: ["Cuturi", "Doucet"]
approx_citations: 700
doi: "10.48550/arXiv.1310.4375"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/wasserstein
  - topic/barycenters
  - method/sinkhorn
  - method/entropic-ot
---

# Fast Computation of Wasserstein Barycenters

Cuturi & Doucet, *ICML 2014*. The computational paper that made **Wasserstein barycenters**
practical for ML — entropic smoothing of the multi-measure Fréchet mean, building directly on
Sinkhorn distances.

## Summary

A Wasserstein barycenter of measures $\{\nu_i\}$ is a Fréchet mean under $W_p$: the measure $\mu$
minimizing $\frac{1}{N}\sum_i W_p^p(\mu,\nu_i)$ (Agueh & Carlier). Exact barycenters need repeated
primal/dual OT solves and are prohibitive at ML scale. This paper gives two subgradient schemes
(fixed support vs free support in $\mathbb{R}^d$) and makes them fast by replacing each OT solve
with **entropically regularized** primal/dual problems whose optima come from Sinkhorn matrix
scaling — the same engine as [[2013-cuturi-sinkhorn-distances]], now used as a differentiable
building block inside a variational problem over many measures.

## Key claims / results

- **Fixed support** (Alg. 1): weights $a$ on a known grid $X$ are optimized by projected /
  accelerated subgradient descent; the subgradient is the average of dual OT potentials
  $\alpha_i^\star$ for each target $\nu_i$.
- **Free support** (Alg. 2): alternate weight updates with Newton-style location updates
  $X\leftarrow(\tfrac{1}{N}\sum_i Y_i T_i^{\star T})\operatorname{diag}(a^{-1})$ from primal plans;
  recovers Lloyd $k$-means when $N=1$, $p=2$, unconstrained weights, and Ng-style uniform
  $k$-means when $\Theta=\{\mathbf{1}_k/k\}$.
- Entropic smoothing yields strictly convex $\mathbf{p}_\lambda$ / $\mathbf{d}_\lambda$; Sinkhorn
  scaling of $K=e^{-\lambda M}$ recovers both smoothed primal plan $T_\lambda^\star$ and dual
  $\alpha_\lambda^\star$ cheaply (Alg. 3), so Algorithms 1–2 become practical.
- Empirically: MNIST digit barycenters on a $50\times 50$ grid (~5k images/digit) and
  **uniform-weight** spatial clustering of US income/population (balanced Voronoi cells vs free
  $k$-means).

## Methodology

- Objective $f(a,X)=\frac{1}{N}\sum_i\mathbf{p}(a,b_i,M_{XY_i})$ over discrete measures.
- Dual LP sensitivity → subgradient in $a$; for $p=2$ Euclidean free support, local quadratic
  approximation of the transport cost → barycentric Newton step in $X$.
- Replace exact $\mathbf{p}/\mathbf{d}$ by entropic $\mathbf{p}_\lambda/\mathbf{d}_\lambda$; solve via
  Sinkhorn–Knopp on $K=\exp(-\lambda M)$.

## Related

- introduces [[wasserstein-barycenters]] — scalable Fréchet means under $W_p$ via entropic OT
- extends [[2013-cuturi-sinkhorn-distances]] — lifts Sinkhorn from pairwise distances to multi-measure barycenters
- applies [[entropic-regularization-sinkhorn]] — matrix scaling supplies the smoothed primal/dual gradients
- applies [[wasserstein-distance]] — barycenter is the Fréchet mean for $W_p^p$
- applies [[monge-kantorovich-formulations]] — uses Kantorovich primal/dual repeatedly inside the variational problem
- background-for [[2019-peyre-computational-optimal-transport]] — monograph later surveys barycenters built on this line
- [[Sources MOC]]
- [[Optimal Transport MOC]]
