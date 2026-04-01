---
description: Generate documentation for code or projects
argument-hint: file path, module, or project directory
allowed-tools: Read, Grep, Glob
---

# Documentation Generator

Generate documentation for:

```
$ARGUMENTS
```

## Process

1. **Read the code** to understand its purpose, public API, and usage patterns
2. **Identify the audience** - Is this for users, contributors, or operators?
3. **Generate appropriate documentation**:
   - **README**: Purpose, quick start, installation, basic usage
   - **API docs**: Function signatures, parameters, return types, examples
   - **Architecture docs**: Component overview, data flow, key decisions
   - **Runbook**: How to deploy, monitor, troubleshoot

## Principles

- Lead with a working example - show, don't just describe
- Document the WHY, not just the WHAT (the code already shows the what)
- Keep it maintainable - don't document things that change frequently without automation
- Assume the reader is a competent engineer who doesn't need hand-holding
