---
description: Fix lint errors, type errors, or failing tests
argument-hint: error output, or just run to auto-detect
allowed-tools: Read, Grep, Glob, Bash(npm:*, npx:*, yarn:*, pnpm:*, pip:*, python:*, go:*, cargo:*, make:*, node:*, pytest:*, jest:*, vitest:*, tsc:*, eslint:*, rubocop:*, git diff:*)
---

# Fix Errors

Act as a Principal Engineer. Fix the following errors systematically.

```
$ARGUMENTS
```

## Process

1. **Detect** — If no specific errors are provided, run the project's lint, type check, and test commands to find them
2. **Categorize** — Group errors by type: lint violations, type errors, test failures, build errors
3. **Fix systematically** — Resolve each error with the minimal correct change:
   - **Lint errors**: Fix the actual issue, don't just suppress the rule
   - **Type errors**: Add correct types, fix mismatches — don't use `any` or `as` casts
   - **Test failures**: Fix the code if the test is correct, fix the test if it's outdated
   - **Build errors**: Resolve missing imports, broken references, config issues
4. **Verify** — Re-run the failing commands to confirm all errors are resolved
5. **Stop if cascading** — If a fix introduces new errors, attempt one more fix cycle. After 2 cycles, stop and report what was fixed, what remains, and why.

## When Information is Insufficient

If no error output is provided and auto-detection finds no errors, report "All checks pass — no errors detected" and stop. Do not invent problems.

## Constraints

- Fix the root cause, not the symptom
- Don't introduce new warnings or errors while fixing existing ones
- Don't change unrelated code
- Never suppress a linter rule without a comment explaining why the suppression is necessary
- Max 2 fix-verify cycles — if errors persist, report the situation rather than chasing indefinitely
- If a lint rule is genuinely wrong for a case, disable it inline with a justification comment
