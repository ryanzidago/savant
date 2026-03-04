# 05 — Database Operations & Migrations

> Are migrations safe against production data, and are queries performant?

## Why

A bad migration can lock tables, corrupt data, or take down production. These are the hardest changes to undo.

## Questions

- Is this migration safe to run on a live database with concurrent traffic?
- Does the migration lock tables, and if so, for how long and with what impact?
- Are new indexes added concurrently where the table is large?
- Is backfilling handled separately from the schema change?
- Are queries using indexes effectively, or will they result in sequential scans?
- Have N+1 queries been avoided through preloading or batching?
- Is the migration reversible, and has the rollback path been considered?
