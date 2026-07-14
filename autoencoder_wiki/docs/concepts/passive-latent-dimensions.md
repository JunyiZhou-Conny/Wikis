---
title: Passive latent dimensions & posterior collapse
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/ml
  - topic/vae
  - topic/hyperparameters
distilled_from:
  - "[[2025-saha-ard-vae]]"
  - "[[2022-bonheme-fondue]]"
  - "[[2026-ritschel-vae-knowledge-compression]]"
  - "[[2017-higgins-beta-vae]]"
---

# Passive latent dimensions & posterior collapse

When a VAE is given more latent axes than the data needs, the surplus axes go **passive** — the
encoder posterior falls back to the prior and the decoder ignores them. This is a *model-side*
signal you can exploit to choose (or trust) the latent dimension.

## Why it matters / where it shows up

Passive dimensions are why **over-provisioning a VAE is relatively safe** but wasteful, and why raw
per-axis variance is a poor importance ranking: a collapsed axis still carries small non-zero
variance. It is the mechanism several latent-sizing methods detect, and it distinguishes this
idea from the data's [[intrinsic-dimension-latent-sizing|intrinsic dimension]] (which is about the
data, not the model).

## Details

- **Detecting it:**
  - ARD prior drives unused axes to near-zero variance (large precision α); a relevance score then
    separates active from passive ([[2025-saha-ard-vae]]).
  - The intrinsic-dimension estimates of a VAE's **mean vs sampled** latents diverge exactly when
    passive variables appear — visible after only a few training steps ([[2022-bonheme-fondue]]).
  - Track **per-dimension KL** to count active dimensions; ELBO alone stays flat and hides it
    ([[2026-ritschel-vae-knowledge-compression]]).
- **Stability plateau:** given 8/20/50 dims, a VAE can converge to the *same* handful of active
  dims — over-provisioned models are near-equivalent ([[2026-ritschel-vae-knowledge-compression]]).
- **Caveat for scRNA:** don't equate "low variance / near-passive" with "useless" — such axes can
  still encode rare cell types, so pruning by variance alone is risky.

## Related

- introduces [[2022-bonheme-fondue]] — passive variables detected via mean-vs-sampled IDE divergence
- applies [[2025-saha-ard-vae]] — ARD prior actively collapses passive axes and scores relevance
- benchmarks [[2026-ritschel-vae-knowledge-compression]] — per-dimension KL + stability plateau evidence
- background-for [[choosing-latent-dimension]] — passive-dimension signals as a way to pick/verify latent size
- applies [[2017-higgins-beta-vae]] — high-β capacity limits leave uninformative units near the prior (low KL)
- applies [[beta-vae-weighted-kl-disentanglement]] — unused-axis collapse as a side effect of the β bottleneck
- contrasts [[intrinsic-dimension-latent-sizing]] — model-side collapse vs data-side degrees of freedom
- contrasts [[monosemantic-features-vs-polysemantic-neurons]] — collapsed unused VAE axes vs mixed-but-active polysemantic neurons
