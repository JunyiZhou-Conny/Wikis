---
title: "FONDUE: an algorithm to find the optimal dimensionality of the latent representations of variational autoencoders"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: C
venue: "arXiv (preprint)"
year: 2022
authors: ["Bonheme", "Grześ"]
approx_citations: 2
doi: "10.48550/arXiv.2209.12806"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/hyperparameters
  - method/vae
---

# FONDUE: finding the optimal number of VAE latent dimensions

Bonheme & Grześ (Univ. of Kent), *arXiv 2022*. **Tier C — preprint (a later version was rejected
by TMLR); flagged per vault contract.** Selects VAE latent dim **without full grid search**.

## Summary

FONDUE (Finding the Optimal Number of Dimensions by Unsupervised Estimation) uses **intrinsic
dimension estimation (IDE)** of a VAE's latent representations. It observes that the IDEs of the
**mean** vs **sampled** latent representations **diverge once passive (unused) variables appear** —
a sign the latent space is over-provisioned. This divergence is visible after only a few training
steps, so the right dimensionality can be found cheaply and unsupervised.

## Key claims / results

- **Passive variables** (dimensions ignored by the decoder) emerge when latent size exceeds the
  data's intrinsic dimension.
- The gap between IDE(mean) and IDE(sampled) pinpoints where passive variables start — pick the
  largest size with **no** passive variables.
- Works **without human supervision or training multiple full models**, unlike grid search.
- Findings: deeper encoder layers have lower IDE; extrinsic latent dim > its IDE; layer IDs
  stabilize very early in training.

## Methodology

- Estimate IDE of mean and sampled latent reps during early training across candidate sizes.
- Threshold on their divergence to choose the number of latent dimensions.

## Relevance to your question

- An alternative to your PCA-ceiling idea: instead of PCA variance, use **intrinsic-dimension
  divergence** as the principled cap. Same spirit ("don't over-provision the latent"), different,
  VAE-native diagnostic that avoids PCA's linearity assumption.

## Related

- introduces [[intrinsic-dimension-latent-sizing]] — passive-variable / IDE divergence as the sizing signal
- introduces [[passive-latent-dimensions]] — mean-vs-sampled IDE divergence detects passive axes
- applies [[choosing-latent-dimension]] — an unsupervised, search-free way to set VAE latent dim
- extends [[2013-kingma-vae]] — diagnoses the standard VAE's latent for superfluous dimensions
- benchmarks [[2025-saha-ard-vae]] — same problem (find relevant latent dims), different mechanism (IDE vs ARD prior)
- [[Sources MOC]]
- [[Autoencoder MOC]]
