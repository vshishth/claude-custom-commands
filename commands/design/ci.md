---
description: Design CI/CD pipeline configuration
argument-hint: project type, tech stack, and target platform (GitHub Actions, GitLab CI, etc.)
allowed-tools: Read, Glob, Bash
---

# CI/CD Pipeline

Design a CI/CD pipeline for:

```
$ARGUMENTS
```

## Process

1. **Analyze** the project structure, tech stack, and existing pipeline (if any)
2. **Design stages**: lint, test, build, security scan, deploy - include only what's needed
3. **Generate configuration** for the target platform with:
   - Dependency caching for fast builds
   - Parallel test execution where beneficial
   - Branch-specific behavior (PR checks vs deploy on main)
   - Secret management
   - Environment promotion (staging -> production)

## Principles

- Fast feedback: fail fast on cheap checks (lint, types) before expensive ones (integration tests)
- Reproducible builds: pin versions, use lock files, cache deterministically
- Security: scan dependencies, don't expose secrets in logs, use least-privilege service accounts
- Keep it simple: don't add stages you don't need yet
