---
title: "Auto-Encoding Variational Bayes (VAE)"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "ICLR 2014 (arXiv 2013)"
year: 2013
authors: ["Kingma", "Welling"]
approx_citations: 40000
doi: "10.48550/arXiv.1312.6114"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/autoencoder
  - method/vae
  - method/reparameterization
---

# Auto-Encoding Variational Bayes (VAE)

Kingma & Welling, *ICLR 2014* (arXiv Dec 2013). The **foundational VAE paper** — introduces the
reparameterization trick and the SGVB/AEVB estimator that every VAE in this wiki descends from.

## Summary

The paper asks how to do efficient inference and learning in directed probabilistic models with
continuous latent variables and intractable posteriors, at scale. It reparameterizes the
variational lower bound (ELBO) into an estimator that is differentiable and optimizable with
plain stochastic gradient descent (**SGVB**), and fits an amortized recognition/encoder network
to approximate the posterior (**AEVB**). When the recognition model is a neural net, the result
is the **variational autoencoder**.

## Key claims / results

- The **reparameterization trick** (`z = μ + σ·ε`, `ε ~ N(0,1)`) makes the ELBO low-variance and
  backprop-friendly — the core enabling idea.
- **Amortized inference**: a single encoder network predicts the posterior for any datapoint, so
  no per-datapoint iterative inference (unlike MCMC) is needed.
- Scales to large datasets; demonstrated on MNIST and Frey Faces with strong likelihood results.

## Methodology

- **Objective:** maximize the ELBO = reconstruction term − KL(q(z|x) ‖ p(z)), with p(z) a
  standard Gaussian prior.
- **Encoder** `q(z|x)` and **decoder** `p(x|z)` are neural nets trained jointly.
- **Estimator:** SGVB, made possible by reparameterizing the latent sampling step.

## Related

<Typed links — this is the root that the wiki's applied VAE papers build on.>

- extends [[2006-hinton-deep-autoencoder]] — adds a probabilistic latent + ELBO to the deep autoencoder
- background-for [[2018-lopez-scvi]] — scVI is a VAE (this framework) with a ZINB decoder for counts
- background-for [[2018-way-tybalt]] — Tybalt applies the VAE directly to transcriptomes
- introduces [[vae-elbo-scrna-count-models]] — the ELBO / KL objective these count models adapt
- contrasts [[probabilistic-vae-vs-count-autoencoder]] — defines the "variational" side of that split
- contrasts [[2023-bricken-towards-monosemanticity]] — end-to-end ELBO latents vs post-hoc L1-sparse AE on frozen activations
- [[Sources MOC]]
- [[Autoencoder MOC]]
