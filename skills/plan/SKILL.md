---
name: plan
description: Use before implementation to define what to build, why, how it should behave, and what to test — without prescribing implementation details
---

# Plan

Write a behavioral plan that defines what to build and why, without dictating how. The plan feeds into `elixir-dev`, which handles task breakdown and implementation.

**Rigid skill. Follow exactly. No shortcuts.**

## When This Runs

Before any implementation. This is the first skill in the lifecycle:

```
/plan → /elixir-dev → /elixir-test → /qa → /review → /retrospective
```

## Phase 1: Explore

Before writing anything, understand the problem deeply through conversation.

### Step 1: Understand intent

Ask the user **why** they want this, not just **what** they want. One question at a time. Keep going until you can explain the motivation back to them and they confirm you've got it.

Good questions:
- "What problem does this solve for your users?"
- "What happens today without this? What's the pain?"
- "Why is this important now rather than later?"
- "Who benefits from this and how?"

**Gate:** You can articulate the user's intent and motivation in your own words, and they confirm it.

### Step 2: Gather context

Read the relevant parts of the codebase:
- Existing code, schemas, tests related to the area
- Any prior plans or retrospectives that touch this topic
- Current constraints (backwards compatibility, dependencies, deadlines)

### Step 3: Propose approaches

Present **2-3 approaches** with:
- A short description of each
- **Pros** and **cons** for each
- Your **recommendation** and **why** — explain your reasoning clearly

Prefer multiple choice over open-ended questions. One decision at a time. If the user picks a different option than your recommendation, ask why — their reasoning may reveal constraints you missed, or you may surface trade-offs they hadn't considered.

**Gate:** User has chosen an approach (or a hybrid). You both agree on the direction.

### Step 4: Refine details

For the chosen approach, walk through the key design decisions one at a time. For each decision point:
- Present options with pros/cons
- Make a recommendation with reasoning
- Get user alignment

Keep going until there are no more open questions about behavior. It's fine to have open questions about implementation — those belong to `/elixir-dev`.

**Gate:** All behavioral decisions resolved. User is ready to see the written plan.

## Phase 2: Document

Write the plan to `docs/plans/<YYYYMMDD_HHMMSS>_<slug>.md`.

The slug should be a short kebab-case summary (e.g., `add-store-creation`, `fix-tenant-scoping`).

Use this template:

```markdown
# Plan: <short description>

DateTime: YYYY-MM-DD HH:MM:SS

## Problem

What is broken, missing, or insufficient? Why does it matter?
Be specific — reference real user impact, business context, or technical debt.

## Goals

What does success look like? Bullet list of concrete outcomes.
- ...

## Non-goals

What are we explicitly NOT doing? This prevents scope creep.
- ...

## Behavior

How should the system behave once this is done? Describe in plain English from the user's or caller's perspective.

- When <trigger>, <expected outcome>.
- When <edge case>, <expected outcome>.
- When <error condition>, <expected outcome>.

Focus on observable behavior, not internal implementation.

## What to test

Behavioral scenarios that verify the goals are met. Plain English, no code.

- Happy path: ...
- Edge cases: ...
- Error cases: ...
- Authorization: ... (if applicable)

Each scenario should be a sentence a non-engineer could understand.

## Product Engineering Dimensions

Refer to `PRODUCT_ENGINEERING_PRINCIPLES.md` for the full list of 16 dimensions and their definitions.

For each dimension, note what this plan implies. Mark N/A if genuinely irrelevant.

### 1. Organisational Alignment
### 2. Business Logic & Intent
### 3. Testing
### 4. Data Model & Schema Design
### 5. Database Operations & Migrations
### 6. Error Handling & Propagation
### 7. Observability & Debuggability
### 8. Security & Authorization
### 9. Performance & Scalability
### 10. Code Quality & Simplicity
### 11. Maintainability & Changeability
### 12. API Design & Contracts
### 13. UI Quality & Accessibility
### 14. Data Privacy & Compliance
### 15. Reliability & Resilience
### 16. Communication & Rollout

## Open Questions

Unresolved decisions or unknowns that need answers before or during implementation.
- ...
```

## Phase 3: Approve

1. Present the full plan to the user.
2. Walk through each section. The user may push back, ask to revise, or add things.
3. Iterate until the user explicitly approves the plan.

**Gate:** User says the plan is approved. Do not proceed without this.

## Phase 4: Hand off

1. Commit the plan file.
2. Hand off to `/elixir-dev`, which reads the plan and does its own task breakdown.

## Quality Bar

- **Behavior over implementation**: if the plan mentions module names, function signatures, or code structure, it's too low-level. Describe what the system does, not how it's built.
- **Scenarios are sentences**: "When a user creates a store with a duplicate name, they see an error" — not `assert {:error, :name_taken} = Stores.create(attrs)`.
- **Every dimension addressed**: all 16 dimensions must be present. N/A is valid. Skipping one is not.
- **Open questions are honest**: if you don't know something, say so. Don't paper over uncertainty.
- **Non-goals are real**: if you can't name at least one non-goal, you haven't scoped the work.

## Red Flags — STOP

- Jumping to writing the plan without exploring intent first
- Asking multiple questions at once instead of one at a time
- Proposing only one approach with no alternatives
- Making a recommendation without explaining why
- Accepting the user's first statement without asking why it matters
- Writing module names or function signatures in the plan
- Skipping dimensions because "they're obviously fine"
- Empty "What to test" section
- No non-goals listed
- Proceeding to implementation without explicit user approval of the plan
- Copying implementation details from existing code into the plan instead of describing behavior
