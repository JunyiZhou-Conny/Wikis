---
title: "The Monge Gap: A Regularizer to Learn All Transport Maps"
type: source
status: done
date: 2026-07-23
source_kind: paper
tier: A
venue: "ICML 2023"
year: 2023
authors: ["Uscidda", "Cuturi"]
approx_citations: 90
doi: "10.48550/arXiv.2302.04953"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/neural-ot
  - topic/wasserstein
  - method/neural-ot
---

# The Monge Gap: A Regularizer to Learn All Transport Maps

Uscidda & Cuturi, *ICML 2023* (Apple / CREST–ENSAE). A frontier **neural Monge-map**
method that replaces ICNN architecture constraints with a cost-agnostic **Monge gap**
regularizer — the architecture-free counterpart to CellOT-style dual ICNNs.

## Summary

Brenier’s theorem motivates learning OT maps as gradients of convex potentials via input-convex
nets (Makkuva et al.; Korotin et al.), but ICNNs are hard to train, tied to squared-Euclidean
cost, and theoretically motivated for densities — not finite samples. This paper drops
architecture constraints on \(T\) and instead regularizes any map by the **Monge gap**
\(\mathcal{M}^c_\rho(T)=\int c(x,T(x))\,d\rho(x)-W_c(\rho,T\sharp\rho)\): the optimality gap of \(T\) as a
\(c\)-Monge map between a reference \(\rho\) and its pushforward. Fitting \(T\sharp\mu\approx\nu\) (e.g. with a
Sinkhorn divergence) plus \(\lambda_{\mathrm{MG}}\mathcal{M}^c_\rho(T)\) recovers \(c\)-OT maps when
\(\mathrm{Spt}(\mu)\subset\mathrm{Spt}(\rho)\). Empirically the method beats ICNNs and vanilla MLPs on the
Korotin continuous \(\mathbb{W}_2\) benchmark and on single-cell perturbation prediction.

## Key claims / results

- \(\mathcal{M}^c_\rho(T)\ge 0\), with equality iff \(T\) is a \(c\)-OT map between \(\rho\) and \(T\sharp\rho\); if also
  \(T\sharp\mu=\nu\) and \(\mathrm{Spt}(\mu)\subset\mathrm{Spt}(\rho)\), then \(T\) is \(c\)-OT between \(\mu\) and \(\nu\).
- For quadratic cost, \(\mathcal{M}^2_\rho\) (and its entropic plug-in) is convex, subadditive, and
  positively homogeneous in \(T\); the discrete estimator is a cyclical-monotonicity violation.
- Naive displacement-cost dualization of the pushforward constraint is intrinsically biased;
  the Monge gap is a **debiased** optimality regularizer homogeneous with fitting losses.
- For translation-invariant costs \(c(x,y)=h(x-y)\), optionally parameterize
  \(T_\theta=x-\nabla h^*\circ F_\theta(x)\) and soft-penalize non-conservativity of \(F_\theta\) via Jacobian
  asymmetry (not a hard ICNN constraint).
- On Korotin et al. (2021) Gaussian-mixture Monge benchmarks (\(d\) up to 256), Monge-gap MLPs
  dominate ICNNs / Fan saddle-point MLPs for \(d\ge 16\); on 4i and scRNA cancer-perturbation
  tasks, they outperform ICNN (CellOT-style), vanilla MLP, and entropic-map baselines under
  Sinkhorn-divergence predictive metrics. Ablations show gains come mainly from
  \(\lambda_{\mathrm{MG}}\), not the conservativity penalty, on real single-cell data.

## Methodology

- Define \(\mathcal{M}^c_\rho\) from the Monge problem; estimate with samples via entropic OT
  \(W_{c,\varepsilon}\) (Sinkhorn) for differentiability.
- Train unconstrained \(T_\theta\) (MLP) by minimizing
  \(\Delta(T_\theta\sharp\mu,\nu)+\lambda_{\mathrm{MG}}\mathcal{M}^c_\rho(T_\theta)\), typically
  \(\Delta=W_{\ell_2^2,\varepsilon}\) or the Sinkhorn divergence \(S_{\ell_2^2,\varepsilon}\).
- Structured-cost variant: \(T_\theta=\mathrm{Id}-\nabla h^*\circ F_\theta\) plus optional Hutchinson-trace
  conservativity regularizer \(\mathcal{C}_\rho(F)\).
- Reference \(\rho\) often set to \(\mu\); \(\lambda_{\mathrm{MG}}\) is easy to tune (\(\sim 1\)–\(10\)) because the gap
  shares the scale of averaged costs.

## Related

- introduces [[neural-optimal-transport]] — Monge-gap regularization as an architecture-free neural Monge solver
- applies [[monge-kantorovich-formulations]] — Monge optimality gap + Kantorovich/entropic \(W_c\) estimators
- background-for [[wasserstein-distance]] — \(W_c\) / Sinkhorn divergence as fitting loss and gap building block
- extends [[entropic-regularization-sinkhorn]] — uses Sinkhorn / Sinkhorn divergence inside the Monge-gap estimator and fitting loss
- contradicts [[2023-bunne-cellot-neural-ot]] — drops ICNN / Brenier architectural constraints that CellOT relies on; same single-cell perturbation setting
- benchmarks [[2023-korotin-neural-optimal-transport]] — sibling neural OT line; Monge gap targets deterministic \(c\)-maps vs Korotin’s maximin strong/weak plans
- extends [[2013-cuturi-sinkhorn-distances]] — entropic OT as the differentiable engine inside \(\mathcal{M}^c_{\hat\rho,\varepsilon}\)
- [[Sources MOC]]
- [[Optimal Transport MOC]]
