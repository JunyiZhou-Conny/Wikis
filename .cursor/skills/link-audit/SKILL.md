---
name: link-audit
description: Audit the wiki graph for orphans, thin links, missing credibility metadata, and broken wikilinks, then propose typed edges to add. Use when the user wants to check links, find orphans, improve connectivity, or lint the wiki.
disable-model-invocation: true
---

# Link audit

Find weak spots in the knowledge graph and propose concrete fixes. Read-first: report before
editing, then apply the fixes the user accepts.

## Checks

```
- [ ] 1. Orphans: source/concept notes with 0 outgoing wikilinks in ## Related
- [ ] 2. Thin sources: source notes linking < 2 concepts or < 1 sibling source
- [ ] 3. Thin concepts: concept notes with < 2 sources in distilled_from / Related
- [ ] 4. Missing credibility: papers lacking tier / venue / approx_citations
- [ ] 5. Broken wikilinks: [[targets]] with no matching file (grey nodes) — list them
- [ ] 6. Untyped links: ## Related entries that are bare wikilinks with no relationship verb
```

Use `Grep`/`Glob` over `docs/sources/` and `docs/concepts/` to gather these. The
"Needs review" and "Thinly linked" Dataview blocks in the MOCs cover 3–4 inside Obsidian.

## Propose edges

For each thinly-linked note, suggest **specific typed links** to real notes in the wiki, e.g.
"link `2021-xu-scanvi` → `extends [[2018-lopez-scvi]]`". Prefer connecting to existing notes;
only suggest a new concept when two+ sources clearly share an idea that has no note yet.

## Output

A short report grouped by check, each item with the file and the proposed fix. Then apply the
fixes the user approves. Do not commit to git.
