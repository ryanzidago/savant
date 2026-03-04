# 11 — Maintainability & Changeability

> Can a future engineer understand and safely modify this without understanding the entire system?

## Why

Code is read and changed far more than it is written. If changing one thing requires understanding everything, velocity dies.

## Questions

- Can this module be understood in isolation, or does it require reading five other files first?
- Are dependencies explicit and injected, or hidden and implicit?
- If a requirement changes, how many files need to be touched?
- Are module boundaries drawn around cohesive domain concepts, not technical layers?
- Is the code structured so that changes are additive rather than requiring modifications to existing paths?
- Are there any time-bombs — hardcoded dates, assumptions about data size, or temporary hacks without tickets?
- Is the coupling between components intentional and minimal?
