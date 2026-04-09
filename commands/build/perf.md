---
description: Identify performance bottlenecks and provide concrete optimizations
argument-hint: file path, code, or description of performance issue
allowed-tools: Read, Grep, Glob, Bash(npm:*, npx:*, node:*, python:*, go:*, cargo:*, time:*, hyperfine:*, ab:*, wrk:*, git diff:*)
---

# Performance Analysis

Act as a Principal Engineer. Analyze for performance issues and provide actionable optimizations.

```
$ARGUMENTS
```

## Process

1. **Baseline** — Establish current performance characteristics. If benchmarks exist, run them. If not, note that a baseline should be created before optimizing.
2. **Profile** — Identify the hot path. What runs most frequently or takes the most time/memory?
3. **Measure** — Determine algorithmic complexity (time and space) of critical paths
4. **Diagnose** — Find the specific bottlenecks:
   - Unnecessary allocations or copies
   - N+1 queries or chatty I/O
   - Missing caching or indexes
   - Suboptimal data structures or algorithms
   - Blocking operations that could be async
   - Redundant computation
5. **Optimize** — For each bottleneck, provide a specific fix with expected impact
6. **Regression guard** — For each optimization, suggest a benchmark or test that will catch performance regressions

## Output

For each finding:
- **Location**: Where in the code (file:line)
- **Impact**: Estimated severity with quantified improvement (e.g., "3x reduction in allocations", not "faster")
- **Fix**: Concrete code change
- **Tradeoff**: Any cost to the optimization (complexity, memory, readability)
- **Regression guard**: Benchmark or assertion to prevent regression

Prioritize by impact. Don't optimize what doesn't matter.

## When Information is Insufficient

If no specific performance issue is described, profile the hot path of the specified code and report the top 3 bottlenecks by estimated impact. If no benchmarks exist, recommend creating them before optimizing.

## Constraints

- Never optimize without measuring first — intuition about performance is often wrong
- Every optimization MUST state its expected improvement quantitatively
- Preserve correctness — a faster wrong answer is not an optimization
- Prioritize algorithmic improvements (O(n²) → O(n log n)) over micro-optimizations
