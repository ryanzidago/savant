# 03 — Testing

> Is there proof the system behaves as intended — across happy paths, sad paths, and edge cases?

## Why

Tests are the only proof that the system works. Without them, confidence comes from hope.

## Questions

- Does the test prove the behaviour, or just exercise the code?
- Are the critical business rules covered by tests that would fail if the rule broke?
- Are sad paths and boundary conditions tested, not just the golden path?
- Are tests isolated from each other, or do they depend on shared state or ordering?
- Is the test readable — can someone understand the intent without reading the implementation?
- Are we testing at the right level (unit, integration, end-to-end) for what we're verifying?
- Would a subtle regression in this area be caught before it reaches production?
