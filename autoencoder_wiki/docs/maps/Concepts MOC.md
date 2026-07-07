---
title: Concepts MOC
type: moc
tags:
  - moc
---

# Concepts MOC

Atomic ideas that connect sources. Each should link ≥2 sources (see [[vault-contract]]).

## All concepts

```dataview
TABLE status, date, length(distilled_from) AS "From N sources"
FROM "concepts"
WHERE type = "concept"
SORT file.name ASC
```

## Recently added

```dataview
TABLE distilled_from, date
FROM "concepts"
WHERE type = "concept"
SORT date DESC
LIMIT 15
```

## Thinly linked (fewer than 2 sources — candidates for the link audit)

```dataview
TABLE distilled_from, date
FROM "concepts"
WHERE type = "concept" AND length(distilled_from) < 2
```

Also browse graph view with filter `tag:#concept` for connectivity.
