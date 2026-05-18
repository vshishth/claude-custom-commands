---
description: Define quality gates that must pass before shipping
argument-hint: gate type or "status" (e.g., "pre-merge", "pre-deploy", "status")
allowed-tools: Read, Grep, Glob, Bash(go test:*, npm test:*, npm run:*, npx:*, tsc:*, eslint:*, golangci-lint:*, git diff:*, find:*)
---

# Quality Guard

Act as a Principal Engineer enforcing quality gates. Run all checks that must pass before code can be shipped, and report a clear pass/fail verdict.

Project type:
!`ls go.mod package.json Cargo.toml .golangci.yml .eslintrc* tsconfig.json 2>/dev/null`

CI config (to mirror locally):
!`find . -name "*.yml" -path "*github/workflows*" -o -name "*.yml" -path "*gitlab-ci*" -o -name "Jenkinsfile" | head -5 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Discover checks** — From CI config and project tooling, identify all quality checks: lint, type-check, test, security scan, build, coverage threshold.
2. **Run checks sequentially** — Execute each check, capturing pass/fail and output. Stop on first critical failure or run all and report.
3. **Assess coverage** — If coverage thresholds are configured, verify current coverage meets the bar.
4. **Check for anti-patterns** — Scan recent changes for: TODO/FIXME without tickets, console.log/fmt.Println in production code, hardcoded secrets, disabled tests.
5. **Produce verdict** — Clear PASS/FAIL with details on each check.

## Gate Presets

- **pre-commit**: lint + type-check (fast, <10s)
- **pre-merge**: lint + type-check + tests + coverage + security (thorough, <5min)
- **pre-deploy**: all of pre-merge + build + integration tests + config validation

## When Information is Insufficient

If gate type isn't specified, run "pre-merge" (the most common use case). If a check tool isn't installed, report it as "SKIP (tool not found)" rather than failing. If CI config exists, mirror its checks locally.

## Output

### Quality Gate: [preset name]

| Check | Status | Duration | Details |
|-------|--------|----------|---------|
| Lint | PASS | 2.3s | 0 warnings |
| Types | PASS | 4.1s | clean |
| Tests | FAIL | 12.4s | 2 failures |
| Coverage | SKIP | - | threshold not configured |
| Security | PASS | 1.8s | 0 vulnerabilities |

### Verdict: FAIL

### Failures (must fix)
- Test `TestReservationCreate`: expected 200, got 422 — [file:line]

### Warnings (should fix)
- 3 TODO comments without ticket references

## Constraints

- A single FAIL in any check means the overall verdict is FAIL — no partial passes
- NEVER skip tests — if tests are slow, report time but still run them
- Security scan failures are always CRITICAL severity
- Report exact file:line for every failure to enable quick fixes
- If running "pre-deploy" gate, the project MUST build successfully
- Include total gate execution time in the report
