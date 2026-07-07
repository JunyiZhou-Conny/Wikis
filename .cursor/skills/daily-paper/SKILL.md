---
name: daily-paper
description: Scheduled daily job — find one top-tier paper on a wiki topic that isn't already in the vault (alternating classic and frontier-lab picks), ingest it, link it, commit, and push. Use when running the daily paper automation or when the user asks to auto-add today's paper.
disable-model-invocation: true
---

# Daily paper

Grow the wiki by one high-quality paper per run, unattended. This skill **is pre-authorized to
commit and push** per `AGENTS.md` — it is the only skill allowed to.

**Which wiki:** default to `autoencoder_wiki` unless the run says otherwise. Let `WIKI` be that
folder and `VAULT = <WIKI>/docs` (the vault root from the wiki's `AGENTS.md`). All paths below
are under `VAULT`.

## Workflow

```
- [ ] 1. Decide today's mode (classic vs frontier) + pick a topic gap
- [ ] 2. Search for a candidate top-tier paper NOT already in the wiki
- [ ] 3. Apply the credibility gate (tier A preferred, B acceptable)
- [ ] 4. Ingest via the ingest-paper flow (write + link)
- [ ] 5. git add + commit + push the new note(s)
- [ ] 6. Print a one-line summary of what was added
```

### 1. Mode + topic gap

**Alternate the taste each run** between two modes:

- **classic** — foundational / canonical / highly-cited papers that anchor the field.
- **frontier** — recent work from top labs (DeepMind, OpenAI, Anthropic, Google, Meta FAIR) or
  the last ~2 years of top venues.

Pick today's mode as the **opposite of the last daily-paper commit**:

```bash
git log --grep="^daily-paper:" -1 --format=%s
```

If the last such commit ends with `[frontier]`, use **classic** today; if `[classic]` (or no
prior daily-paper commit), use **frontier**. Then read `docs/maps/` MOCs and the `topic/*` tags
across `docs/sources/` and pick a topic gap that fits today's mode — a thinly covered core topic,
or a natural next paper on a well-covered thread (follow-up, benchmark, competing method).

### 2. Search

Search for influential papers on that topic in today's mode (Semantic Scholar, arXiv, venue
proceedings, lab blogs). **Dedupe** against `docs/sources/` — never re-add an existing paper.

### 3. Gate

Only tier **A** or **B** (see `.cursor/rules/wiki-standard.mdc`). If nothing clears the bar
today, **add nothing and commit nothing** — print "no qualifying paper found" and stop. Quality
over cadence.

### 4. Ingest

Follow the `ingest-paper` skill: write `<VAULT>/sources/papers/{year}-{author}-{slug}.md`
with full credibility frontmatter, distill summary/claims/method, link ≥2 concepts and ≥1
sibling source, and update the topic MOC.

### 5. Commit + push

End the commit subject with today's mode tag so the next run can alternate:

```bash
git add <WIKI>/docs/
git commit -m "daily-paper: add {title} ({tier}, {venue} {year}) [{mode}]"
git push
```

Commit only files under the wiki's `docs/` — never anything else. Push is pre-authorized for
this skill per `AGENTS.md`. On a cloud automation run the agent works on its own branch, so the
push opens the change as a branch/PR for review rather than landing on `main` directly.

### 6. Summary

One line: title, tier, venue/year, and the links created — so the morning review is a glance.
