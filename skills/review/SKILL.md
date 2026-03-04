---
name: review
description: Evaluate a change against all 16 product engineering principles. Use when reviewing a diff, PR, spec, design document, or any proposed change.
---

Evaluate a change against all 16 product engineering principles.

## Instructions

1. Determine the input:
   - If a diff or staged changes: gather via `git diff`
   - If a PR: gather diff and description via `gh pr view` and `gh pr diff`
   - If a spec or design doc: read the file provided
   - If unclear: ask what should be reviewed

2. Dispatch to all 16 principle agents in parallel, passing each the same input:
   - `01-organisational-alignment`
   - `02-business-logic-and-intent`
   - `03-testing`
   - `04-data-model-and-schema-design`
   - `05-database-operations-and-migrations`
   - `06-error-handling-and-propagation`
   - `07-observability-and-debuggability`
   - `08-security-and-authorization`
   - `09-performance-and-scalability`
   - `10-code-quality-and-simplicity`
   - `11-maintainability-and-changeability`
   - `12-api-design-and-contracts`
   - `13-ui-quality-and-accessibility`
   - `14-data-privacy-and-compliance`
   - `15-reliability-and-resilience`
   - `16-communication-and-rollout`

3. Each agent loads its corresponding principle from `principles/` and evaluates the input against its questions.

4. Collect all results and merge into a single report, preserving principle order (01–16). Omit principles with no findings.

## Output Format

Number each finding using `<principle-number>.<finding-sequence>` where principle-number is the principle's own number (01–16) and finding-sequence is the ordinal position within that principle (1, 2, 3, ...).

```
# Principle Review

## 03 — Testing

3.1 **Question**: Are sad paths and boundary conditions tested?
    **Evidence**: `user_controller.ex` — no test for invalid email format
    **Suggestion**: Add a test case for malformed email input

3.2 **Question**: Is the refactored filter behavior verified?
    **Evidence**: Changed from `Enum.map` + `Enum.reject` to `Enum.flat_map` but no test confirms filtering.
    **Suggestion**: Add a test confirming empty messages are omitted from output.

## 08 — Security & Authorization

8.1 **Question**: Is authorization checked at the data access layer?
    **Evidence**: `update/2` in `post_controller.ex` checks ownership in the controller but not in the context function
    **Suggestion**: Move the ownership check into `Posts.update_post/2`

---

**Summary**: X findings across Y principles. No issues in the remaining Z principles.
```
