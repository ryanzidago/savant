# 04 — Data Model & Schema Design

> Does the schema faithfully represent the domain, with constraints enforced at the database level?

## Why

The schema outlives every other layer. A permissive schema lets invalid data in; fixing it later means migrating every row.

## Questions

- Does the schema model the domain accurately, or is it shaped by UI or API convenience?
- Are constraints (NOT NULL, uniqueness, foreign keys, check constraints) enforced at the database level?
- Can the schema represent an invalid state, or does the structure prevent it?
- Are nullable columns intentionally nullable, or just defaulting to permissive?
- Is the naming consistent and domain-aligned across tables and columns?
- Are relationships modelled correctly (1:1, 1:N, M:N) with appropriate join strategies?
- Will this schema be painful to migrate away from as the domain evolves?
