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

Act as a Principal Engineer. [Brief framing of what you want Claude to do]

[Dynamic context blocks with !`...`]

\```
$ARGUMENTS
\```

## Process

1. **Step 1** - What to analyze or do first
2. **Step 2** - Next action
3. **Step 3** - Final action

## When Information is Insufficient

Describe what to do when inputs are ambiguous, incomplete, or missing.
Example: "If X is not provided, ask the user. If Y is unclear, default to Z."

## Output

Describe the expected output format with mandatory fields.
Every finding MUST include a concrete, actionable fix — never generic advice.

## Constraints

- Hard rule that MUST or MUST NOT be followed
- Another hard constraint
- Safety guard if command modifies state
```

## Tips

- Keep commands under 65 lines — Claude already knows how to do most things; you're setting focus and format
- Use `allowed-tools` to limit scope — always scope Bash narrowly: `Bash(npm test:*, git log:*)` not bare `Bash`
- Use `!` backtick syntax for dynamic context (e.g., !`git status --short`)
- Focus on WHAT and WHY, not exhaustive HOW — trust the model
- One command, one purpose
- Always include a "When Information is Insufficient" section for ambiguity handling
- Every output finding must include a concrete fix, not generic advice
- Use "Constraints" for hard rules, not soft "Principles"
