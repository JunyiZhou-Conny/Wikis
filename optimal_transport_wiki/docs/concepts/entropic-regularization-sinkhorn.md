---
title: Entropic regularization & the Sinkhorn algorithm
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/ml
  - topic/optimal-transport
  - method/sinkhorn
distilled_from:
  - "[[2013-cuturi-sinkhorn-distances]]"
  - "[[2020-williams-intro-optimal-transport]]"
  - "[[2018-alvarez-melis-gromov-wasserstein-alignment]]"
  - "[[2018-chizat-scaling-algorithms-unbalanced]]"
  - "[[2019-sejourne-unbalanced-sinkhorn-divergences]]"
---

# Entropic regularization & the Sinkhorn algorithm

Adding an entropy penalty −λH(Γ) to the OT problem makes it strictly convex and differentiable,
with a closed-form solution reachable by **iterative diagonal (matrix) scaling** — the Sinkhorn
algorithm.

## Why it matters / where it shows up

This is the computational engine of modern OT: it turns an expensive LP into a handful of
matrix–vector products, is GPU-friendly and differentiable, and generalizes cleanly to
Gromov-Wasserstein and to unbalanced problems. [[2020-williams-intro-optimal-transport]] gives
the ε→0 / ε→∞ intuition before the Sinkhorn algorithm itself.

## Details

- As ε→0, entropic OT recovers exact OT; as ε→∞, the plan → the independent coupling p qᵀ —
  regularization softens sparsity ([[2020-williams-intro-optimal-transport]]).
- Solution form Γ* = diag(u) K diag(v), K = exp(−C/λ); Sinkhorn alternately rescales rows/columns
  ([[2013-cuturi-sinkhorn-distances]]).
- Each **Gromov-Wasserstein** iteration is an inner Sinkhorn solve
  ([[2018-alvarez-melis-gromov-wasserstein-alignment]]).
- Generalizes to **unbalanced** OT by scaling against soft marginal penalties
  ([[2018-chizat-scaling-algorithms-unbalanced]]).
- Entropic OT is **biased** (nonzero for equal inputs); **Sinkhorn divergences** debias it
  ([[2019-sejourne-unbalanced-sinkhorn-divergences]]).

## Related

- introduces [[2013-cuturi-sinkhorn-distances]] — the entropic-OT / Sinkhorn method
- background-for [[2020-williams-intro-optimal-transport]] — ε-limits and near-linear-time motivation
- applies [[2018-alvarez-melis-gromov-wasserstein-alignment]] — Sinkhorn as the inner GW solver
- extends [[2018-chizat-scaling-algorithms-unbalanced]] — unbalanced generalization of the scaling iterations
- contrasts [[2019-sejourne-unbalanced-sinkhorn-divergences]] — debiases the entropic estimate
