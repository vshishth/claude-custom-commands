---
description: Generate documentation for code or projects
argument-hint: file path, module, or project directory
allowed-tools: Read, Grep, Glob
---

# Documentation Generator

Act as a Principal Engineer. Generate clear, maintainable documentation.

```
$ARGUMENTS
```

## Process

1. **Read the code** to understand its purpose, public API, and usage patterns
2. **Identify the audience** — Is this for users, contributors, or operators?
3. **Generate appropriate documentation**:
   - **README**: Purpose, quick start, installation, basic usage, configuration
   - **API docs**: Function signatures, parameters, return types, examples
   - **Architecture docs**: Component overview, data flow, key decisions
   - **Runbook**: How to deploy, monitor, troubleshoot common issues
4. **Freshness strategy** — For each doc section, note whether it can be auto-generated (from code, schemas, types) vs must be manually maintained. Prefer auto-generation to prevent drift.

## When Information is Insufficient

If no specific module is targeted, generate a project-level README. If a README already exists, improve it rather than replacing it — preserve existing content that is still accurate. If the codebase lacks comments, infer purpose from function names, tests, and usage patterns.

## Output

Documentation in markdown format, appropriate for the identified audience. Every code example must be runnable — no pseudocode.

## Constraints

- Lead with a working example — show, don't just describe
- Document the WHY, not just the WHAT (the code already shows the what)
- Keep it maintainable — prefer auto-generated docs (JSDoc/pydoc/rustdoc) over separate files that will drift
- Assume the reader is a competent engineer who doesn't need hand-holding
- Every code example MUST be runnable and tested against the current codebase
- Improve existing docs rather than replacing them — preserve accurate content
