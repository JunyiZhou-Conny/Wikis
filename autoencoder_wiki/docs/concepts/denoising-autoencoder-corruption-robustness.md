---
title: Denoising autoencoder as corruption-robust representation learning
type: concept
status: done
date: 2026-07-12
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/denoising-autoencoder
distilled_from:
  - "[[2008-vincent-denoising-autoencoders]]"
  - "[[2006-hinton-deep-autoencoder]]"
  - "[[2019-eraslan-dca]]"
---

# Denoising autoencoder as corruption-robust representation learning

A **denoising autoencoder (DAE)** learns a representation by reconstructing a **clean** input
from a **corrupted** version — so the code must capture stable structure recoverable from
partial observation, not just memorize the identity map.

## Why it matters / where it shows up

Classic deep autoencoders train on clean reconstruction ([[2006-hinton-deep-autoencoder]]).
Vincent et al. add an explicit robustness criterion: partially destroy the input, then repair
it ([[2008-vincent-denoising-autoencoders]]). That idea recurs whenever "denoising" is the goal —
including count autoencoders that impute scRNA dropout ([[2019-eraslan-dca]]) — though the
corruption model and loss change with the domain.

## Details

- **Training signal:** x̃ ∼ q_D(·|x) (e.g. random masking / zeroing); minimize L(x, decode(encode(x̃))).
- **Why it helps:** blocks trivial identity solutions → overcomplete codes are usable; forces
  features that depend on redundant evidence across many dimensions.
- **Views:** manifold projection (off-manifold → on-manifold), variational bound on a generative
  model with a corruption stage, lower bound on I(X;Y) under corrupted inputs.
- **Not the same as SAE sparsity:** DAEs regularize via **input corruption**; sparse dictionary
  AEs regularize via **code sparsity** ([[sparse-autoencoder-dictionary-learning]]).

## Related

- introduces [[2008-vincent-denoising-autoencoders]] — canonical ICML formulation and SdA stacking
- extends [[2006-hinton-deep-autoencoder]] — stacked AE pretraining with a different local criterion
- applies [[2019-eraslan-dca]] — domain-specific denoising (ZINB/NB count loss) rather than
  generic coordinate blanking
- contrasts [[sparse-autoencoder-dictionary-learning]] — overcomplete codes via corruption vs L1
