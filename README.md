# wikis

Personal wiki projects — **sibling repos**, each with its own `AGENTS.md`, `README.md`, and vault folder.

| Wiki | Obsidian vault path | Topic |
|------|---------------------|-------|
| [finance_wiki](./finance_wiki/) | `finance_wiki/Finance-Wiki/` | Macro, markets, China FX, IPO |
| [autoencoder_wiki](./autoencoder_wiki/) | `autoencoder_wiki/docs/` | Autoencoders & ML |
| [ml-hardware_wiki](./ml-hardware_wiki/) | `ml-hardware_wiki/docs/` | CPU, GPU, model training |

## Shared tooling (`.cursor/`)

One rule + four skills, shared by every wiki here:

| Skill | What it does |
|---|---|
| `ingest-paper` | Add a paper (URL/DOI/arXiv/PDF) → credibility-tiered, linked source note |
| `distill-concepts` | Turn sources into atomic concept notes that connect papers |
| `link-audit` | Find orphans / thin links / missing tiers, propose typed edges |
| `daily-paper` | Scheduled: add one top-tier paper on a wiki topic, then commit |

The rule `wiki-standard.mdc` (always on) enforces credibility tiers and typed linking.

**Scaffold baseline:** `../wiki_scaffold/` (v0.1.1+ — sources under `sources/{kind}/`)

## Add another wiki

```bash
./../wiki_scaffold/scripts/init-vault.sh /Users/conny/Desktop/wikis/<name>_wiki
# Edit AGENTS.md, rename maps, start adding concepts/
```

Then add a row to this README.
