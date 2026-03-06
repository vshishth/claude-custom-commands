---
description: Generate tests for code with meaningful coverage
argument-hint: file path or paste code to test
allowed-tools: Read, Grep, Glob, Bash
---

# Test Generator

Generate tests for the following code:

```
$ARGUMENTS
```

## Approach

1. **Identify** the public interface and key behaviors to test
2. **Detect** the testing framework already in use (or recommend one if none exists)
3. **Generate tests** in this priority order:
   - Happy path for each public function/method
   - Edge cases (empty inputs, boundaries, nulls, large inputs)
   - Error cases (invalid inputs, failure modes, exceptions)
   - Integration points (if the code interacts with external systems)

## Principles

- Test behavior, not implementation details
- Each test should have a single clear assertion and a descriptive name
- Use the Arrange-Act-Assert pattern
- Mock external dependencies, not internal logic
- Avoid testing private methods directly - test through the public API
- Include both positive and negative test cases
