---
title: Wasserstein loss (supervised)
type: concept
status: done
date: 2026-07-18
tags:
  - concept
  - domain/ml
  - topic/wasserstein
  - topic/supervised-ot
  - method/sinkhorn
distilled_from:
  - "[[2015-frogner-wasserstein-loss]]"
  - "[[2013-cuturi-sinkhorn-distances]]"
  - "[[2019-sejourne-unbalanced-sinkhorn-divergences]]"
---

# Wasserstein loss (supervised)

Using the **Wasserstein / entropic OT cost** between a model's predicted measure and a target
label measure as the training objective — so the ground metric on the output space shapes the
gradient.

## Why it matters / where it shows up

Standard cross-entropy and KL ignore semantic structure among labels. A Wasserstein loss
penalizes "nearby" mistakes less than distant ones, which matters for multi-label tagging,
hierarchies, and any setting where partial credit should follow a metric. It is the supervised
counterpart to using \(W\) as a generative / adversarial objective.

## Details

- Canonical formulation: ERM with \(W_p^p(h(x), y)\) on the label simplex, optimized via
  Cuturi–Sinkhorn gradients ([[2015-frogner-wasserstein-loss]], building on
  [[2013-cuturi-sinkhorn-distances]]).
- Soft-marginal / unnormalized variants replace hard coupling constraints with KL penalties —
  an early bridge to unbalanced OT losses ([[2015-frogner-wasserstein-loss]]; later debiased
  unbalanced Sinkhorn divergences in [[2019-sejourne-unbalanced-sinkhorn-divergences]]).
- Distinct from **cost-only adversarial** uses of \(W_1\) (e.g. WGAN): here both prediction and
  target are explicit measures, and the plan (or its dual) is computed each step.

## Related

- introduces [[2015-frogner-wasserstein-loss]] — first supervised multi-label Wasserstein ERM loss
- applies [[2013-cuturi-sinkhorn-distances]] — entropic OT / Sinkhorn makes the loss trainable
- extends [[2019-sejourne-unbalanced-sinkhorn-divergences]] — debiased unbalanced Sinkhorn losses continue the soft-marginal ML-loss thread
- applies [[wasserstein-distance]] — the scalar being minimized is an OT distance on label space
- applies [[entropic-regularization-sinkhorn]] — the computational engine for the surrogate
