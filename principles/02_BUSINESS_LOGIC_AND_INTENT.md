# 02 — Business Logic & Intent

> Does the work solve the right problem, and is the intent explicit and traceable?

## Why

Implicit business rules become tribal knowledge. When intent is scattered or undocumented, every change is a gamble.

## Questions

- Is the business rule expressed explicitly in code, or is it implicit and scattered?
- Can someone reading this code understand *why* this logic exists without external context?
- Are edge cases in the business domain accounted for, or just the happy path?
- Is the logic tested at the level where the business rule lives, not just at the UI or API layer?
- If this rule changes tomorrow, is there one place to update it?
- Are domain terms used consistently between code, UI, and documentation?
- Is the intent traceable back to a ticket, spec, or conversation?
