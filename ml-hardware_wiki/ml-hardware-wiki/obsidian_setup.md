# Obsidian vault setup

How to use the `docs/` folder as an Obsidian knowledge graph, synced via git across
machines. This guide is **domain-agnostic** — adapt paths to your consumer project.

## Big picture

| Layer | Where | What it holds |
|---|---|---|
| **L0 factory** | compute env, local disk | raw data, run outputs, PDFs (often gitignored) |
| **Engine** | project repo code | catalog + vault emitter |
| **Vault** | `docs/` in git | markdown graph (text only, fast to sync) |
| **Reading room** | Obsidian on your Mac | browse graph + Dataview dashboards |

Keep heavy artifacts out of git. The vault holds **text + metadata + wikilinks**.

---

## 1. Install Obsidian

1. Install [Obsidian](https://obsidian.md) (**v1.12.4+** for optional CLI).
2. *Open folder as vault* → choose `<project>/docs/` (**not** the repo root).
3. Trust the folder when prompted.

**In this scaffold repo:** open `wiki_scaffold/docs/` directly to preview the template.

---

## 2. Graph view

- Left ribbon → graph icon, or *Cmd-P → "Open graph view"*.
- Nodes = notes; edges = `[[wikilinks]]`.
- **Settings → Groups:** color by tag, e.g. `tag:#run`, `tag:#source`, `tag:#concept`.
- **Grey nodes** = unresolved wikilinks (targets not yet generated) — normal during ingest.

No build step. Links you emit in auto-generated notes *are* the graph.

---

## 3. Community plugins

*Settings → Community plugins → Browse* (disable Restricted Mode first).

| Plugin | Required? | Purpose |
|---|---|---|
| **Dataview** | **Yes** | Live tables on MOC pages from YAML frontmatter |
| **Templater** | Optional | Auto-fill from `00-system/templates/` |

Commit plugin manifests once (see §6). Built-in **Graph** and **Properties** need no install.

---

## 4. Obsidian CLI (optional)

Obsidian 1.12.4+ ships a CLI that controls the running desktop app.

- *Settings → General → Command line interface → Register CLI*
- Examples: `obsidian search query="sharpe"`, `obsidian backlinks file="runs/my-run"`

Requires Obsidian **running on a desktop** (typically Mac, not headless servers).
Cursor agents on Mac can call it from the integrated terminal.

Plain file writes work without the CLI — CLI is polish for append/backlinks.

---

## 5. Everyday loop

```
Engine regen (./hub vault, /regen-vault, /log-source)
        │
        ▼
git commit + push
        │
        ▼
Other machine: git pull → Obsidian refreshes → Dataview tables update
        │
        ▼
/distill-concepts + /wiki-lint (scheduled or on demand)
```

**Do not hand-edit** `runs/` or `sources/`. Put durable prose in long-form `framework.md`
at `docs/` root; let concepts distill automatically.

---

## 6. Git hygiene

**Ignore (never commit):**

- `docs/.obsidian/workspace*.json`, `graph.json`, `appearance.json`, `app.json`
- `hotkeys.json`, `canvas.json`, `cache/`, `trash/`
- `docs/*.canvas`

**Commit once (when plugins change):**

- `docs/.obsidian/community-plugins.json`
- `docs/.obsidian/core-plugins.json`
- `docs/.obsidian/plugins/*/`

Merge conflicts in markdown are usually additive — keep both sides' knowledge, remove conflict markers.

---

## 7. Folder map

| Folder | Contents | Edited by |
|---|---|---|
| `00-system/` | contract, domains, templates | scaffold upgrades |
| `runs/` | auto-generated runs | engine |
| `sources/` | auto-generated ingest | engine / `/log-source` |
| `sources/{kind}/` | ingest by type (`discussions/`, `papers/`, …) | engine / `/log-source` |
| `concepts/` | auto-distilled ideas | `/distill-concepts` |
| `maps/` | MOC dashboards | scaffold + `/regen-mocs` |
| `sources/raw/` | L0 PDFs (often gitignored) | you (drop files) |

Start at [[Home MOC]].

---

## 8. Sources layout

Ingest notes live under `sources/{kind}/`, not flat in `sources/`:

| Folder | `source_kind` | Examples |
|--------|---------------|----------|
| `sources/discussions/` | `discussion` | Cursor conversations, podcast distillates |
| `sources/papers/` | `paper` | Academic papers |
| `sources/articles/` | `article` | External articles |
| `sources/courses/` | `course` | Course notes |
| `sources/raw/` | — | L0 PDFs, clips (not markdown) |

Browse via [[Sources MOC]] (Dataview table includes a `folder` column). Classification by
**ingest type** (folder) plus **topic tags** in frontmatter — not by topic subfolders, since
one source often spans many topics.
