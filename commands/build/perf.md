---
description: Identify performance bottlenecks and provide concrete optimizations
argument-hint: file path, code, or description of performance issue
allowed-tools: Read, Grep, Glob, Bash
---

# Performance Analysis

Analyze the following for performance issues and provide actionable optimizations:

```
$ARGUMENTS
```

## Process

1. **Profile** - Identify the hot path. What runs most frequently or takes the most time/memory?
2. **Measure** - Determine algorithmic complexity (time and space) of critical paths
3. **Diagnose** - Find the specific bottlenecks:
   - Unnecessary allocations or copies
   - N+1 queries or chatty I/O
   - Missing caching or indexes
   - Suboptimal data structures or algorithms
   - Blocking operations that could be async
   - Redundant computation
4. **Optimize** - For each bottleneck, provide a specific fix with expected impact

## Output

For each finding:
- **Location**: Where in the code
- **Impact**: Estimated severity (10x slower vs 10% slower matters)
- **Fix**: Concrete code change
- **Tradeoff**: Any cost to the optimization (complexity, memory, readability)

Prioritize by impact. Don't optimize what doesn't matter.
