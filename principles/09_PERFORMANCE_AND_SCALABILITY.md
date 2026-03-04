# 09 — Performance & Scalability

> Will this hold up under production load — bounded operations, efficient renders, no unnecessary work in the hot path?

## Why

Performance problems are architecture problems discovered too late. An unbounded query that works on 100 rows will take down production at 100k.

## Questions

- Are all operations bounded — no unbounded lists, no full-table scans on large tables?
- Is work being done eagerly that could be deferred, batched, or cached?
- Are database queries efficient under realistic data volumes, not just dev fixtures?
- Is the hot path free of unnecessary computation, serialization, or I/O?
- Are LiveView or React renders efficient — no redundant re-renders or excessive DOM diffing?
- Has the change been considered under 10x current load?
- Are pagination, rate limiting, or timeouts in place where needed?
