---
title: k-sparse autoencoder (hard Top-k)
type: concept
status: done
date: 2026-07-18
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/sparse-autoencoder
distilled_from:
  - "[[2014-makhzani-k-sparse-autoencoders]]"
  - "[[2023-bricken-towards-monosemanticity]]"
  - "[[2006-hinton-deep-autoencoder]]"
---

# k-sparse autoencoder (hard Top-k)

A **k-sparse autoencoder** is a (usually linear, tied-weight) autoencoder that enforces sparsity
by keeping only the **k largest** hidden activations and zeroing the rest — so
**\(L_0 \le k\)** is set directly, with no L1 coefficient to tune.

## Why it matters / where it shows up

Classic deep AEs compress through a bottleneck ([[2006-hinton-deep-autoencoder]]). k-sparse AEs
instead allow an overcomplete hidden layer and regularize by **exact support selection**
([[2014-makhzani-k-sparse-autoencoders]]). That hard Top-k mechanism is the conceptual ancestor
of modern TopK SAEs used for LM dictionary learning, which often swap L1+ReLU
([[2023-bricken-towards-monosemanticity]]) for the same fixed-\(L_0\) activation.

## Details

- **Forward:** \(z = W^\top x + b\), then \(z \leftarrow \mathrm{TopK}(z)\) (or equivalent
  adaptive threshold / sort); reconstruct from the sparsified code.
- **Train:** backprop reconstruction error only through the active support; optionally **anneal
  \(k\)** from large → target so units do not die early.
- **Vs L1 SAEs:** L1 shrinks magnitudes and needs a \(\lambda\) schedule; hard k-sparse sets
  cardinality exactly and can use pure MSE.
- **Sparsity level as inductive bias:** larger \(k\) → local filters; smaller \(k\) → more
  global parts — a knob for shallow vs deep downstream use.
- **Encoding mismatch:** training support size \(k\) need not equal the feature support
  \(\alpha k\) used for classification.

## Related

- introduces [[2014-makhzani-k-sparse-autoencoders]] — original ICLR formulation and MNIST/NORB results
- contrasts [[2023-bricken-towards-monosemanticity]] — L1+ReLU SAE sparsity vs hard Top-k cardinality
- extends [[2006-hinton-deep-autoencoder]] — reconstructive AE with overcomplete sparse code instead of bottleneck compression
- applies [[sparse-autoencoder-dictionary-learning]] — dictionary learning via AE + exact sparse coding step
