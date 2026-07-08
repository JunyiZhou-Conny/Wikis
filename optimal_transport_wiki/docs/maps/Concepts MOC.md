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

## Thinly linked (fewer than 2 sources — candidates for the link audit)

```dataview
TABLE distilled_from, date
FROM "concepts"
WHERE type = "concept" AND length(distilled_from) < 2
```

## Related

- [[Home MOC]]
