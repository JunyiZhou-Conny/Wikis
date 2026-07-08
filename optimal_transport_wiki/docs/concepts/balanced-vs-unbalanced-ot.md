---
title: Balanced vs unbalanced optimal transport
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/math
  - topic/unbalanced-ot
distilled_from:
  - "[[2018-chizat-unbalanced-ot-formulations]]"
  - "[[2018-chizat-scaling-algorithms-unbalanced]]"
  - "[[2019-sejourne-unbalanced-sinkhorn-divergences]]"
  - "[[2019-yang-scalable-unbalanced-ot-gans]]"
---

# Balanced vs unbalanced optimal transport

**Balanced** OT requires the two measures to have equal total mass and matches marginals
*exactly*. **Unbalanced** OT relaxes the marginal constraints — penalizing deviation instead of
enforcing it — so it can transport between measures of **different mass** and allow **mass
creation and destruction**.

## Why it matters / where it shows up

Real data rarely conserves mass: cells divide and die, populations grow, and outliers should be
down-weighted rather than force-matched. Unbalanced OT is the principled fix, and it is more
robust to outliers/noise than balanced OT.

## Details

- **Mechanism:** replace the hard constraints γ1 = μ, γᵀ1 = ν with soft **divergence penalties**
  (KL / Fisher-Rao / TV) on the marginals ([[2018-chizat-unbalanced-ot-formulations]]).
- **Distinguished metric:** Wasserstein-Fisher-Rao / Hellinger-Kantorovich interpolates transport
  and growth ([[2018-chizat-unbalanced-ot-formulations]]).
- **Algorithms:** Sinkhorn-style diagonal scaling against the soft penalties
  ([[2018-chizat-scaling-algorithms-unbalanced]]); debiased **unbalanced Sinkhorn divergences** as
  ML losses ([[2019-sejourne-unbalanced-sinkhorn-divergences]]).
- **Neural / scalable:** learn a transport map **plus a scaling factor** for mass, GAN-style
  ([[2019-yang-scalable-unbalanced-ot-gans]]).
- Balanced OT ([[monge-kantorovich-formulations]]) is the equal-mass special case.

## Related

- introduces [[2018-chizat-unbalanced-ot-formulations]] — dynamic & Kantorovich definitions of unbalanced OT
- extends [[2018-chizat-scaling-algorithms-unbalanced]] — Sinkhorn scaling for the unbalanced problem
- applies [[2019-yang-scalable-unbalanced-ot-gans]] — neural map + scaling factor for mass change
- background-for [[2019-sejourne-unbalanced-sinkhorn-divergences]] — robust debiased losses for the regime
- background-for [[wasserstein-fisher-rao-metric]] — its distinguished metric interpolating transport and growth
- contrasts [[monge-kantorovich-formulations]] — the balanced, exact-marginal baseline
