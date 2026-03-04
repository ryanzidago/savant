# 15 — Reliability & Resilience

> Can the system handle partial failures gracefully — with retry safety, idempotency, and no silent data loss?

## Why

Partial failures are inevitable. Systems that aren't designed for them turn small outages into total ones.

## Questions

- If an external dependency fails, does the system degrade gracefully or crash entirely?
- Are operations idempotent where they need to be — safe to retry without side effects?
- Is there a risk of silent data loss if a process crashes mid-operation?
- Are timeouts configured for external calls, or can a hung dependency block the system?
- Are distributed operations (multi-step workflows, async jobs) designed to resume or compensate on failure?
- Is there a circuit breaker or backoff strategy for flaky dependencies?
- Has the failure mode been tested, not just the success path?
