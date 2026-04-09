---
description: Explain unfamiliar code, trace logic, and clarify architecture
argument-hint: file path, function name, or paste code
allowed-tools: Read, Grep, Glob
---

# Explain Code

Act as a Principal Engineer. Explain the following code clearly and thoroughly.

```
$ARGUMENTS
```

## Process

1. **Read** the code and its surrounding context (imports, callers, callees)
2. **Explain** what it does at a high level — the purpose and intent, not just line-by-line
3. **Trace** the key logic paths, including edge cases and error handling
4. **Contextualize** — how does this fit into the broader system? What depends on it?

## Output

- **Purpose**: One-sentence summary of what this code exists to do
- **How it works**: Walk through the logic in plain language
- **Key concepts**: Any patterns, algorithms, or domain knowledge needed to understand it
- **Gotchas**: Non-obvious behavior, implicit assumptions, or tricky edge cases
- **Security implications**: Note any security-sensitive patterns (auth, crypto, input handling, data exposure) if present
- **Related code**: Other files/functions that interact with this

## When Information is Insufficient

If the referenced code does not exist at the given path, search for it by function/class name using Grep. If not found, report this to the user rather than guessing.

## Constraints

- Explain the WHY, not just the WHAT — the code already shows the what
- Adjust depth to complexity — don't over-explain simple code
- Use concrete examples when abstract logic is hard to follow
- If the code contains a bug or security issue, flag it clearly but do not fix it — that's a separate command
- Do not modify any code — this is a read-only analysis
