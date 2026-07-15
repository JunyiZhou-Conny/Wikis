---
title: "Scaling Monosemanticity: Extracting Interpretable Features from Claude 3 Sonnet"
type: source
status: done
date: 2026-07-15
source_kind: paper
tier: A
venue: "Transformer Circuits Thread (Anthropic)"
year: 2024
authors: ["Templeton", "Conerly", "Marcus", "Lindsey", "Bricken", "Chen", "Pearce", "Henighan", "Olah"]
approx_citations: 860
doi: ""
source_path: "sources/raw/sae/"
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# Scaling Monosemanticity: Extracting Interpretable Features from Claude 3 Sonnet

Templeton, Conerly, Marcus, Lindsey, Bricken, Henighan, Olah et al., *Transformer Circuits Thread*
(Anthropic), May 2024. Shows that **sparse autoencoders scale** from toy one-layer LMs to a
production model (Claude 3 Sonnet), recovering millions of interpretable features via
**scaling-law–guided** dictionary learning on the residual stream.

## Summary

Towards Monosemanticity left open whether SAE dictionary learning would work on frontier-scale
transformers. This paper trains SAEs with up to **~34M features** on Claude 3 Sonnet's **middle-layer
residual stream**, choosing width and training steps with compute **scaling laws**. The learned
features are often monosemantic, highly abstract (multilingual, multimodal, concrete↔abstract),
and causally steerable — including safety-relevant directions (deception, sycophancy, bias,
power-seeking). The authors stress remaining gaps: incomplete dictionaries and weak faithfulness
metrics.

## Key claims / results

- **SAEs work at production scale:** 1M / 4M / 34M-feature dictionaries on Sonnet's mid residual
  stream yield interpretable features; reconstruction explains **≥65%** of activation variance with
  **<300** active features per token on average.
- **Scaling laws guide SAE training:** compute-optimal loss follows a power law; optimal FLOPS
  split between dictionary width and training steps also scale as power laws (width growing
  somewhat faster than steps in the tested regime); learning rate should shrink with budget.
- **Features are abstract and cross-modal:** e.g. Golden Gate Bridge, brain sciences, transit
  infrastructure — often fire across languages and on images despite text-only SAE training;
  concept frequency systematically relates to the dictionary size needed to resolve a feature.
- **Steering works:** intervening on feature activations changes Sonnet's behavior in ways that
  match the interpretation (specificity + influence checks, plus automated interpretability vs
  neurons).
- **Safety-relevant features exist** (deception, sycophancy, bias, dangerous content) and
  influence outputs when manipulated — but existence ≠ the model will act on them in deployment.
- **Dead features grow with width** (~2% / 35% / 65% for 1M / 4M / 34M), so training procedure
  remains a bottleneck.

## Methodology

- **Subject:** Claude 3 Sonnet (finetuned production model, March 2024); SAE on **middle-layer
  residual stream** (cheaper than MLP; mitigates cross-layer superposition; mid-depth for abstract
  features).
- **Architecture:** ReLU encoder → linear decoder; activations normalized so mean squared L2 =
  residual dim \(D\); loss = MSE reconstruction + L1 on \(f_i(\mathbf{x})\cdot\|\mathbf{W}^{\mathrm{dec}}_{\cdot,i}\|_2\)
  (decoder-norm–weighted sparsity so unit decoder columns are feature directions).
- **Scale:** dictionaries of 1,048,576 / 4,194,304 / 33,554,432 features; L1 coefficient 5 (under
  their normalization); LR chosen from a narrow sweep suggested by scaling analysis.
- **Scaling-law sweep:** treat (width × steps) as the compute axes; pick 34M training length to
  minimize proxy loss at fixed budget; extrapolate LR.
- **Eval:** hand + automated interpretability (specificity rubrics, steering / influence),
  geometry and computational-role analyses; dead features = inactive on \(10^7\) tokens.

## Related

- extends [[2023-bricken-towards-monosemanticity]] — same SAE dictionary-learning recipe, scaled from a 512-neuron one-layer MLP to Claude 3 Sonnet's residual stream
- extends [[2006-hinton-deep-autoencoder]] — reconstructive AE skeleton retained; capacity flipped to million-scale overcomplete sparse codes for interpretability
- applies [[sparse-autoencoder-dictionary-learning]] — SAE as weak dictionary learning, now with decoder-norm–weighted L1 and production-scale width
- applies [[monosemantic-features-vs-polysemantic-neurons]] — monosemantic feature unit of analysis validated on a frontier LM, including safety-relevant directions
- introduces [[sae-scaling-laws]] — compute scaling laws that allocate FLOPS between dictionary width and training steps
- [[Sources MOC]]
- [[Autoencoder MOC]]
