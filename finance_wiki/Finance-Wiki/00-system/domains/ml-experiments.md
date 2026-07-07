# ML experiments domain profile

`vault_domain: ml-experiments`

Use for machine learning training runs, eval sweeps, and pipeline executions.

## Output folder

`docs/runs/` (consumer may alias legacy `experiments/` during migration)

## Filename convention

Chronological or catalog id, e.g.:

- `2026-06-11-001-baseline-transformer`
- `gpu__hvg_m2_ood__impact_cellot` (flat catalog id — sortable, grep-friendly)

## Required frontmatter

```yaml
type: run
family: "impact_cellot"           # model family or pipeline name
mode: "ood"                       # optional: iid | ood | train | val
metrics:
  r2: 0.92
  mmd: 0.04
  frac_gap_closed_decoded: 0.71   # project north-star — name in AGENTS.md
hyperparameters:
  learning_rate: 0.001
  batch_size: 64
dataset_hash: "sha256:…"
git_commit: "abc1234"
parent_id: "gpu__hvg_m2_iid__impact_cellot"
tags:
  - run
  - domain/ml
  - family/impact_cellot
  - mode/ood
```

## Tag conventions

| Tag prefix | Example | Meaning |
|---|---|---|
| `family/` | `family/scgen` | Model or pipeline family |
| `mode/` | `mode/ood` | Eval split mode |
| `data/` | `data/v08` | Dataset version |
| `hvg/` | `hvg/seurat_v3` | Preprocessing variant |

Add tags in the engine renderer, not by hand.

## Wikilink targets (typical)

- Sibling run in same experiment grid
- Concept notes: model names, metrics, preprocessing ideas
- `[[Runs MOC]]`

## Reference implementation

speciesOT `./hub vault` → `speciesOT/hub/vault.py`

When adopting scaffold, align output path to `runs/` and map `experiment_id` → `id`.

## L0 artifacts (not in vault)

- Results directories (`results/`, `cellot/.../results/`)
- `config.yaml`, `evals.csv`, metric sidecars
- Large figures → gitignored rich cards; link as plain paths in run notes
