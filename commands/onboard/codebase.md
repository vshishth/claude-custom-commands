---
description: Generate codebase map with architecture overview and module boundaries
argument-hint: optional depth (e.g., "high-level", "detailed")
allowed-tools: Read, Grep, Glob, Bash(find:*, wc:*, tree:*, git log:*, ls:*)
---

# Codebase Map

Act as a Principal Engineer creating an architecture map for a codebase. Produce a visual and navigable guide to the system's structure.

Directory structure:
!`find . -type f -name "*.go" -o -name "*.ts" -o -name "*.tsx" -o -name "*.py" -o -name "*.rs" | head -50`

Top-level layout:
!`ls -d */ 2>/dev/null | head -20`

```
$ARGUMENTS
```

## Process

1. **Map module boundaries** — Identify top-level packages/modules and their responsibilities from directory names, package declarations, and import patterns.
2. **Trace dependency flow** — Determine which modules depend on which. Identify the dependency direction (who imports whom).
3. **Identify layers** — Detect architectural layers (API/handlers → service/business logic → repository/data → infrastructure/external).
4. **Find integration points** — Locate where external systems are called (HTTP clients, gRPC stubs, queue producers/consumers, database connections).
5. **Measure size** — Report file counts and line counts per module to indicate relative complexity.

## When Information is Insufficient

If depth is "high-level" or not specified, show only top-level modules and their relationships. If "detailed", drill into sub-packages. If the codebase is a monorepo, ask which service to map or show the top-level service inventory.

## Output

### Architecture Diagram (ASCII)
```
[Layer/Module] --depends-on--> [Layer/Module]
```

### Module Inventory
| Module | Responsibility | Size (files/LOC) | Key Entry Point |
|--------|---------------|-------------------|-----------------|

### Dependency Flow
- Direction of dependencies (which layer depends on which)
- External integration points

### Hotspots
- Largest modules (potential complexity)
- Most-imported modules (coupling risk)
- Modules with no tests

## Constraints

- Use ASCII diagrams only — no external rendering tools
- Derive architecture from code structure, not assumptions
- Distinguish between compile-time and runtime dependencies
- Flag circular dependencies as warnings
