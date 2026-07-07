# Finance sources domain profile

`vault_domain: finance-sources`

Use for learning material, market notes, and reference ingest **before** you have
backtest outputs. When backtests exist, add `finance-backtests` profile or emit `type: run`
notes with finance metrics.

## Output folders

`sources/` for ingested learning material, organized by ingest type:

| Subfolder | `source_kind` | Examples |
|-----------|---------------|----------|
| `sources/discussions/` | `discussion` | Cursor chats, podcast distillates |
| `sources/papers/` | `paper` | Campbell ch.21, working papers |
| `sources/articles/` | `article` | Blog posts, news write-ups |
| `sources/courses/` | `course` | Lecture notes, MOOC exports |
| `sources/raw/` | — | L0 PDFs, clips (not markdown notes) |

`runs/` for backtests and strategy runs (when available)

## Filename convention

- Sources: `{date}-{seq}-{slug}.md` under the subfolder matching `source_kind`
  - e.g. `sources/discussions/2026-06-16-001-finance-discussion-macro-spacex-china-fx.md`
- Runs: `2026-06-11-001-momentum-v3`

## Source frontmatter

```yaml
type: source
source_kind: paper              # paper | article | course | book | podcast | discussion
source_path: "sources/raw/campbell-ch21.pdf"
authors: ["Campbell", "Lo", "MacKinlay"]
year: 1997
tags:
  - source
  - domain/finance
  - topic/econometrics
```

## Run frontmatter (when backtests exist)

```yaml
type: run
strategy: "momentum-v3"
metrics:
  sharpe: 1.42
  max_drawdown: -0.08
  total_return: 0.23
hyperparameters:
  lookback_days: 20
  rebalance: "weekly"
dataset_hash: "sha256:…"        # price panel snapshot
tags:
  - run
  - domain/finance
  - strategy/momentum
```

## Ingest pipeline

1. Drop PDF/URL reference in `sources/raw/` (gitignore large files if needed)
2. Run `/log-source` skill → structured note under `sources/{kind}/`
3. Run `/distill-concepts` → `concepts/*.md` clustered by topic
4. When backtests land, engine emits `runs/*.md` with `parent_id` lineage

## Tag conventions

| Tag prefix | Example |
|---|---|
| `topic/` | `topic/options`, `topic/momentum` |
| `strategy/` | `strategy/mean-reversion` |
| `market/` | `market/equities`, `market/fx` |

## L0 artifacts

- Raw PDFs, exported HTML, course slides under `sources/raw/`
- Backtest output folders, trade logs, config YAML (for runs)
