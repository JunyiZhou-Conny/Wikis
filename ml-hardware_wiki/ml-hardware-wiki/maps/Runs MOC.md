---
title: Runs MOC
type: moc
tags:
  - moc
---

# Runs MOC

Live dashboard over every run the project engine catalogs. Tables are **[[Dataview]]**
queries — install Dataview (see [[obsidian_setup]] §3) and they refresh when you
regenerate vault notes.

> Notes in `runs/` are **auto-generated** — don't hand-edit. Fix the engine and re-emit.

## All runs (by date)

```dataview
TABLE status, engine, date, parent_id AS "Parent"
FROM "runs"
WHERE type = "run"
SORT date DESC
```

## Done runs

```dataview
TABLE status, metrics, tags, regenerate_cmd AS "Regenerate"
FROM "runs"
WHERE type = "run" AND status = "done"
SORT date DESC
LIMIT 20
```

## Failed / running

```dataview
TABLE status, date, regenerate_cmd AS "Regenerate"
FROM "runs"
WHERE type = "run" AND status != "done"
SORT date DESC
```

## Lineage roots (no parent)

```dataview
TABLE date, status, tags
FROM "runs"
WHERE type = "run" AND !parent_id
SORT date ASC
```
