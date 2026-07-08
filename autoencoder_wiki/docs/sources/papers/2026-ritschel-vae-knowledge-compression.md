---
title: "The Knowledge Hierarchy in Compressed Representations: What Variational Autoencoders Forget First"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: C
venue: "Zenodo (preprint)"
year: 2026
authors: ["Ritschel"]
approx_citations: 0
doi: "10.5281/zenodo.18973865"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/scrna
  - topic/hyperparameters
---

# What VAEs forget first as the latent shrinks

Ritschel, *Zenodo preprint 2026*. **Tier C — unrefereed preprint, 0 citations, unaffiliated
author; flagged per vault contract.** An empirical sweep of what breaks as VAE latent dim drops.

## Summary

Trains VAEs on synthetic data with **five planted generative factors**, sweeping latent dim from
d=50 down to d=1, and probes what survives at each level (reconstruction, covariance recovery,
linear-probe factor recovery, minority-cluster separability, posterior collapse). Frames latent
sizing around the data's **intrinsic dimensionality**.

## Key claims / results

- **Stability plateau**: given 8, 20, or 50 latent dims, the VAE converges to the **same ~5 active
  dimensions** matching the planted factors — over-provisioned models are functionally equivalent.
- Pushing latent dim **below** the intrinsic dimension causes **rapid, simultaneous collapse**
  across all knowledge types; the **rare (5%) subtype degrades first**.
- **ELBO stays flat** across the plateau and gives no warning of impending collapse — a diagnostic
  blind spot.
- Practical recommendation: use latent dim **≥ 2–3× estimated intrinsic dimension**, monitor
  **per-dimension KL** for active-dimension count, and supplement ELBO with factor-recovery R² and
  minority-cluster silhouette.

## Methodology

- Controlled synthetic generative factors of known prevalence/signal; five targeted probes per
  compression level.

## Relevance to your question

- Argues *against* a tight PCA-style ceiling: because rare biology dies first when you compress to
  the intrinsic dimension, it recommends **over-provisioning to 2–3× intrinsic dim** rather than
  capping at the variance-explained count. Directly relevant to scRNA rare-cell-type concerns.
- Weigh accordingly: unrefereed, synthetic-only, single unaffiliated author.

## Related

- extends [[intrinsic-dimension-latent-sizing]] — argues for 2–3× intrinsic dim rather than a tight cap
- benchmarks [[passive-latent-dimensions]] — per-dimension KL + stability plateau as active-dimension evidence
- applies [[choosing-latent-dimension]] — a "when in doubt, over-provision" counterpoint to variance ceilings
- contradicts [[evaluating-vae-scrna-metrics]] — warns ELBO/reconstruction miss rare-subtype loss; adds minority-cluster probes
- background-for [[hyperparameter-sensitivity-vae-scrna]] — per-dimension KL as an active-dimension diagnostic
- applies [[2018-lopez-scvi]] — relevant to scVI's low default latent dim and rare cell types
- [[Sources MOC]]
- [[Autoencoder MOC]]
