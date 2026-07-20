---
title: Greedy layer-wise unsupervised pretraining
type: concept
status: done
date: 2026-07-20
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/autoencoder
  - method/rbm-pretraining
distilled_from:
  - "[[2007-bengio-greedy-layer-wise]]"
  - "[[2006-hinton-deep-autoencoder]]"
---

# Greedy layer-wise unsupervised pretraining

**Greedy layer-wise unsupervised pretraining** builds a deep network by training **one layer at a
time** with a local unsupervised objective (RBM contrastive divergence or autoencoder
reconstruction), then **fine-tunes** all layers jointly on the task of interest.

## Why it matters / where it shows up

Before reliable end-to-end deep training, this was the practical way to get deep autoencoders and
classifiers to work ([[2006-hinton-deep-autoencoder]]). Bengio et al. showed it is a **general
principle**, not an RBM quirk: stacked autoencoders match DBN pretraining, and the main win is
better **optimization / initialization**, with a side benefit of more abstract codes
([[2007-bengio-greedy-layer-wise]]). Later denoising and sparse AE stacks reuse the same
layer-wise composition pattern with different local criteria.

## Details

- **Greedy step:** fit layer ℓ to model (or reconstruct) the representation from layer ℓ−1;
  freeze or keep those weights as init for the next stage.
- **Building blocks:** RBM (CD) or autoencoder (reconstruction cross-entropy / MSE); width need
  not strictly decrease — weight decay + SGD often block trivial identity maps.
- **Fine-tuning:** supervised (or reconstructive) gradient descent on the full stack after
  pretraining.
- **Failure mode:** if p(x) carries little information about y, pure unsupervised greediness
  underperforms; partial supervision on early layers is a fix.
- **Modern contrast:** VAEs and deep nets usually train end-to-end from random (or simple) init;
  the concept remains the historical root of "stacked AE" pipelines.

## Related

- introduces [[2007-bengio-greedy-layer-wise]] — systematic MNIST / continuous-input study; AE
  stacks vs DBN vs supervised-greedy vs no pretraining
- introduces [[2006-hinton-deep-autoencoder]] — RBM layer-wise pretraining then fine-tuning a
  deep bottleneck autoencoder (Science 2006)
- background-for [[vae-vs-linear-nonlinear-dr-benchmarks]] — enables the deep nonlinear AE side
  of AE-vs-PCA comparisons
- contrasts [[2013-kingma-vae]] — layer-wise unsupervised init vs single ELBO trained end-to-end
  with the reparameterization trick
