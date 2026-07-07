---
title: Sources MOC
type: moc
tags:
  - moc
---

# Sources MOC

Ingested papers, articles, and learning material. Papers carry a **tier** (see
[[vault-contract]] → credibility standard).

## Papers by tier

```dataview
TABLE tier, venue, year, approx_citations AS cites, authors
FROM "sources"
WHERE type = "source" AND source_kind = "paper"
SORT tier ASC, approx_citations DESC
```

## All sources

```dataview
TABLE source_kind, file.folder AS folder, tier, year, status, date
FROM "sources"
WHERE type = "source"
SORT date DESC
```

## By kind

| Subfolder | `source_kind` | What goes here |
|-----------|---------------|----------------|
| `sources/discussions/` | `discussion` | Cursor chats, podcast distillates |
| `sources/papers/` | `paper` | Academic papers, preprints (require `tier`) |
| `sources/articles/` | `article` | External articles, blog posts |
| `sources/courses/` | `course` | Course / lecture notes |
| `sources/raw/` | — | L0 PDFs, clips (not markdown notes) |

## Recent ingest

```dataview
TABLE source_kind, tier, file.folder AS folder, date
FROM "sources"
WHERE type = "source"
SORT date DESC
LIMIT 15
```

## Needs review — missing credibility metadata

```dataview
TABLE venue, year, tier
FROM "sources"
WHERE type = "source" AND source_kind = "paper" AND (!tier OR !venue OR !approx_citations)
```

## Related

- [[Home MOC]]
