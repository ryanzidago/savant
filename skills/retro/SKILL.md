---
name: retrospective
description: Use after completing a development session — captures what happened, what was learned, and process improvements
---

# Retrospective

Write a timestamped retrospective after completing a development session.

## Instructions

1. Gather context:
   - Current branch name
   - Number of commits in this session (`git log --oneline main..HEAD | wc -l`)
   - Files changed (`git diff --stat main..HEAD`)

2. Write the retrospective to `docs/retrospectives/<YYYYMMDD_HHMMSS>_<slug>.md`.

   The slug should be a short kebab-case summary of the work (e.g. `add-vector-search`, `fix-tenant-scoping`).

3. Use this template:

```markdown
# Retrospective: <short description of the work done>

DateTime: YYYY-MM-DD HH:MM:SS
Branch: <branch name>
Commits: <number of commits in this session>

## What went well
- ...

## What went wrong
- ...

## What I learned
- ...

## What surprised me
- ...

## Process improvements
- ...

## Guardrails to add

For each problem that went wrong, ask: **can a machine catch this next time?**

Not every problem has an automated guardrail. That's fine. The point is to think it through honestly, not to manufacture rules for the sake of it.

If a guardrail fits, pick the right level:

| Tool | Good for | Examples |
|------|----------|----------|
| **Credo check** | Lint-time code style / convention violations | Missing tenant scope, stray `IO.inspect`, raw SQL outside `Repo.query` |
| **ast-grep rule** | Structural code patterns that are always wrong | `Repo.get` without tenant filter, unmatched `Task.async` |
| **Boundary rule** | Architectural dependency violations | LiveView calling Repo directly, context depending on another context's schema |
| **Test** | Behavioral regression for a specific bug | The exact scenario that broke, encoded as a test case |
| **Compiler warning / Dialyzer** | Type-level or unused-code issues | Missing return type, unreachable clause |

For each proposed guardrail, include:
1. **What it prevents** — the specific failure mode
2. **Where it lives** — file path or config location
3. **Sketch** — a brief pseudocode or config snippet

If no guardrail fits, say **"No guardrail — here's why"** and note what _would_ help instead:
- A skill or memory update so the knowledge is available next session
- A documentation improvement
- "This was a one-off judgment call — no rule can encode it"

The honest answer is sometimes "nothing automated would have caught this."

## Self-building software

Propose improvements that make the system better at building itself over time:

### Skill & memory updates
- Should any existing skill be updated based on what was learned?
- Should a new skill be created to encode a recurring workflow?
- Should any memory file be updated with a new pattern or convention?

### Codegen & templates
- Could a Mix task or code generator prevent manual repetition of what was built?
- Would a template or snippet avoid the boilerplate encountered?

### Feedback loops
- Could a test be added that acts as a regression detector for the class of bug found?
- Could a CI check (compiler warning, dialyzer, Credo, ast-grep, boundary) catch this earlier?
- Could an observability improvement (log, metric, trace) make the next diagnosis faster?
```

4. For each item in "What went wrong", consider whether an automated guardrail could prevent it. Add one with a sketch if it fits. If not, say why.

5. For "Self-building software", review existing skills and memory files before proposing updates. Only propose changes that are clearly warranted by the session.

6. Commit the retrospective file.

## Quality Bar

Be honest and specific — vague bullets like "things went smoothly" are useless. Reference concrete files, functions, error messages, or decisions. The value comes from specificity.

Each section should have at least one bullet. If nothing went wrong, you weren't paying attention.

Guardrails must be actionable — "be more careful" is not a guardrail. A Credo check with pseudocode is. But "no guardrail fits — this was a judgment call" is an honest and valid answer. Don't invent rules just to fill the section.
