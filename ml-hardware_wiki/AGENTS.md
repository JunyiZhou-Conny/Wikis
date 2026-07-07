# AGENTS.md — ml-hardware_wiki

## Project

Knowledge wiki for CPU/GPU hardware, model training performance, and practical training
engineering (memory, throughput, scaling, framework tradeoffs).

## Vault

- **Obsidian vault root:** `ml-hardware-wiki/` (not repo root)
- **Scaffold version:** wiki-scaffold v0.1.1 — baseline at `../../wiki_scaffold`, read-only
- **vault_domain:** `ml-experiments` (see `ml-hardware-wiki/00-system/domains/ml-experiments.md`)
- **Sibling wikis:** `../finance_wiki/`, `../autoencoder_wiki/`

## Hard rules

- **Never `git commit` or `git push` unless the user explicitly asks.**
- **Do not modify** `wiki_scaffold` for daily notes — edit this repo only.
- Concepts may be hand-distilled from discussions; runs/sources follow vault-contract when an engine exists.

## L0 artifacts

| Kind | Location |
|------|----------|
| Raw PDFs / clips | `ml-hardware-wiki/sources/raw/` |
| Distilled concepts | `ml-hardware-wiki/concepts/` |
| Training benchmarks (future) | `ml-hardware-wiki/runs/` |

## Where things live

| Path | Purpose |
|------|---------|
| `ml-hardware-wiki/maps/` | Home MOC, Training Hardware MOC |
| `ml-hardware-wiki/concepts/` | Atomic ideas (GPU memory, batching, scaling, …) |
| `ml-hardware-wiki/sources/` | Ingest notes — subfolders by kind (`discussions/`, `papers/`, …) |
| `ml-hardware-wiki/runs/` | Benchmark / experiment notes (when available) |
| `ml-hardware-wiki/00-system/` | Templates, vault-contract |

## Precedence

1. This `AGENTS.md`
2. `ml-hardware-wiki/00-system/vault-contract.md`
3. `ml-hardware-wiki/00-system/domains/ml-experiments.md`
