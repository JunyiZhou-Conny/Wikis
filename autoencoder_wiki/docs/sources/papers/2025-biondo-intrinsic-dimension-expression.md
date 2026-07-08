---
title: "The intrinsic dimension of gene expression during cell differentiation"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: B
venue: "Nucleic Acids Research"
year: 2025
authors: ["Biondo", "Cirone", "Valle", "Lazzardi", "Caselle", "Osella"]
approx_citations: 3
doi: "10.1093/nar/gkaf805"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/scrna
  - topic/dimensionality-reduction
---

# The intrinsic dimension of gene expression during cell differentiation

Biondo et al., *Nucleic Acids Research* 2025 (preprint bioRxiv 2024). Estimates the **intrinsic
dimension (ID)** of single-cell expression and links it to biology — the quantity a principled
latent-dim choice should track.

## Summary

The paper argues that the **intrinsic dimension** of single-cell transcriptomic profiles
**decreases as cells differentiate**, mirroring Waddington's landscape. Using ID estimators, it
defines a **potency score** (higher ID ⇒ more stem/pluripotent) that reproduces known potency
hierarchies across species and protocols without prior biological labels.

## Key claims / results

- ID of expression profiles is a **robust, label-free potency score**; it drops along
  differentiation trajectories.
- Validated across many datasets, species, and differentiation processes.
- Compares ID estimators: **projective/PCA-based** ones (number of PCs for a given % variance,
  eigenvalue entropy, Gini of eigenvalues) vs **geometric** ones (TwoNN). TwoNN is preferred as
  more robust to curvature/outliers than the PCA-based counts.

## Methodology

- Multiple ID estimators on sub-sampled cell populations; TwoNN as the main geometric estimator.
- Analogy to the Hopfield model: "differentiation" simulated by lowering temperature.

## Relevance to your question

- Directly relevant to "what should set the latent dimension": the honest target is the data's
  **intrinsic dimension**, not a fixed PCA variance cutoff. Notably it treats the **PCA
  variance-explained count as *one* ID estimator among several**, and finds geometric estimators
  more reliable — evidence against over-trusting a PCA 95%/99% rule as *the* answer.

## Related

- background-for [[intrinsic-dimension-latent-sizing]] — provides scRNA intrinsic-dimension estimates a latent dim should track
- applies [[choosing-latent-dimension]] — frames latent sizing as an intrinsic-dimension estimation problem on real biology
- extends [[scrna-dr-pipeline-hvg-to-latent]] — informs how aggressively the HVG→latent step can compress
- benchmarks [[2020-li-dr-benchmark]] — sibling scRNA DR source in the vault
- [[Sources MOC]]
- [[Autoencoder MOC]]
