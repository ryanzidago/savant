# 12 — API Design & Contracts

> Are interfaces well-defined, consistent, and backward-compatible — both external and internal?

## Why

APIs are promises. Breaking a contract breaks every consumer silently. Good boundaries make independent evolution possible.

## Questions

- Is the API shaped around the consumer's needs, or leaking internal implementation details?
- Are request and response shapes consistent with existing API conventions?
- Is the contract versioned or designed so it can evolve without breaking existing clients?
- Are error responses structured, consistent, and informative?
- Are internal module boundaries treated as contracts — with clear inputs, outputs, and expectations?
- Is the API idempotent where it should be?
- Are optional fields, defaults, and nullability intentional and documented?
