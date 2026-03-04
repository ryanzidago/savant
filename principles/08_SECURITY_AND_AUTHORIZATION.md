# 08 — Security & Authorization

> Are access controls applied at the right layer, inputs sanitized, and tenant boundaries enforced?

## Why

A single authorization gap can expose every customer's data. Security failures are trust-destroying and often irreversible.

## Questions

- Is authorization checked at the data access layer, not just the UI or controller?
- Can a user access or mutate another tenant's data through any path?
- Are inputs validated and sanitized before reaching the database or being rendered?
- Are secrets stored securely and never logged, serialized, or exposed in responses?
- Is authentication state verified on every request, not assumed from a previous check?
- Are destructive or sensitive operations protected by additional confirmation or scoping?
- Has the change been considered from the perspective of a malicious authenticated user?
