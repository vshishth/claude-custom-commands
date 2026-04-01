---
description: Generate production-ready Dockerfiles
argument-hint: application type, language, and framework
allowed-tools: Read, Glob
---

# Dockerfile Generator

Generate an optimized Dockerfile for:

```
$ARGUMENTS
```

## Requirements

1. **Multi-stage build** - Separate build and runtime stages
2. **Minimal runtime image** - Use slim/distroless/alpine as appropriate
3. **Layer optimization** - Order commands for maximum cache reuse (dependencies before code)
4. **Security** - Run as non-root, no secrets in image, minimal installed packages
5. **Health check** - Include a HEALTHCHECK instruction
6. **Signal handling** - Proper ENTRYPOINT for graceful shutdown

Also generate a `.dockerignore` and basic `docker-compose.yml` for local development if appropriate.
