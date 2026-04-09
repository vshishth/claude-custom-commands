---
description: Design CI/CD pipeline configuration
argument-hint: project type, tech stack, and target platform (GitHub Actions, GitLab CI, etc.)
allowed-tools: Read, Grep, Glob, Bash(git:*, ls:*)
---

# CI/CD Pipeline

Act as a Principal Engineer. Design a production-grade CI/CD pipeline.

```
$ARGUMENTS
```

## Process

1. **Analyze** the project structure, tech stack, and existing pipeline (if any). If an existing pipeline exists, propose incremental improvements rather than a rewrite.
2. **Design stages**: lint → type-check → test → security scan → build → deploy — include only what's needed
3. **Generate configuration** for the target platform (default: GitHub Actions) with:
   - Dependency caching for fast builds
   - Parallel test execution where beneficial
   - Branch-specific behavior (PR checks vs deploy on main)
   - Secret management via platform-native secrets
   - Environment promotion (staging → production) with approval gates
   - Artifact management — where builds are stored, retention policy
   - Notification strategy — what triggers alerts (failures, deployments) and where (Slack, PR comments)

## Output

- **Pipeline configuration file(s)** — ready to commit
- **Environment/secret configuration** — what secrets need to be configured in the platform
- **Estimated pipeline duration** — expected time for PR checks vs full deploy
- **Caching configuration** — what's cached, expected cache hit rate

## When Information is Insufficient

If no target platform is specified, default to GitHub Actions. If the project has an existing pipeline, analyze it first and propose incremental improvements. If the test suite is unknown, include a placeholder stage with a clear TODO.

## Constraints

- Pipeline MUST complete under 10 minutes for PR checks — split longer jobs or parallelize
- Fail fast: run cheap checks (lint, types) before expensive ones (integration tests, builds)
- Reproducible builds: pin versions, use lock files, cache deterministically
- Never store secrets in pipeline config — use the platform's secret management
- Never expose secrets in logs — mask all secret values
- Keep it simple: don't add stages you don't need yet
