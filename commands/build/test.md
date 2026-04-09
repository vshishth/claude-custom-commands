---
description: Generate tests for code with meaningful coverage
argument-hint: file path or paste code to test
allowed-tools: Read, Grep, Glob, Bash(npm:*, npx:*, yarn:*, pnpm:*, pip:*, python:*, go:*, cargo:*, make:*, node:*, pytest:*, jest:*, vitest:*, tsc:*, git diff:*)
---

# Test Generator

Act as a Principal Engineer. Generate meaningful, maintainable tests.

```
$ARGUMENTS
```

## Approach

1. **Identify** the public interface and key behaviors to test
2. **Detect** the testing framework already in use and follow existing test conventions (naming, file location, fixture patterns)
3. **Generate tests** in this priority order:
   - Happy path for each public function/method
   - Edge cases (empty inputs, boundaries, nulls, large inputs)
   - Error cases (invalid inputs, failure modes, exceptions)
   - Integration points (if the code interacts with external systems)
4. **Follow conventions** — Use the project's existing test naming pattern. If none exists, use: `describe('ComponentName', () => { it('should [expected behavior] when [condition]') })`
5. **Run tests** — Execute the generated tests to verify they pass. Fix any failures.

## When Information is Insufficient

If no testing framework is detected, recommend one appropriate for the language/framework and ask the user to confirm before generating tests. If the code has no clear public API (e.g., scripts, middleware), test the observable side effects.

## Output

- Test file(s) placed in the project's conventional test location
- Each test with a descriptive name that explains the expected behavior
- All tests passing when run

## Constraints

- Test behavior, not implementation details — tests should survive refactors
- Each test should have a single clear assertion and a descriptive name
- Use the Arrange-Act-Assert pattern
- Mock external dependencies, not internal logic
- Avoid testing private methods directly — test through the public API
- Avoid flaky patterns: no `sleep()`, no reliance on execution order, no shared mutable state between tests
- Test file location must match the project's convention (co-located, `__tests__/`, `test/`, etc.)
- Include both positive and negative test cases
