---
name: elixir-qa
description: Use after implementation is complete to QA a feature through iex scenarios and optionally through the browser via Playwright MCP
---

# Elixir QA

Two-track QA verification: iex scenarios (always) and browser flows (when Playwright MCP is available and the feature touches UI).

**Rigid skill. Follow exactly. No shortcuts.**

## When This Runs

Called by `elixir-dev` after `mix precommit` passes, before `/review`. Can also be invoked standalone with `/qa`.

```
... all tasks done → mix precommit → /qa → /review → /retrospective
```

## Step 0: Gather Context

Before generating scenarios, understand what was built:

1. Review the commits from this session (`git log --oneline main..HEAD`)
2. Identify the public functions that were added or changed
3. Identify whether the feature touches UI (LiveView, controllers, templates)

## Track 1 — iex Scenarios (always runs)

### Phase 1: Generate Scenarios

Based on the implemented code, generate a scenario list. Each scenario has:
- **Description**: what is being verified (plain English)
- **Command**: the exact iex expression to run
- **Expected**: the expected output shape or value

Cover these categories:
- **Happy path**: normal usage with valid inputs
- **Edge cases**: empty inputs, boundary values, large inputs
- **Error cases**: invalid inputs, missing required fields, constraint violations

Create a `TaskCreate` for each scenario with:
- **subject**: imperative form (e.g., "Verify user creation with valid attrs")
- **description**: the iex command and expected output
- **activeForm**: present continuous (e.g., "Verifying user creation with valid attrs")

**Gate:** All scenarios generated and created as tasks before executing any.

### Phase 2: Execute Scenarios

Start an interactive session:
```bash
iex -S mix
```

If `iex -S mix` fails to start (compilation error, missing dependency), **STOP** and report the error. Do not attempt to run scenarios against a broken build.

For each scenario (in task order):

1. `TaskUpdate` — mark task `in_progress`
2. Run the iex command
3. Compare actual output to expected output shape
4. If it matches: `TaskUpdate` — mark task `completed`
5. If it does NOT match: **STOP**. Report:
   - Which scenario failed
   - The iex command that was run
   - Expected output
   - Actual output
   - Do NOT proceed to Track 2 or `/review`

**Gate:** All iex scenarios pass.

## Track 2 — Browser Flows (conditional)

### Detection

Check if Playwright MCP tools (e.g., `browser_navigate`, `browser_click`) are available in your tool list. If they are not available, print:

```
Playwright MCP not available — skipping browser QA.
```

Then skip to the Summary.

### Applicability

Even if Playwright is available, only run browser QA if the feature touches UI. If commits only changed backend code (contexts, schemas, non-web modules), print:

```
No UI changes detected — skipping browser QA.
```

Then skip to the Summary.

### Phase 3: Generate User Flows

Based on the implemented feature, generate user flow scenarios. Each flow has:
- **Description**: what user journey is being verified
- **Steps**: ordered list of actions (navigate, fill, click, verify)
- **Expected outcome**: what the user should see at the end

Cover these categories:
- **Happy path**: complete the main user journey successfully
- **Validation errors**: submit with invalid/missing data, verify error messages
- **Edge cases**: unusual but valid inputs, rapid actions

Create a `TaskCreate` for each flow.

**Gate:** All flows generated and created as tasks before executing any.

### Phase 4: Execute User Flows

Ensure the Phoenix server is running. Check if it's already running first; start it only if needed:
```bash
mix phx.server
```

For each flow (in task order):

1. `TaskUpdate` — mark task `in_progress`
2. Execute each step using Playwright MCP tools:
   - `browser_navigate` to go to URLs
   - `browser_type` to fill form fields
   - `browser_click` to click buttons/links
   - `browser_snapshot` to read page state and verify content
3. After each step, verify the expected outcome
4. If all steps pass: `TaskUpdate` — mark task `completed`
5. If any step fails: **STOP**. Report:
   - Which flow failed
   - Which step within the flow
   - What was expected vs what actually happened
   - Do NOT proceed to `/review`

**Gate:** All browser flows pass.

## Summary

After both tracks complete (or Track 2 is skipped), print a summary:

```
QA Summary
──────────
iex scenarios:     X/X passed
Browser flows:     Y/Y passed (or "skipped — Playwright not available" or "skipped — no UI changes")
──────────
Result: PASS
```

If everything passed, control returns to elixir-dev which proceeds to `/review`.

## Red Flags — STOP

- Skipping iex scenarios because "the tests already cover it"
- Generating only happy path scenarios (always include error + edge cases)
- Proceeding to browser QA when iex scenarios failed
- Proceeding to /review when any QA scenario failed
- Not verifying actual output against expected — just running commands without checking
- Generating scenarios that don't match the actual implemented code
