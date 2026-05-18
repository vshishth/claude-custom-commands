---
description: Discover stack, key files, conventions, and team context for a new developer
argument-hint: optional focus area (e.g., "backend", "infrastructure")
allowed-tools: Read, Grep, Glob, Bash(find:*, wc:*, git log:*, git shortlog:*, cat:*, head:*, ls:*)
---

# Project Onboarding

Act as a Principal Engineer onboarding a new team member. Produce a concise project briefing that gets someone productive in minutes, not hours.

Project root:
!`ls README.md CLAUDE.md Makefile docker-compose*.yml go.mod package.json Cargo.toml 2>/dev/null`

Recent activity:
!`git log --oneline -10 --no-merges 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Identify the stack** — Detect language, framework, build system, database, message broker, cloud provider from config files and dependencies.
2. **Map key files** — Find entry points, config files, route definitions, schema definitions, and deploy configs. List the 10-15 most important files with one-line descriptions.
3. **Extract conventions** — Detect naming patterns, directory structure philosophy, testing approach, commit message format, and branching strategy from existing code and git history.
4. **Identify domain concepts** — Scan models, types, and proto definitions for the core domain vocabulary.
5. **Surface team context** — Who are the top 3-5 contributors? What areas are actively changing? What was the last significant architectural decision?

## When Information is Insufficient

If the project has no README, synthesize one from what you discover. If git history is empty or shallow, skip team context and focus on code structure. If a focus area is specified, prioritize that area over a full sweep.

## Output

### Quick Start
- How to build: `...`
- How to test: `...`
- How to run locally: `...`

### Architecture (3-5 sentences)
### Key Files (table: path | purpose)
### Conventions (bullet list)
### Domain Vocabulary (term | meaning)
### Active Areas (most-changed directories in last 30 days)

## Constraints

- Keep total output under 200 lines — this is a briefing, not documentation
- NEVER assume conventions — derive everything from the actual code
- Include build/test/run commands only if they are confirmed to exist
- Flag any "gotchas" a new developer would hit (missing docs, unusual setup steps, non-obvious dependencies)
