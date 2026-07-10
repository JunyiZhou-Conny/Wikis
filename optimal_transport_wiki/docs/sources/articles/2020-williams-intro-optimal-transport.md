---
title: "A Short Introduction to Optimal Transport and Wasserstein Distance"
type: source
status: done
date: 2026-07-10
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
flagged per vault contract.** Explicitly kept as the wiki's **primary learning onramp** to OT:
intuition-first, code-backed, and repeatedly points to [[2019-peyre-computational-optimal-transport]]
for rigor.

## Summary

An intuition-over-rigor introduction motivating optimal transport as a **distance between
probability distributions** that fixes two failures of KL divergence: KL is asymmetric and blows
up to +∞ when supports don't overlap. OT's **Wasserstein distance** (a.k.a. Earth Mover's
Distance) is symmetric, satisfies the triangle inequality, and stays finite/intuitive even for
disjoint supports. The post builds the "piles of dirt into holes" picture, discretizes it to a
linear program, solves it with `scipy.optimize.linprog`, works 1D and 2D examples, and closes on
**entropic regularization** — the computational enabler for OT in ML.

## Key claims / results

- **Why OT (vs KL):** desirable distances are symmetric + obey the triangle inequality; KL is
  neither robust (∞ on unequal support) nor symmetric. Smoothing supports before KL is a brittle
  workaround; Wasserstein stays finite and ranks the same toy pairs intuitively.
- **Earth-mover picture:** piles = density of P, holes = density of Q (equal total mass); cost is
  squared Euclidean; a plan T moves nonnegative mass, allowing **splitting** (Kantorovich, not
  Monge). Marginal constraints: outgoing mass matches p, incoming mass matches q.
- **Coupling view:** a feasible plan is a probability on X×X with the given marginals; the
  **product measure** T = p⊗q is always feasible.
- **Discrete OT = linear program:** minimize ⟨T, C⟩ s.t. T1 = p, Tᵀ1 = q, T ≥ 0;
  W₂(P,Q) = ⟨T*, C⟩^{1/2} with C_ij = ‖x_i − x_j‖². Symmetry and W=0 iff P=Q shown directly;
  triangle inequality deferred.
- **Optimal plans are sparse**, tracing a monotone curved path; peaks in T* track peaks in the
  marginals (because of the row/column sum constraints).
- **Order-p Wasserstein:** with C_ij = ‖x_i − x_j‖^p, W_p = ⟨T*, C⟩^{1/p}. Order p=1 is noted as
  more robust to outliers (→ Peyré & Cuturi ch. 6).
- **Closed forms** (via Peyré & Cuturi Remarks 2.30–2.31): (i) **1D** — W_p via inverse CDFs,
  (∫₀¹ |F⁻¹ − G⁻¹|^p dy)^{1/p}; (ii) **Gaussians** — W₂ via means + **Bures** metric on
  covariances (univariate: Euclidean distance in (μ, σ) plane).
- **Entropic regularization:** add −ε H(T); as ε→0 recovers exact OT; as ε→∞ the plan → p qᵀ
  (outer product / independent coupling). Softens sparsity and moves the solution off the sharp
  edges of the coupling polytope. Turns the O(d³ log d) LP (Orlin) into near-linear-time solves
  (Altschuler et al., Dvurechensky et al.) — the key ML enabler. Points to Peyré & Cuturi ch. 4.
- **Unbalanced OT** flagged for unequal-mass extensions (Peyré & Cuturi §10.2); entropy
  definition discrepancies matter there.
- Applications cited as motivation: imaging, generative models (WGAN), biological data analysis.

## Methodology

- Expository: physical intuition → continuous Kantorovich formulation → grid discretization →
  LP → worked 1D and 2D examples with `scipy.optimize.linprog` demo code → entropic-regularization
  coda with Peyré & Cuturi Fig. 4.2 reproduced. Prioritizes intuition; defers measure theory.

## Related

- introduces [[wasserstein-distance]] — Earth Mover's Distance, metric properties, and why it beats KL on unequal support
- applies [[monge-kantorovich-formulations]] — motivates the Kantorovich (mass-splitting) relaxation over Monge
- background-for [[entropic-regularization-sinkhorn]] — closes on the entropic penalty, ε-limits, and near-linear-time payoff
- introduces [[closed-form-wasserstein]] — 1D inverse-CDF and Gaussian/Bures analytic cases
- background-for [[balanced-vs-unbalanced-ot]] — flags unbalanced OT as the unequal-mass extension
- extends [[2013-cuturi-sinkhorn-distances]] — pedagogical companion to the entropic-OT method
- background-for [[2019-peyre-computational-optimal-transport]] — repeatedly points readers to that monograph for depth
- [[Sources MOC]]
- [[Optimal Transport MOC]]
