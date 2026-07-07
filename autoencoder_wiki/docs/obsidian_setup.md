# Obsidian vault setup

How to use the `docs/` folder as an Obsidian knowledge graph, synced via git across machines.

## Big picture

| Layer | Where | What it holds |
|---|---|---|
| **L0 originals** | `sources/raw/` (PDFs often gitignored) | raw PDFs, clips, manifests |
| **Vault** | `docs/` in git | markdown graph (text + metadata + wikilinks) |
| **Reading room** | Obsidian on your Mac | browse graph + Dataview dashboards |

Notes are hand-written by you and the agent (via the `.cursor/skills/`). Keep heavy binaries
out of git; the vault holds text.

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
- **Settings → Groups:** color by tag, e.g. `tag:#source`, `tag:#concept`, `tag:#moc`.
- **Grey nodes** = unresolved wikilinks (targets not yet written) — normal, they mark ideas to fill in.

No build step. The `[[wikilinks]]` in your notes *are* the graph.

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
- Examples: `obsidian search query="vae"`, `obsidian backlinks file="sources/papers/2018-lopez-scvi"`

Requires Obsidian **running on a desktop** (typically Mac, not headless servers).
Cursor agents on Mac can call it from the integrated terminal.

Plain file writes work without the CLI — CLI is polish for append/backlinks.

---

## 5. Everyday loop

```
ingest-paper / daily-paper skill → source note (+ links)
        │
        ▼
distill-concepts → concept notes that connect sources
        │
        ▼
git commit + push  →  other machine: git pull → Obsidian + Dataview refresh
        │
        ▼
link-audit (on demand) → find orphans, propose typed edges
```

Notes are hand-written and freely editable. Keep one idea per concept note.

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
| `00-system/` | contract, domain profile, templates | you (rarely) |
| `sources/{kind}/` | ingest by type (`discussions/`, `papers/`, …) | you / `ingest-paper` / `daily-paper` |
| `concepts/` | atomic ideas | you / `distill-concepts` |
| `maps/` | MOC dashboards | you |
| `sources/raw/` | L0 PDFs + manifests (often gitignored) | you (drop files) |

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
