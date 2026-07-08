# Literature sources domain profile

`vault_domain: literature-sources`

Use for academic papers, preprints, and technical reports across any field.

## Output folder

`sources/papers/` for markdown ingest notes (see subfolder table in [[vault-contract]]).
L0 PDFs go in `sources/raw/`.

## Filename convention

`{year}-{firstauthor}-{short-slug}.md` under `sources/papers/`, e.g.
`sources/papers/2013-cuturi-sinkhorn-distances.md`

## Required frontmatter

```yaml
type: source
source_kind: paper              # paper | article | course | book | discussion
tier:                           # A | B | C
venue: ""
year:
authors: []
approx_citations:
doi: ""
source_path: "sources/raw/<file>.pdf"
tags:
  - source
  - domain/ml
```

## Required body sections

```markdown
# Title

## Summary
One paragraph.

## Key claims / results
Benchmarks, claims, limitations.

## Methodology
Formulation, assumptions, algorithm.

## Related
Typed wikilinks — ≥2 concepts and ≥1 sibling source.
```

## Tag conventions

| Tag prefix | Example |
|---|---|
| `field/` | `field/math`, `field/ml`, `field/biology` |
| `topic/` | `topic/unbalanced-ot`, `topic/wasserstein` |
| `method/` | `method/sinkhorn`, `method/neural-ot` |
