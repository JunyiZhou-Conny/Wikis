---
title: vault-contract
type: system
tags:
  - system
---

# Vault contract (note-writing rules)

This is a **hand-curated research brain**. Notes are written by you and the agent — there is
no code engine and nothing is auto-generated. This file governs *how notes are shaped* so
Obsidian and agents can read them deterministically.

Project rules and commands live in [`AGENTS.md`](../../AGENTS.md), which outranks this file.

## Note types (only three)

| Type | Folder | What it is |
|---|---|---|
| `source` | `sources/{kind}/` | One ingested paper / article / course / discussion |
| `concept` | `concepts/` | One atomic idea that connects ≥2 sources |
| `moc` | `maps/` | Topic hub / index |

`sources/raw/` holds L0 originals (PDFs, clips) and manifests — not markdown notes.

## Credibility standard (papers)

Every `source` with `source_kind: paper` must declare a **tier**. Papers below the bar are
not ingested silently — flag them and ask.

| Tier | Bar | Examples |
|---|---|---|
| **A** | Top venue, foundational, or frontier lab | NeurIPS / ICML / ICLR / Nature / Science; or a report from DeepMind, OpenAI, Anthropic, Google, Meta FAIR; or the canonical paper for a method |
| **B** | Solid peer-reviewed venue | Reputable journal/conference, well cited for its age |
| **C** | Preprint / blog / unvetted | arXiv with low uptake, blog posts — allowed only when explicitly justified |

Required frontmatter for a paper: `tier`, `venue`, `year`, `authors`, and a citation
estimate (`approx_citations`). No credibility metadata → the note is incomplete.

## Knowledge linking (the point of the brain)

Links are what make this a brain instead of a folder of PDFs. Rules:

- Every new `source` links **≥2 concepts** (existing or newly created) and **≥1 sibling source**.
- Every `concept` links **≥2 sources** in its `## Related`.
- Use **typed links** in `## Related` — state the relationship, don't just drop a wikilink:

```markdown
## Related
- extends [[2018-lopez-scvi]] — scANVI adds semi-supervised labels on top of scVI's latent
- benchmarks [[2020-li-dr-benchmark]] — evaluated head-to-head there
- contradicts [[some-claim]] — reports the opposite result on real data
```

Relationship verbs: `extends`, `contradicts`, `benchmarks`, `supersedes`, `applies`,
`introduces`, `background-for`. Unresolved wikilinks (grey nodes) are fine — they mark
concepts not yet written.

## Directory rules

| Folder | Rule |
|---|---|
| `00-system/` | Contract, domain profile, templates. Edit rarely. |
| `sources/{kind}/` | One note per source, in the subfolder matching `source_kind`. |
| `concepts/` | One idea per note; ≥2 wikilinks in `## Related`. |
| `maps/` | MOC hubs; structure stable, Dataview tables refresh from frontmatter. |
| `sources/raw/` | L0 originals + manifests. Gitignore large binaries. |

Wikilinks to sources use the filename stem only, not the folder path.

## Tag taxonomy (keep it small)

- Kind: `#source`, `#concept`, `#moc`, `#system`
- Domain: `#domain/ml`, `#domain/literature`
- Topic: `topic/…` (e.g. `topic/vae`), Method: `method/…`, Field: `field/…`

Don't invent one-off tags. If a tag needs to exist everywhere, add it to this contract.

## Editing discipline

- Source and concept notes are hand-written — edit them freely, unlike the old engine model.
- Keep one idea per concept note; split when a note starts covering two.
- MOCs' Dataview queries stay generic so they keep working as notes are added.
- Prefer `status: archived` over deleting a linked note.
