---
description: Template for creating new Claude commands
---

# Command Template

## Structure

```markdown
---
description: One-line description of what this command does
argument-hint: what input to provide
allowed-tools: Read, Grep, Glob, Bash(specific:patterns)
---

# Command Name

[Brief framing of what you want Claude to do]

\```
$ARGUMENTS
\```

## Process

1. **Step 1** - What to analyze or do first
2. **Step 2** - Next action
3. **Step 3** - Final action

## Output

Describe the expected output format.

## Principles

- Key constraint or quality bar
- Another constraint
```

## Tips

- Keep commands under 50 lines - Claude already knows how to do most things; you're setting focus and format
- Use `allowed-tools` to limit scope and prevent unintended side effects
- Use `!` backtick syntax for dynamic context (e.g., !`git status`)
- Focus on WHAT and WHY, not exhaustive HOW - trust the model
- One command, one purpose
