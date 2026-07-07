# AGENTS.md — finance_wiki

## Project

Finance knowledge wiki: macro/Fed cycles, asset bubbles, IPO mechanics (e.g. SpaceX SPCX), China personal FX controls, cross-border brokerage, US–China tech investment barriers.

## Vault

- **Obsidian vault root:** `Finance-Wiki/` (not repo root)
- **Scaffold version:** wiki-scaffold v0.1.1 — baseline at `../../wiki_scaffold`, read-only
- **vault_domain:** `finance-sources` (see `Finance-Wiki/00-system/domains/finance-sources.md`)
- **Sibling wikis:** `../autoencoder_wiki/`, listed in `../README.md`

## Hard rules

- **Never `git commit` or `git push` unless the user explicitly asks.**
- **Do not modify** `wiki_scaffold` when adding finance notes — edit this repo only.
- Concepts may be hand-distilled from discussions; runs/sources follow vault-contract when an engine exists.

## L0 artifacts

| Kind | Location |
|------|----------|
| Raw PDFs / clips | `Finance-Wiki/sources/raw/` |
| Distilled concepts | `Finance-Wiki/concepts/` |

## Where things live

| Path | Purpose |
|------|---------|
| `Finance-Wiki/maps/` | Home MOC, Finance Topics MOC, cross-vault indexes |
| `Finance-Wiki/concepts/` | Atomic finance ideas |
| `Finance-Wiki/sources/` | Ingest notes — subfolders by kind (`discussions/`, `papers/`, …) |
| `Finance-Wiki/00-system/` | Templates, vault-contract |

## Precedence

1. This `AGENTS.md`
2. `Finance-Wiki/00-system/vault-contract.md`
3. `Finance-Wiki/00-system/domains/finance-sources.md`
