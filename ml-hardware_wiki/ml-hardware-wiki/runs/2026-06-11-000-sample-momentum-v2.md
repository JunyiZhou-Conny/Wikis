---
id: "2026-06-11-000-sample-momentum-v2"
type: run
status: done
date: 2026-06-11
parent_id: "2026-06-10-000-sample-momentum-v1"
strategy: "momentum-v2"
engine: "wiki-scaffold-example"
regenerate_cmd: "see examples/sample-run-note.md"
git_commit: "0000000"
metrics:
  sharpe: 1.31
  max_drawdown: -0.11
  total_return: 0.18
hyperparameters:
  lookback_days: 60
  rebalance: "weekly"
tags:
  - run
  - domain/finance
  - strategy/momentum
---

# Sample momentum v2 — scaffold validation run

**Status** `done` · **Parent:** [[2026-06-10-000-sample-momentum-v1]] · **Concepts:**
[[momentum factor decay]] · [[volatility scaling]]

> This note validates Dataview queries on [[Runs MOC]]. Delete or overwrite when your
> real engine emits runs.

## Headline metrics

| Metric | Value |
|---|---|
| Sharpe | 1.31 |
| Max drawdown | -11% |
| Total return | 18% |

## What changed

Reduced lookback from 90 to 60 days; added volatility scaling on position sizes.
Example narrative — real notes come from your engine + agent synthesis.

## On-disk references

- `examples/backtests/sample-config.yaml` (fictional)

---
See also: [[Runs MOC]] · [[Home MOC]]
