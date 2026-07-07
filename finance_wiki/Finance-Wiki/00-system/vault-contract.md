---
title: vault-contract
type: system
tags:
  - system
---

# Vault contract (note-writing rules only)

> **The vault (`docs/`) is an AUTO-GENERATED view of the project engine — not a separate
> system you maintain by hand.** The engine + repo-root [`AGENTS.md`](../../AGENTS.md) are
> the source of truth; this file governs *how notes are shaped* so Obsidian and agents can
> read them deterministically.

For project rules, metrics, and commands → read `AGENTS.md` (outranks this file).

## Ground truth

- Ground every claim in artifacts and docs **actually present in the repo**.
- **Do not web-search** to fill project knowledge gaps — say what's missing and propose
  ingesting a source note instead.
- Long-form docs at `docs/` root (e.g. `framework.md`) are canonical prose; vault notes
  *distill and link* them.

## Directory rules

| Folder | Rule |
|---|---|
| `00-system/` | Contract, domain profiles, templates. Edit rarely. |
| `runs/` | **AUTO-GENERATED** — experiment/backtest/pipeline runs. Never hand-edit. |
| `sources/` | **AUTO-GENERATED** — papers, articles, learning material ingest. Never hand-edit. |
| `sources/discussions/` | Chat / podcast distillates (`source_kind: discussion`) |
| `sources/papers/` | Academic papers, preprints (`source_kind: paper`) |
| `sources/articles/` | External articles (`source_kind: article`) |
| `sources/courses/` | Course / lecture notes (`source_kind: course`) |
| `concepts/` | **AUTO-GENERATED** (distilled by engine/agent). Do not hand-write unless freezing a note. |
| `maps/` | MOC dashboards; structure stable, tables refresh from frontmatter. |
| `sources/raw/` | L0 originals (PDFs, clips) — gitignore large binaries in consumer repos. |

Source markdown notes must live in the subfolder that matches `source_kind` (see
[[Sources MOC]]). Wikilinks to sources use the filename stem only, not the folder path.

See the active domain profile in `00-system/domains/` (declared in `AGENTS.md` as
`vault_domain`).

## Autogeneration discipline

1. **Regenerate, don't patch** — if a run note is wrong, fix the engine and re-emit.
2. **`regenerate_cmd`** — every auto note must say how to rebuild it (e.g. `./hub vault`).
3. **Lineage** — set `parent_id` when a run/source clearly continues a predecessor.
4. **Wikilinks** — auto notes must link `wikilink_targets` and `[[Runs MOC]]` / `[[Sources MOC]]`.
5. **Conservative deletes** — archive (`status: archived`) instead of deleting linked notes.

## How concept notes are produced

Concepts are **distilled**, not typed by hand:

- Cluster related runs/sources
- Extract from long-form `framework.md` sections
- Run `/distill-concepts` (consumer-repo skill)

Use [[concept-note|concept template]] shape. One idea per note; ≥2 wikilinks in `## Related`.

## Tag taxonomy (keep it small)

**Universal:**

- Kind: `#run`, `#source`, `#concept`, `#moc`, `#system`
- Domain: `#domain/ml`, `#domain/finance`, `#domain/literature`

**Domain-specific tags** — defined in `00-system/domains/*.md`. Do not invent ad-hoc tags
by hand; change the engine so they regenerate.

## Agent precedence

1. Running engine behavior
2. `AGENTS.md`
3. Long-form framework docs
4. This vault contract
5. Auto-generated vault notes (runs, sources, concepts)

## Editing discipline

- Don't rename auto-generated run/source files; change the engine's id scheme instead.
- MOCs may be updated by `/regen-mocs` or wiki-lint; keep Dataview queries generic.
- Unresolved wikilinks (grey nodes) are acceptable — they mark concepts not yet distilled.
