---
description: Validate and guide local development environment setup (tools, deps, creds)
argument-hint: optional focus (e.g., "backend", "frontend", "infrastructure")
allowed-tools: Read, Grep, Glob, Bash(which:*, go version:*, node --version:*, npm --version:*, python --version:*, docker --version:*, kubectl version:*, aws --version:*, brew:*, cat:*, ls:*, find:*)
---

# Local Setup Validation

Act as a Principal Engineer validating a developer's local environment. Check every prerequisite and provide exact fix commands for anything missing.

Project requirements:
!`ls go.mod package.json requirements.txt Makefile docker-compose*.yml .tool-versions .nvmrc .go-version 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Detect required tools** — From project config files, determine required: language runtimes, package managers, build tools, infrastructure CLIs, container tools.
2. **Check versions** — Verify installed versions match project requirements (from `.tool-versions`, `.nvmrc`, `go.mod`, `engines` in package.json).
3. **Validate dependencies** — Check if dependencies are installed (`go mod download`, `npm ci`, etc.) and up to date.
4. **Check credentials** — Verify required credentials are configured (AWS profile, Docker registry login, kubectl context) without exposing values.
5. **Verify local services** — Check if required local services are running (database, cache, queue) via docker-compose or equivalent.
6. **Test the build** — Confirm the project builds and tests pass locally.

## When Information is Insufficient

If the project has no setup documentation, derive requirements from config files and Dockerfile. If specific versions can't be determined, check for `.tool-versions` (asdf) or equivalent. If credentials can't be verified safely, list what's needed and how to obtain it.

## Output

### Environment Status
| Requirement | Expected | Actual | Status |
|-------------|----------|--------|--------|
| Go | 1.22+ | 1.22.3 | pass |
| Node | 20.x | not found | FAIL |

### Fix Commands
```bash
# For each failure, the exact command to fix it:
brew install node@20
```

### Credentials Checklist
- [ ] AWS profile configured: `aws sts get-caller-identity`
- [ ] Docker registry: `docker login`
- [ ] kubectl context: `kubectl config current-context`

### Ready to Develop
- Build: `make build` — [pass/fail]
- Test: `make test` — [pass/fail]
- Run: `make run` or `docker-compose up` — [instructions]

## Constraints

- NEVER run install commands automatically — only report what's needed and provide commands
- NEVER expose credential values — only check existence
- Check version compatibility, not just presence (wrong version causes subtle bugs)
- If Docker is available, prefer containerized development over local installs
- Flag conflicting tool versions (multiple Go versions, nvm vs system node)
