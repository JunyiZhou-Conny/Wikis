---
title: Sources MOC
type: moc
tags:
  - moc
---

# Sources MOC

Ingested papers, articles, and learning material.

## All sources

```dataview
TABLE source_kind, file.folder AS folder, year, authors, status, date
FROM "sources"
WHERE type = "source"
SORT file.folder ASC, date DESC
```

## By kind

| Subfolder | `source_kind` | What goes here |
|-----------|---------------|----------------|
| `sources/discussions/` | `discussion` | Cursor chats, podcast distillates |
| `sources/papers/` | `paper` | Academic papers, preprints |
| `sources/articles/` | `article` | External articles, blog posts |
| `sources/courses/` | `course` | Course / lecture notes |
| `sources/raw/` | — | L0 PDFs, clips (not markdown notes) |

## Papers

```dataview
TABLE file.folder AS folder, year, source_path
FROM "sources"
WHERE type = "source" AND source_kind = "paper"
SORT year DESC
```

## Recent ingest

```dataview
TABLE source_kind, file.folder AS folder, tags, regenerate_cmd AS "Regenerate"
FROM "sources"
WHERE type = "source"
SORT date DESC
LIMIT 15
```

## Related

- [[Home MOC]]
