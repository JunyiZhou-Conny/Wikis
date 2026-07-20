---
title: "Greedy Layer-Wise Training of Deep Networks"
type: source
status: done
date: 2026-07-20
source_kind: paper
tier: A
venue: "NIPS"
year: 2007
authors: ["Bengio", "Lamblin", "Popovici", "Larochelle"]
approx_citations: 5500
doi: "10.7551/mitpress/7503.003.0024"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - topic/dimensionality-reduction
  - method/autoencoder
  - method/rbm-pretraining
---

# Greedy Layer-Wise Training of Deep Networks

Bengio, Lamblin, Popovici & Larochelle, *NIPS* 2006 (NIPS 19, 2007). The **canonical analysis
of greedy layer-wise unsupervised pretraining** — shows the Hinton-style strategy is a general
principle, and that **stacked autoencoders** work as layer blocks alongside RBMs/DBNs.

## Summary

Deep nets are representationally more efficient than shallow ones, but random-init gradient descent
often fails. Hinton et al. had just introduced greedy layer-wise unsupervised training for Deep
Belief Networks. This paper studies *why* that strategy works, extends RBMs/DBNs to continuous
inputs, and — crucial for this wiki — shows the same layer-wise recipe succeeds when each layer
is an **auto-encoder** (auto-associator) rather than an RBM. Experiments on MNIST support that
unsupervised pretraining mainly **helps optimization** by placing weights near a good basin, while
also yielding more abstract codes that **generalize** better once the full net is fine-tuned.

## Key claims / results

- **Stacked autoencoders ≈ DBNs for pretraining:** after supervised fine-tuning, AE-initialized
  deep nets match DBN pretraining on MNIST (test error ~1.4% vs ~1.2%), and both beat
  no-pretraining deep nets (~2.4%) and shallow nets (~1.9%).
- **Unsupervised beats supervised greediness:** purely supervised layer-wise pretraining is worse
  (~2.0% test) — too greedy; a one-hidden-layer supervised stage can discard information that
  deeper composition would have used.
- **Optimization + representation hypothesis:** when the top hidden layer is constrained to 20
  units, nets *without* pretraining fail to fit the training set well (high variance); with
  pretraining they still train and generalize — evidence that lower layers were initialized into
  useful codes, not that the top alone was memorizing.
- Continuous-input RBM/DBN extensions (Gaussian / truncated-exponential units) improve
  predictive models on real-valued data; when p(x) is uninformative about y, **partial
  supervision** on the first layer restores the benefit of the greedy stack.

## Methodology

- **DBN baseline:** greedy contrastive-divergence training of stacked RBMs, then optional
  supervised fine-tuning of the mean-field deep net.
- **Auto-encoder stack:** train each layer to minimize reconstruction cross-entropy
  `R = −∑ x_i log p_i(x) + (1−x_i) log(1−p_i(x))` with
  `p(x) = sigm(c + W sigm(b + W'x))`; stack by feeding (deterministic) codes upward; then
  add a logistic output and fine-tune end-to-end.
- **Controls:** supervised greedy layer-wise init; deep net with random init; shallow net;
  Experiment 3 shrinks the top hidden layer to 20 units to stress-test the optimization story.
- Continuous units: change energy / sampling while keeping CD-style updates.

## Related

- extends [[2006-hinton-deep-autoencoder]] — same deep AE / RBM-pretraining lineage; shows the
  greedy principle is not RBM-specific and that stacked autoencoders initialize deep nets about
  as well as DBNs
- background-for [[2013-kingma-vae]] — documents the pretraining-era solution to deep
  encoder/decoder training that end-to-end ELBO optimization later largely replaced
- introduces [[greedy-layer-wise-unsupervised-pretraining]] — the general "train one unsupervised
  layer at a time, then fine-tune" principle
- background-for [[vae-vs-linear-nonlinear-dr-benchmarks]] — makes deep nonlinear AE stacks
  trainable, the optimization half of the "deep AE vs shallow/linear DR" story
- [[Sources MOC]]
- [[Autoencoder MOC]]
