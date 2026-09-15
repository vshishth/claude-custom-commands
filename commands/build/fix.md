---
description: Fix a failing build, lint, vet, or test — or apply the minimal fix from a /understand/investigate result — Go/.NET aware, verified by re-running
argument-hint: error output, failing test name, CI job URL, or the "Recommended fix" section from /investigate; empty to auto-detect
allowed-tools: Read, Grep, Glob, Bash(go build:*, go test:*, go vet:*, go tool:*, go generate:*, make:*, buf:*, golangci-lint:*, gofmt:*, dotnet build:*, dotnet test:*, dotnet format:*, npm test:*, npm run:*, npx tsc:*, npx eslint:*, git status:*, git diff:*, git log:*, git blame:*, git stash list:*, cat:*, ls:*), mcp__teamcity, mcp__github__get_pull_request
---

# Fix

Make the failing thing pass by fixing its cause, prove it with a re-run, and change nothing else.

```
$ARGUMENTS
```

Working tree:
!`git status --short`

Stack signals:
!`ls go.mod Makefile buf.yaml .golangci.yml .golangci.yaml *.sln package.json 2>/dev/null`

Project memory index:
!`cat ~/.claude/projects/$(pwd | sed 's|/|-|g')/memory/MEMORY.md 2>/dev/null || echo "(no memory dir for this project)"`

## Process

1. **Get the real error.** If `$ARGUMENTS` is empty, run the stack's checks in order and stop at the first failure:
   - Go: `go build ./...` → `go vet ./...` → `go test ./...` (or `make test`) → `make lint` / `golangci-lint run` → `buf lint` if protos changed.
   - .NET: `dotnet build` → `dotnet test` on the affected project.
   - Frontend: `npm run lint` → `npx tsc --noEmit` → `npm test`.
   If `$ARGUMENTS` is a CI job, fetch the failing step's log rather than guessing from the summary. Work from the full error text, not the last line.

2. **Check memory for a known trap.** Scan the index above before fixing anything in the toolchain. Known pre-existing failures in these repos include: buf failing with a BSR "resource … not found" hash (missing `~/.netrc` credential, not your change); `golangci-lint` failing on `missing go.sum entry` or a Go-version mismatch (broken pre-existing in `partnerships-loyalty`); Pacific-timezone test flakes in `Server`. If the failure matches a memory entry, say so and do not "fix" `go.mod`, the Makefile, or the global test default.

3. **Is it pre-existing?** `git stash list` / `git diff` to confirm the failure is caused by the current changes. Run the same check on a clean tree if unsure. A pre-existing failure gets reported, not silently absorbed into this PR.

4. **Classify and fix at the cause.**
   - **Build / compile**: missing import, wrong signature, generated code out of date (`make generate` / `make generate-protos` / `go generate ./...`) — regenerate rather than hand-edit generated files.
   - **Vet / lint**: fix the code. A `//nolint:<rule> // <reason>` or `#pragma warning disable` is allowed only with a reason and only when the rule is wrong for this case.
   - **Test failure**: read the assertion and the code under test; decide which is wrong. Fix the code if the test encodes the requirement; fix the test only if the requirement changed and say which requirement. Never delete an assertion, widen a tolerance, or add `t.Skip` to get green.
   - **Flaky test**: reproduce with `go test -run <Name> -count=20` (Go) or repeated `dotnet test --filter` before touching it. If it is timing/ordering, fix the determinism, not the timeout.
   - **From `/investigate`**: apply the recommended fix at the sink named there. Add a regression test that fails before and passes after.

5. **Verify by re-running the exact failing command**, then the full check for that stack. Paste the tail of the output. Also run `gofmt -l .` / `dotnet format --verify-no-changes` if formatting could have drifted.

6. **Two cycles maximum.** If a fix surfaces new failures, do one more cycle. After that, stop and report: fixed, remaining, and why — a cascading failure usually means the diagnosis was wrong, not that more edits are needed.

## When Information is Insufficient

- Auto-detect finds nothing: report "all checks pass" with the commands run, and stop. Do not invent problems.
- The failure cannot be reproduced locally (needs a DB, BSR token, or CI-only env): report the exact command and error, state what did pass, and describe the fix as *unverified locally*.
- The failing test's intent is unclear: quote the assertion, read `git log -p` on the test, and ask before changing it.

## Output

- **Failure**: the exact command and error (first meaningful line)
- **Cause**: file:line and why — pre-existing or introduced by current changes
- **Fix**: what changed and why it is the minimal correct change
- **Verification**: re-run output tail for the failing command and the full stack check
- **Not touched**: pre-existing failures or lint suppressions left in place, with the memory entry that explains them

## Constraints

- Fix causes, not symptoms. Do not suppress, skip, or loosen to get green.
- Do not edit `go.mod`/`go.sum`, the Makefile, or global test defaults to work around a known-broken toolchain.
- Do not change unrelated code; note drive-by findings for a separate PR.
- Do not regenerate code you cannot build and test afterward.
- Do not commit or push — that is `/ship/pr`.
