---
description: Benchmarking with regression detection and historical comparison
argument-hint: package, function, or file to benchmark
allowed-tools: Read, Grep, Glob, Bash(go test -bench:*, go test -run=^$ -bench:*, npm run bench:*, npx:*, node --prof:*, hyperfine:*, git stash:*, git log:*, cat:*)
---

# Benchmark

Act as a Principal Engineer focused on performance. Run benchmarks, detect regressions, and provide actionable optimization guidance.

Project type:
!`ls go.mod package.json Cargo.toml 2>/dev/null`

Current branch:
!`git branch --show-current 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Discover benchmarks** — Find existing benchmark files/functions. For Go: `_test.go` files with `Benchmark*` functions. For JS/TS: bench files or vitest bench configs.
2. **Run benchmarks** — Execute targeted benchmarks for the specified scope. Capture: ops/sec, ns/op, allocs, memory.
3. **Compare against baseline** — If a baseline exists (previous run, main branch), compare results and flag regressions (>5% degradation).
4. **Profile hotspots** — If a regression is found, identify the likely cause from allocation patterns or flamegraph data.
5. **Recommend fixes** — For each regression or bottleneck, provide a concrete optimization with expected improvement.

## When Information is Insufficient

If no benchmarks exist for the target, generate a benchmark file first and then run it. If no baseline exists, establish one and report absolute numbers. If the target is ambiguous, list available benchmarks and ask which to run.

## Output

| Benchmark | Current | Baseline | Delta | Status |
|-----------|---------|----------|-------|--------|
| name | 150 ns/op | 140 ns/op | +7.1% | REGRESSION |

### Regressions (if any)
For each: root cause hypothesis + concrete fix

### Recommendations
Prioritized list of optimizations with expected impact

## Constraints

- NEVER run benchmarks with `-count` less than 3 — statistical significance matters
- Always report allocations alongside time (allocs often matter more than ns/op)
- Flag flaky benchmarks (high variance between runs)
- Do not modify production code without confirming the benchmark results first
