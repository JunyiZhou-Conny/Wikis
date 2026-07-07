---
name: ingest-paper
description: Ingest a paper (URL, DOI, arXiv id, or PDF) into the wiki as a credibility-tiered, linked source note. Use when the user wants to add a paper, log a source, or save research to the wiki.
disable-model-invocation: true
---

# Ingest paper

Turn a paper reference into a `sources/papers/` note that clears the credibility bar and is
linked into the graph. Follow every step — the value is in the gating and linking, not just
saving text.

**Vault root:** paths below are relative to the active wiki's vault root, declared in that
wiki's `AGENTS.md` (e.g. `autoencoder_wiki/docs/`). Work inside the wiki the user is asking about.

## Workflow

```
- [ ] 1. Resolve the reference (fetch metadata + abstract)
- [ ] 2. Assign a credibility tier; stop if it fails the bar
- [ ] 3. Check for duplicates already in sources/
- [ ] 4. Write the source note from the template
- [ ] 5. Link it (≥2 concepts, ≥1 sibling source), spawning concepts if needed
- [ ] 6. Report what was added and the links created
```

### 1. Resolve

From a URL / DOI / arXiv id, gather: title, authors, year, venue, abstract, and a citation
estimate. Use web fetch/search for metadata (Semantic Scholar, arXiv, the venue page). If the
user gives a local PDF, read it. Metadata gathering is the *only* allowed web use — a note's
claims must come from the paper, not the web.

### 2. Tier (gate) — see `.cursor/rules/wiki-standard.mdc`

- **A**: top venue (NeurIPS/ICML/ICLR/Nature/Science) OR frontier lab (DeepMind/OpenAI/Anthropic/Google/Meta FAIR) OR canonical paper for a method.
- **B**: solid peer-reviewed, reasonably cited for its age.
- **C**: preprint/blog/unvetted.

If it's tier C, **stop and ask** whether to proceed unless the user already said so.

### 3. Dedupe

Search `docs/sources/` for the title/authors. If it exists, update that note instead of
creating a duplicate.

### 4. Write

Copy `docs/00-system/templates/source-note.md` to
`docs/sources/papers/{year}-{firstauthor}-{short-slug}.md`. Fill `tier`, `venue`, `year`,
`authors`, `approx_citations`, `doi`. Write `## Summary`, `## Key claims / results`,
`## Methodology` from the actual paper. Keep it tight — this is a distillate, not a copy.

### 5. Link (the important part)

- Find ≥1 sibling source already in the wiki (search `sources/` by topic/method) and link it with a typed verb.
- Link ≥2 concepts. If a needed concept doesn't exist, either create it now (see the `distill-concepts` skill) or leave a grey wikilink and note it.
- Add the paper to the relevant topic MOC in `docs/maps/`.

### 6. Report

State: file path, assigned tier (with reasoning), and the typed links you created. If it was
tier C or you left grey links, say so explicitly.

## Do not

- Do not commit to git (unless invoked by the `daily-paper` automation).
- Do not fabricate citation counts or venues — if unknown, say "unknown" and lower confidence.
