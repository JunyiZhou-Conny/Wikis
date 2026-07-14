---
title: "β-VAE: Learning Basic Visual Concepts with a Constrained Variational Framework"
type: source
status: done
date: 2026-07-14
source_kind: paper
tier: A
venue: "ICLR"
year: 2017
authors: ["Higgins", "Matthey", "Pal", "Burgess", "Glorot", "Botvinick", "Mohamed", "Lerchner"]
approx_citations: 3100
doi: ""
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/autoencoder
  - method/vae
  - method/beta-vae
---

# β-VAE: Learning Basic Visual Concepts with a Constrained Variational Framework

Higgins, Matthey, Pal, Burgess, Glorot, Botvinick, Mohamed & Lerchner (DeepMind), *ICLR*
2017. The **canonical β-VAE** paper — weights the VAE KL term with β > 1 to push unsupervised
latents toward **disentangled** generative factors.

## Summary

Unsupervised models rarely recover clean, factorized latents of the independent causes of the
data. Starting from the Kingma & Welling VAE, the authors cast inference as a constrained
optimization that caps the capacity of the latent channel against an isotropic Gaussian prior,
then introduce a Lagrange multiplier **β** on the KL. With β = 1 the objective is the usual ELBO;
with β > 1 the stronger bottleneck + independence pressure yields more interpretable factorized
codes on CelebA, 3D chairs, and 3D faces, beating VAE, InfoGAN, and (qualitatively) matching
semi-supervised DC-IGN. They also propose a linear-classifier protocol to score disentanglement
when some ground-truth factors are known.

## Key claims / results

- **β > 1 improves disentanglement** vs the unmodified VAE (β = 1): latent traversals isolate
  factors such as azimuth, emotion, hair style (CelebA), chair width / leg style, and face
  lighting / elevation more cleanly than entangled VAE baselines.
- Against prior art, unsupervised β-VAE discovers **overlapping or richer** factor sets than
  InfoGAN and matches or exceeds semi-supervised DC-IGN on labelled factors while also finding
  unlabelled ones (e.g. chair leg style).
- On a controlled 2D-shapes dataset (identity × X × Y × scale × rotation), their
  **disentanglement metric** scores β-VAE (β = 4) at **99.23%**, near ground truth / DC-IGN
  (~99–100%) and well above VAE (~62%), InfoGAN (~74%), PCA, and ICA.
- Informative latents have **high KL to the prior**; near-zero-KL units are unused — the same
  capacity story as posterior collapse, now used as a feature of the bottleneck.
- Trade-off: larger β can **blur reconstructions** and drop factors that move few pixels; β must
  be tuned (metric or visual heuristics), not left at 1.

## Methodology

- **Objective:** L = E_{q_φ(z|x)}[log p_θ(x|z)] − β D_KL(q_φ(z|x) ‖ p(z)), with p(z) = N(0, I).
  Derived as a KKT Lagrangian of max reconstruction subject to D_KL < ε.
- **Model:** convolutional encoder/decoder VAEs (architecture in their Tbl. 1); train with the
  reparameterization trick as in the original VAE.
- **Eval (qualitative):** fix all but one latent and traverse it on CelebA / chairs / faces;
  compare to VAE, InfoGAN, DC-IGN.
- **Eval (quantitative):** synthetic shapes with known factors; build z_diff vectors that hold one
  factor fixed across pairs; train a **low-VC linear classifier** to predict which factor was
  fixed — high accuracy ⇒ latents already factorized.

## Related

- extends [[2013-kingma-vae]] — same ELBO / reparameterized VAE, with β scaling the KL capacity
  and independence pressure
- background-for [[2019-rolinek-vae-pca-directions]] — Rolinek et al. analyze the β-VAE /
  diagonal-posterior mechanism that later disentanglement work builds on
- introduces [[beta-vae-weighted-kl-disentanglement]] — β-weighted KL as the canonical unsupervised
  disentanglement knob
- applies [[passive-latent-dimensions]] — high-β capacity limits leave unused axes near the prior
  (low KL), which the paper reads as uninformative latents
- contrasts [[monosemantic-features-vs-polysemantic-neurons]] — generative-factor disentanglement
  inside an end-to-end VAE vs post-hoc SAE features for LM superposition
- [[Sources MOC]]
- [[Autoencoder MOC]]
