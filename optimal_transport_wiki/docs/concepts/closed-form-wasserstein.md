---
title: Closed-form Wasserstein (1D & Gaussians)
type: concept
status: done
date: 2026-07-10
tags:
  - concept
  - domain/math
  - topic/wasserstein
distilled_from:
  - "[[2020-williams-intro-optimal-transport]]"
  - "[[2019-peyre-computational-optimal-transport]]"
---

# Closed-form Wasserstein (1D & Gaussians)

Two analytically tractable cases of the Wasserstein distance: **univariate** measures via
inverse CDFs (quantile functions), and **Gaussians** via means plus the **Bures** metric on
covariances.

## Why it matters / where it shows up

Most OT problems need numerical solvers (LP / Sinkhorn / neural duals). These closed forms are
the exceptions used for sanity checks, 1D baselines, and Gaussian-mixture / Bures geometry in
ML — and they make W₂ concrete before the discrete LP picture.

## Details

- **1D / univariate.** For order-p Wasserstein,
  W_p(P,Q) = (∫₀¹ |F⁻¹(y) − G⁻¹(y)|^p dy)^{1/p}, where F⁻¹, G⁻¹ are inverse CDFs
  ([[2020-williams-intro-optimal-transport]], citing Peyré & Cuturi Remarks 2.30–2.31).
- **Gaussians.** For N(μ₁, Σ₁) and N(μ₂, Σ₂),
  W₂² = ‖μ₁ − μ₂‖₂² + B(Σ₁, Σ₂)² with B the Bures metric on positive-definite matrices.
  Univariate special case: W₂ = √((μ₁−μ₂)² + (σ₁−σ₂)²) — Euclidean distance in the (μ, σ) plane
  ([[2020-williams-intro-optimal-transport]]).
- Full statements and references: [[2019-peyre-computational-optimal-transport]].
- Outside these cases, continuous OT is hard; practice discretizes to an LP / entropic problem
  ([[wasserstein-distance]], [[entropic-regularization-sinkhorn]]).

## Related

- introduces [[2020-williams-intro-optimal-transport]] — states both closed forms as the notable analytic cases
- introduces [[2019-peyre-computational-optimal-transport]] — Remarks 2.30–2.31 are the reference statements
- extends [[wasserstein-distance]] — special cases of the general W_p definition
- contrasts [[entropic-regularization-sinkhorn]] — numerical path when no closed form exists
