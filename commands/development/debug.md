---
description: Systematic root cause analysis and debugging
argument-hint: error message, stack trace, or description of the bug
allowed-tools: Read, Grep, Glob, Bash
---

# Debug

Diagnose the following issue systematically:

```
$ARGUMENTS
```

## Process

1. **Reproduce** - Identify exact conditions that trigger the bug
2. **Isolate** - Narrow down to the specific component/line causing the failure
3. **Root cause** - Determine WHY the bug exists, not just WHERE
4. **Fix** - Provide the minimal correct fix
5. **Verify** - Suggest how to confirm the fix works and doesn't regress

## Output

- **Root cause**: Clear explanation of why this happens
- **Fix**: Specific code changes with reasoning
- **Test**: How to verify the fix
- **Prevention**: What would have caught this earlier (test, lint rule, type, etc.)
