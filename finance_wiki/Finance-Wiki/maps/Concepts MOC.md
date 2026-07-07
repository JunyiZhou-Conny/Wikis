---
title: Concepts MOC
type: moc
tags:
  - moc
---

# Concepts MOC

```dataview
TABLE status, date, source_doc, length(distilled_from) AS "From N sources"
FROM "concepts"
WHERE type = "concept"
SORT file.name ASC
```

## Related

- [[Home MOC]]
- [[Finance Topics MOC]]
