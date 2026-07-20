---
title: Sinkhorn divergence
type: concept
status: done
date: 2026-07-20
tags:
  - concept
  - domain/ml
  - topic/optimal-transport
  - topic/wasserstein
  - method/sinkhorn
  - method/entropic-ot
distilled_from:
  - "[[2018-genevay-sinkhorn-divergences]]"
  - "[[2019-sejourne-unbalanced-sinkhorn-divergences]]"
  - "[[2013-cuturi-sinkhorn-distances]]"
---

# Sinkhorn divergence

A **debiased entropic optimal-transport loss**: subtract the self-transport terms so the loss
vanishes when the two measures agree —
\(S_\varepsilon(\alpha,\beta)=\mathrm{OT}_\varepsilon(\alpha,\beta)-\tfrac12\mathrm{OT}_\varepsilon(\alpha,\alpha)-\tfrac12\mathrm{OT}_\varepsilon(\beta,\beta)\)
(equivalently Genevay et al.'s \(\overline{W}_{c,\varepsilon}\)).

## Why it matters / where it shows up

Plain Sinkhorn / entropic OT is a biased discrepancy (nonzero at \(\alpha=\beta\)) and blurs
couplings. Debiasing makes a usable ML loss that still runs on Sinkhorn iterations, interpolates
toward MMD as \(\varepsilon\to\infty\), and extends to unbalanced mass transport.

## Details

- Introduced for generative modeling as the **Sinkhorn loss**, with autodiff through Sinkhorn
  scalings ([[2018-genevay-sinkhorn-divergences]]).
- Built on entropic OT / Sinkhorn distances ([[2013-cuturi-sinkhorn-distances]]).
- Extended to **unbalanced** marginals via divergence-penalized formulations
  ([[2019-sejourne-unbalanced-sinkhorn-divergences]]).

## Related

- introduces [[2018-genevay-sinkhorn-divergences]] — balanced Sinkhorn loss + OT–MMD interpolation
- extends [[2019-sejourne-unbalanced-sinkhorn-divergences]] — unbalanced Sinkhorn divergences
- applies [[2013-cuturi-sinkhorn-distances]] — debiasing sits on top of entropic OT / Sinkhorn
