# AGENTS.md — autoencoder_wiki

## Project

Hand-curated research brain for autoencoders, VAEs, and representation learning. Every note
is written by you or the agent — no code engine, nothing auto-generated.

## Vault

- **Obsidian vault root:** `docs/`
- **vault_domain:** `literature-sources` (see `docs/00-system/domains/literature-sources.md`)
- **Sibling wikis:** `../finance_wiki/`, `../ml-hardware_wiki/`

## Hard rules

- **Never `git commit` or `git push` unless the user explicitly asks** — *except* the
  `daily-paper` skill, which is pre-authorized to commit **and push** a single
  credibility-gated paper (files under `docs/` only). Nothing else may commit or push.
- **High source bar.** Papers must clear the credibility standard in
  `docs/00-system/vault-contract.md`. Don't ingest tier-C sources silently.
- **Link everything.** Every new source links ≥2 concepts and ≥1 sibling source; every
  concept links ≥2 sources. Use typed links (`extends`, `benchmarks`, `contradicts`, …).

## Where things live

| Path | Purpose |
|------|---------|
| `docs/maps/` | Home MOC, topic indexes |
| `docs/concepts/` | Atomic ideas connecting sources |
| `docs/sources/{kind}/` | Ingested papers / articles / courses / discussions |
| `docs/sources/raw/` | L0 PDFs + manifests |
| `docs/00-system/` | Contract, domain profile, templates |

## Skills (verbs)

| Skill | Use |
|---|---|
| `ingest-paper` | URL/PDF → credibility-gated, tiered, linked source note |
| `distill-concepts` | Turn one or more sources into atomic concept notes |
| `link-audit` | Find orphans / thin links, propose typed edges |
| `daily-paper` | Scheduled: add one top-tier paper on a wiki topic |

## Precedence

1. This `AGENTS.md`
2. `docs/00-system/vault-contract.md`
3. `docs/00-system/domains/literature-sources.md`
