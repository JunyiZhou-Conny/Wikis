---
name: daily-paper
description: Scheduled daily job — find one top-tier paper on a wiki topic that isn't already in the vault, ingest it, link it, and commit. Use when running the daily paper automation or when the user asks to auto-add today's paper.
disable-model-invocation: true
---

# Daily paper

Grow the wiki by one high-quality paper per run, unattended. This skill **is pre-authorized to
commit** per `AGENTS.md` — it is the only skill allowed to.

**Which wiki:** default to `autoencoder_wiki` unless the run says otherwise. Let `WIKI` be that
folder and `VAULT = <WIKI>/docs` (the vault root from the wiki's `AGENTS.md`). All paths below
are under `VAULT`.

## Workflow

```
- [ ] 1. Pick a topic gap
- [ ] 2. Search for a candidate top-tier paper NOT already in the wiki
- [ ] 3. Apply the credibility gate (tier A preferred, B acceptable)
- [ ] 4. Ingest via the ingest-paper flow (write + link)
- [ ] 5. git add + commit the new note(s)
- [ ] 6. Print a one-line summary of what was added
```

### 1. Topic gap

Read `docs/maps/` MOCs and the `topic/*` tags across `docs/sources/`. Pick a topic that is
core to the wiki but thinly covered, or extend a well-covered thread with a natural next paper
(a follow-up, a benchmark, a competing method).

### 2. Search

Search for influential papers on that topic (Semantic Scholar, arXiv, venue proceedings, lab
blogs). Prefer highly-cited or foundational work and recent frontier-lab releases. **Dedupe**
against `docs/sources/` — never re-add an existing paper.

### 3. Gate

Only tier **A** or **B** (see `.cursor/rules/wiki-standard.mdc`). If nothing clears the bar
today, **add nothing and commit nothing** — print "no qualifying paper found" and stop. Quality
over cadence.

### 4. Ingest

Follow the `ingest-paper` skill: write `<VAULT>/sources/papers/{year}-{author}-{slug}.md`
with full credibility frontmatter, distill summary/claims/method, link ≥2 concepts and ≥1
sibling source, and update the topic MOC.

### 5. Commit

```bash
git add <WIKI>/docs/
git commit -m "daily-paper: add {title} ({tier}, {venue} {year})"
```

Commit only files under the wiki's `docs/` — never anything else.

- **Local / manual run:** commit only, do **not** push. The user reviews and pushes.
- **Cloud automation run:** the cloud agent works on its own branch — commit, then let the
  automation push that branch as usual so the change is visible for review.

### 6. Summary

One line: title, tier, venue/year, and the links created — so the morning review is a glance.
