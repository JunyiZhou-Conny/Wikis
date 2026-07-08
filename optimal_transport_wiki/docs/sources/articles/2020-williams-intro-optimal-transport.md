---
title: "A Short Introduction to Optimal Transport and Wasserstein Distance"
type: source
status: done
date: 2026-07-07
source_kind: article
tier: C
venue: "Its Neuronal (personal research blog)"
year: 2020
authors: ["Williams"]
approx_citations: 0
doi: ""
url: "https://alexhwilliams.info/itsneuronalblog/2020/10/09/optimal-transport/"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/math
  - topic/optimal-transport
  - topic/wasserstein
  - method/sinkhorn
---

# A Short Introduction to Optimal Transport and Wasserstein Distance

Alex H. Williams, *Its Neuronal* blog, 2020. **Tier C — expository blog post (not peer-reviewed);
flagged per vault contract.** A credible, intuition-first tutorial by a computational
neuroscientist; excellent onramp to the wiki's OT foundations.

## Summary

An intuition-over-rigor introduction motivating optimal transport as a **distance between
probability distributions** that fixes two failures of KL divergence: KL is asymmetric and blows
up to +∞ when supports don't overlap. OT's **Wasserstein distance** (a.k.a. Earth Mover's
Distance) is symmetric, satisfies the triangle inequality, and stays finite/intuitive even for
disjoint supports. The post builds the "piles of dirt into holes" picture, discretizes it to a
linear program, solves it with `scipy.optimize.linprog`, and closes on **entropic
regularization**.

## Key claims / results

- **Why OT:** desirable distances are symmetric + obey the triangle inequality; KL is neither
  robust (∞ on unequal support) nor symmetric — Wasserstein is both.
- **Kantorovich picture:** a transport plan is a coupling whose marginals must equal P and Q; the
  post uses the mass-splitting **Kantorovich** relaxation (not Monge) for tractability (footnote).
- **Discrete OT = linear program:** minimize ⟨T, C⟩ s.t. T1 = p, Tᵀ1 = q, T ≥ 0; W(P,Q) = ⟨T*, C⟩^{1/2}
  with squared-Euclidean cost (order-2). Symmetry and W=0 iff P=Q shown directly.
- **Optimal plans are sparse**, tracing a monotone path; peaks track the marginals.
- **Entropic regularization:** add −εH(T); as ε→0 recovers exact OT, as ε→∞ the plan → p qᵀ
  (outer product). Turns the O(d³ log d) LP into near-linear-time solves — the key ML enabler.
- Notes analytic cases (1D via inverse CDFs; Gaussians via the Bures metric) and points to
  **unbalanced OT** (Peyré & Cuturi §10.2) for unequal-mass extensions.

## Methodology

- Expository: physical intuition → continuous formulation → grid discretization → LP →
  worked 1D and 2D examples with code; entropic-regularization coda.

## Related

- introduces [[wasserstein-distance]] — the Earth Mover's Distance and its metric properties, from scratch
- applies [[monge-kantorovich-formulations]] — motivates using the Kantorovich (mass-splitting) relaxation
- background-for [[entropic-regularization-sinkhorn]] — closes on the entropic penalty and its near-linear-time payoff
- extends [[2013-cuturi-sinkhorn-distances]] — pedagogical companion to the entropic-OT method
- background-for [[2019-peyre-computational-optimal-transport]] — repeatedly points readers to that monograph for depth
- background-for [[balanced-vs-unbalanced-ot]] — flags unbalanced OT as the unequal-mass extension
- [[Sources MOC]]
- [[Optimal Transport MOC]]
