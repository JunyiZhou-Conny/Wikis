---
title: "Flow Matching for Generative Modeling"
type: source
status: done
date: 2026-07-21
source_kind: paper
tier: A
venue: "ICLR 2023"
year: 2023
authors: ["Lipman", "Chen", "Ben-Hamu", "Nickel", "Le"]
approx_citations: 4100
doi: "10.48550/arXiv.2210.02747"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/neural-ot
  - topic/wasserstein
  - method/neural-ot
---

# Flow Matching for Generative Modeling

Lipman, Chen, Ben-Hamu, Nickel & Le, *ICLR 2023* (Meta AI / FAIR). The canonical
**Flow Matching** paper: simulation-free CNF training via conditional vector-field
regression, with **OT displacement interpolants** as the key non-diffusion path.

## Summary

Continuous normalizing flows can model arbitrary probability paths, but scalable training
beyond diffusion was blocked by ODE-simulation costs or biased gradients. This paper
introduces **Flow Matching (FM)**: regress a neural vector field \(v_t\) onto a target field
\(u_t\) that generates a chosen path \(p_t\). The marginal FM loss is intractable, so they
prove **Conditional Flow Matching (CFM)** — regressing onto per-sample conditional fields
\(u_t(x\mid x_1)\) — has identical \(\theta\)-gradients. Gaussian conditional paths recover
diffusion VE/VP as special cases; the standout instance uses McCann's **OT displacement
interpolant** between noise and a concentrated Gaussian at \(x_1\), yielding straight,
constant-speed conditional trajectories that train and sample faster than curved diffusion
paths on ImageNet.

## Key claims / results

- **Thm. 1:** the mixture of conditional vector fields (eq. 8) generates the marginal path
  \(p_t=\int p_t(\cdot\mid x_1)\,q(x_1)\,dx_1\).
- **Thm. 2:** under positivity, \(\nabla_\theta\mathcal{L}_{\mathrm{FM}}=\nabla_\theta\mathcal{L}_{\mathrm{CFM}}\),
  so CNFs train simulation-free without knowing the marginal field.
- **Thm. 3:** for Gaussian paths \(p_t=\mathcal{N}(\mu_t(x_1),\sigma_t^2 I)\), the affine flow
  \(\psi_t(x)=\sigma_t x+\mu_t\) has closed-form VF
  \(u_t=(\sigma'_t/\sigma_t)(x-\mu_t)+\mu'_t\).
- **OT conditional path:** \(\mu_t=tx_1\), \(\sigma_t=1-(1-\sigma_{\min})t\) is the OT
  displacement map between \(\mathcal{N}(0,I)\) and \(\mathcal{N}(x_1,\sigma_{\min}^2 I)\);
  particles move in straight lines at constant speed (vs diffusion overshoot/backtracking).
- Empirically (same U-Net): FM-OT beats DDPM / score matching / ScoreFlow on CIFAR-10 and
  ImageNet 32/64 in NLL, FID, and NFE; ImageNet-128 FID 20.9; faster FID descent in training;
  better low-NFE quality/cost tradeoff; strong \(64\to 256\) super-resolution FID/IS.
- Caveat: conditional OT optimality does **not** imply the learned *marginal* field is a
  global OT solution — later OT-CFM / BatchOT work tightens that link.

## Methodology

- Sample \(t\sim U[0,1]\), \(x_1\sim q\), \(x_0\sim\mathcal{N}(0,I)\); form
  \(\psi_t(x_0)=\sigma_t x_0+\mu_t(x_1)\); regress \(v_t(\psi_t(x_0))\) onto
  \(\frac{d}{dt}\psi_t(x_0)\) (for OT: target \(x_1-(1-\sigma_{\min})x_0\)).
- Inference: draw \(x_0\sim\mathcal{N}(0,I)\), integrate the learned ODE with off-the-shelf
  solvers (dopri5 / fixed-step midpoint); likelihood via the CNF change-of-variables.
- Ablations hold architecture fixed and swap diffusion vs OT conditional paths under FM, plus
  score-matching / DDPM baselines.

## Related

- introduces [[neural-optimal-transport]] — simulation-free CNF / flow-matching route to neural
  transport, with OT displacement paths as the supervising geometry
- applies [[monge-kantorovich-formulations]] — McCann OT displacement interpolant as the
  conditional probability path between noise and data Gaussians
- applies [[wasserstein-distance]] — conditional paths are \(W_2\) OT maps between isotropic
  Gaussians; straight trajectories approximate efficient transport
- extends [[2023-korotin-neural-optimal-transport]] — sibling neural OT line; Lipman learns a
  continuous generative VF under OT paths vs Korotin's maximin dual for strong/weak plans
- benchmarks [[2023-bunne-cellot-neural-ot]] — both recover continuous transport maps; Lipman via
  FM-OT CNFs for images, CellOT via ICNN Monge maps for single-cell perturbations
- [[Sources MOC]]
- [[Optimal Transport MOC]]
