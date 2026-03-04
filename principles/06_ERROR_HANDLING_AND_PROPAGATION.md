# 06 — Error Handling & Propagation

> Are errors explicit, propagated to the right boundary, and translated into something meaningful?

## Why

Silent failures corrupt data and erode trust. You find them last, and they cost the most.

## Questions

- Is every failure mode accounted for, or are there silent swallows?
- Are errors translated at module boundaries into domain-meaningful terms?
- Does the caller get enough context to act on the error?
- Are retryable vs. fatal errors distinguishable?
- Is the user shown something actionable, or a generic 500?
- Are errors logged with enough context to diagnose without reproducing?
- Are external service failures handled gracefully without cascading?
