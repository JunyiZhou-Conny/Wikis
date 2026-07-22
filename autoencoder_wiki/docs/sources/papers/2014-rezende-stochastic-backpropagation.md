---
title: "Stochastic Backpropagation and Approximate Inference in Deep Generative Models"
type: source
status: done
date: 2026-07-22
source_kind: paper
tier: A
venue: "ICML 2014"
year: 2014
authors: ["Rezende", "Mohamed", "Wierstra"]
approx_citations: 6900
doi: "10.48550/arXiv.1401.4082"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/vae
  - topic/autoencoder
  - method/vae
  - method/reparameterization
  - method/variational-inference
---

# Stochastic Backpropagation and Approximate Inference in Deep Generative Models

Rezende, Mohamed & Wierstra, *ICML 2014* (Google DeepMind). The **DeepMind co-founding VAE/DLGM paper** — develops stochastic backpropagation through latent Gaussians and trains deep directed generative models with a recognition-model encoder, contemporaneous with [[2013-kingma-vae]].

## Summary

The paper introduces **deep latent Gaussian models (DLGMs)**: layered directed models with Gaussian latents and nonlinear (MLP) transformations that generate observations by ancestral sampling. Exact marginal likelihoods are intractable, so they introduce a **recognition model** \(q(\xi\mid v)\) as a stochastic encoder and optimize a variational free-energy / ELBO. The enabling machinery is **stochastic backpropagation** — Gaussian gradient identities (Bonnet/Price) plus location-scale reparameterizations — so gradients flow through sampled latents and both generative and recognition parameters can be trained jointly with SGD (RMSprop). Empirically, DLGMs produce competitive MNIST likelihoods, realistic samples, useful 2D visualizations, and iterative missing-data imputation.

## Key claims / results

- **Stochastic backpropagation** gives low-variance gradients of expectations under Gaussian (and other location-scale) variational distributions, avoiding the poor scaling of REINFORCE-style score-function estimators.
- A **recognition model** conditioned on data amortizes approximate posterior inference and concentrates samples on posterior mass (unlike prior sampling).
- Rank-one + diagonal covariance structure in \(q\) captures posterior correlations at near-linear cost versus a full covariance.
- On binarized MNIST, DLGM test NLL reaches **87.30** (diagonal) / **86.60** (rank-one), beating factor analysis, NLGBN, and wake-sleep under the same architecture family, and competitive with strong density estimators of the era (RBM/DBN/NADE numbers quoted for context).
- Developed **concurrently and complementarily** with Kingma & Welling’s SGVB/AEVB treatment of the same reparameterization idea.

## Methodology

- **Generative model:** \(L\) layers of Gaussian latents \(\xi_l\sim\mathcal{N}(0,I)\), deterministic MLP maps \(T_l\), and observation likelihood \(\pi(v\mid T_0(h_1))\); recovers factor analysis / NLGBN as special cases.
- **Objective:** variational free energy \(\mathcal{F} = D_{\mathrm{KL}}[q(\xi)\|p(\xi)] - \mathbb{E}_q[\log p(v\mid\xi,\theta_g)p(\theta_g)]\) (ELBO-style lower bound on \(-\log p(v)\)).
- **Recognition model:** DAG of Gaussians (often MLP → mean / covariance factors), optionally with precision \(C^{-1}=D+uu^\top\).
- **Training:** minibatch Monte Carlo — bottom-up sample from \(q\), top-down generate, backprop via reparameterized Gaussian rules; update \(\theta_g\) and \(\theta_r\) together (Algorithm 1).

## Related

- contrasts [[2013-kingma-vae]] — contemporaneous sibling: DLGM / Bonnet–Price stochastic-backprop framing vs Kingma’s SGVB/AEVB presentation of the same amortized VI idea
- extends [[2006-hinton-deep-autoencoder]] — replaces deterministic bottleneck codes with deep latent Gaussians + variational recognition encoder
- background-for [[2018-lopez-scvi]] — scVI inherits amortized encoder + ELBO training from this VAE lineage
- introduces [[amortized-variational-inference]] — recognition model as stochastic encoder of approximate posteriors
- applies [[vae-elbo-scrna-count-models]] — free-energy / ELBO objective that count VAEs later specialize
- contrasts [[probabilistic-vae-vs-count-autoencoder]] — clarifies the variational (recognition + KL) side of that split at the method root
- [[Sources MOC]]
- [[Autoencoder MOC]]
