# Literature sources domain profile

`vault_domain: literature-sources`

Use for academic papers, preprints, and technical reports across any field.

## Output folder

`sources/papers/` for markdown ingest notes (see subfolder table in [[vault-contract]]).
L0 PDFs go in `sources/raw/`.

## Filename convention

`{date}-{seq}-{author-slug-short-title}.md` under `sources/papers/`, e.g.
`sources/papers/2026-06-11-001-vaswani-attention-is-all-you-need.md`

## Required frontmatter

```yaml
type: source
source_kind: paper              # paper | preprint | report | thesis
source_path: "sources/raw/attention-is-all-you-need.pdf"
authors: ["Vaswani", "Shazeer", "Parmar"]
year: 2017
venue: "NeurIPS"
tags:
  - source
  - domain/literature
  - field/ml
  - method/attention
```

## Required body sections

```markdown
# Title

## Summary
One paragraph.

## Methodology
Architecture, training, assumptions.

## Key results
Benchmarks, claims, limitations.

## Concepts introduced
Wikilinks to [[concept notes]] (auto-created by distill step).

## Related
- [[Sources MOC]]
- Prior work links
```

## Ingest pipeline

1. PDF → `sources/raw/`
2. `/log-source` extracts text, writes structured markdown under `sources/papers/`
3. `/distill-concepts` creates `concepts/` for methods and ideas
4. Optional: link `type: run` notes that cite this source via `source_refs`

## Tag conventions

| Tag prefix | Example |
|---|---|
| `field/` | `field/biology`, `field/finance` |
| `method/` | `method/transformer`, `method/ot` |

## L0 artifacts

- PDFs in `sources/raw/` (gitignore or Git LFS for large libraries)
