---
name: elixir-test
description: Use when writing, reviewing, or modifying tests in an Elixir codebase — covers self-contained test design, test pyramid discipline, and efficient test execution
---

# Writing Elixir Tests

Tests are **self-contained, readable top-to-bottom, and easy to delete**. No shared setup blocks. Each test tells its own complete story.

**Rigid skill. Follow exactly. No shortcuts.**

## The Test Pyramid

Follow the [Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html). Write many fast unit tests, some integration tests, very few end-to-end tests.

| Level | What to test | Volume | Speed |
|-------|-------------|--------|-------|
| **Unit** | Pure functions, domain logic, data transformations | Many | Fast |
| **Integration** | DB queries, external service boundaries, Ecto changesets, context modules | Some | Medium |
| **End-to-end** | Critical user journeys (LiveView / controller tests) | Few | Slow |

**Push tests down.** If you can test it with a unit test, don't write an integration test. If you can test it with an integration test, don't write an end-to-end test.

**Don't test trivial code.** No tests for getters, simple struct access, or code that just delegates.

## Running Tests — Fail Fast, Minimal Output

Always use flags to fail fast and suppress noise.

**Run a single test by line number (during RED/GREEN):**
```bash
mix test test/path/to/module_test.exs:LINE --max-failures 1 --no-all-warnings
```

**Run stale tests (after implementation changes):**
```bash
mix test --stale --max-failures 1 --no-all-warnings
```

**Retry only previously failed tests:**
```bash
mix test --failed --no-all-warnings
```

**Final full suite (before committing):**
```bash
mix test
```

**Never** run `mix test` without flags during development — it floods the context window with noise. Only run the bare `mix test` as a final verification.

## No `setup` Blocks

`setup` and `setup_all` are **forbidden**. Each test sets up its own data inline or via private helper functions defined in the same module.

Why:
- Tests are self-contained — read one test, understand everything
- No hidden state from distant setup blocks
- Tests can be deleted without breaking siblings
- No cascading failures from shared setup
- No complexity pushed to a higher-level abstraction

**Only exception:** `setup :verify_on_exit!` (Mox pattern)

### Use private helpers instead

```elixir
describe "activate/1" do
  test "activates an inactive account" do
    account = build_inactive_account()
    assert {:ok, %{active: true}} = Accounts.activate(account)
  end

  test "returns error for already active account" do
    account = build_active_account()
    assert {:error, :already_active} = Accounts.activate(account)
  end
end

defp build_inactive_account do
  %Account{id: 1, active: false, email: "test@example.com"}
end

defp build_active_account do
  %Account{id: 2, active: true, email: "active@example.com"}
end
```

## Module Template

```elixir
defmodule MyApp.YourModuleTest do
  use ExUnit.Case, async: true

  describe "function_name/1" do
    test "describes the expected outcome" do
      # arrange — build test data inline or via private helper
      input = build_input()

      # act
      result = YourModule.function_name(input)

      # assert
      assert result == expected
    end
  end

  # Private helpers at the bottom of the module
  defp build_input do
    %{key: "value"}
  end
end
```

## Choosing a Test Case

| Case | When | Async |
|------|------|-------|
| `use ExUnit.Case, async: true` | Pure logic, no DB, no web | `true` |
| `use MyApp.DataCase, async: true` | Ecto / DB access | `true` |
| `use MyAppWeb.ConnCase, async: true` | Controller / LiveView tests | `true` |

Always pass `async:` explicitly.

## Test Descriptions

- Group with `describe "function_name/arity"`
- Plain English outcomes — **never** prefix with "should"
- One condition per test

```elixir
# Good
test "returns merged data keyed by name" do
test "excludes system schemas" do
test "returns error when input is empty" do

# Bad
test "should return merged data" do
test "test that it works" do
```

## Data Setup

No factory libraries unless the project already uses one. Create data inline:

- Structs and maps built directly
- Ecto changesets/inserts for integration tests
- Private helper functions for repeated patterns within the same test module
- `on_exit/1` inside helpers for cleanup when needed

## LiveView / Controller Testing

- Use `Phoenix.LiveViewTest` and standard test helpers
- Use `render_submit/2`, `render_change/2` for forms
- Use `element/2`, `has_element?/2` — **never** test raw HTML strings
- Focus on testing user-visible outcomes, not implementation details
- Keep these tests few — most logic should be tested at lower levels

## Quick Reference

```
1. Pyramid:  Unit (many) → Integration (some) → E2E (few)
2. Case:     use ExUnit.Case, async: true  (or DataCase / ConnCase)
3. Group:    describe "function/arity" do
4. Name:     test "expected outcome in plain English" do
5. Setup:    inline or private helper — NO setup blocks
6. Run one:  mix test test/path_test.exs:LINE --max-failures 1 --no-all-warnings
8. Run stale: mix test --stale --max-failures 1 --no-all-warnings
9. Retry:    mix test --failed --no-all-warnings
10. Final:   mix test (full suite, before commit)
```
