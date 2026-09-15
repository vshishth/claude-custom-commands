---
description: Implement one PR-sized slice of a feature from a Jira ticket, spec, or description — Go/.NET aware, tests included, verified before handoff
argument-hint: Jira key, spec path, or feature description; optionally "PR 2 of 4: <scope>" to implement one slice of a plan
allowed-tools: Read, Grep, Glob, Bash(go build:*, go test:*, go vet:*, go mod:*, go tool:*, go generate:*, make:*, buf:*, golangci-lint:*, gofmt:*, dotnet build:*, dotnet test:*, dotnet format:*, npm test:*, npm run:*, git status:*, git diff:*, git log:*, git branch:*, cat:*, ls:*), mcp__atlassian__getJiraIssue, mcp__github__get_issue, mcp__github__get_pull_request
---

# Implement

Build exactly one reviewable slice, in the repo's existing style, with tests that ran green. If the ticket needs more than one PR, implement the first and hand back a plan for the rest.

```
$ARGUMENTS
```

Current branch:
!`git branch --show-current`

Working tree:
!`git status --short`

Stack signals:
!`ls go.mod Makefile buf.yaml buf.gen.yaml .golangci.yml .golangci.yaml *.sln Directory.Build.props package.json 2>/dev/null`

Make targets:
!`grep -oE "^[a-z][a-z0-9_-]+:" Makefile 2>/dev/null | tr -d ':' | tr '\n' ' '`

Project memory index:
!`cat ~/.claude/projects/$(pwd | sed 's|/|-|g')/memory/MEMORY.md 2>/dev/null || echo "(no memory dir for this project)"`

## Process

1. **Read the ask.** If `$ARGUMENTS` is a Jira key, fetch it and extract acceptance criteria. If it names a PR slice ("PR 2 of 4"), implement only that slice. Restate AC as a checklist before touching code.

2. **Read memory before exploring.** Scan the index above for the module, ticket, or epic. Project memory records traps that grep will not show you (e.g. a config struct that makes env vars mandatory at boot, a lint path that is broken pre-existing, a proto rule no linter checks). Cite anything you rely on.

3. **Explore the pattern, not the whole repo.** Find the closest existing feature and copy its shape: file layout, error handling, logging, test style. In `partnerships-*` services the reference pattern is `partnerships-order`. In `Server`, service/repo tests hit a real DB and clean up in `[TearDown]` — there are no repo interfaces to mock.

4. **Size and split.** If the change spans more than one of {proto, migration, service/handler, infra/config, docs}, or exceeds ~8 files, stop and propose ordered PRs — one concern each, smallest dependency first. Ask which slice to build now. A single PR is reviewable in one sitting.

5. **Plan the slice** in 5–10 lines: files to add/modify, public API changes, edge cases, and which AC it closes. State assumptions explicitly. If a public interface or proto changes, note compatibility (`buf breaking`, wire format, callers).

6. **Build.** Minimal code in the existing style. No new dependencies without saying why the existing ones are insufficient. No drive-by refactors — note them for a separate PR.

7. **Test as you go.** Table-driven tests in Go; the repo's fixture pattern in .NET. Cover the happy path plus the edge cases from step 5. Do not weaken or delete existing assertions to make a test pass.

8. **Verify — run, don't describe.**
   - Go: `go build ./...` · `go vet ./...` · `go test ./...` (or `make test`). Lint via `make lint` / `golangci-lint run` if it works in this repo; if memory says lint is broken pre-existing, say so and skip rather than "fixing" go.mod. Protos: `make generate-protos` / `buf lint` / `buf breaking` — if buf fails with a BSR "resource not found" hash, it is missing credentials in `~/.netrc`, not your change.
   - .NET: `dotnet build` · `dotnet test` scoped to the affected project(s) (`--filter` for the class you touched).
   - Frontend: `npm test` / `npm run lint`.
   Paste the final command and its tail. If anything fails, fix it or report it — never claim green without output.

9. **Hand off.** Summarize what changed, which AC are closed, what remains for later slices, and anything the reviewer should look at first. Then `/ship/pr`.

## When Information is Insufficient

- No acceptance criteria on the ticket: derive a provisional checklist from the description, mark it *inferred*, and confirm before building.
- The ask depends on a service or API not in this repo: define the interface boundary, stub it behind an interface, and name what you need from the other side.
- Two existing patterns conflict: pick the more recent one (`git log` on both), say which you chose and why.
- Tests cannot run locally (missing DB, missing BSR token, broken lint): report the exact command and error, state what *did* pass, and mark verification as partial.

## Output

- **Slice**: what this PR does, in one line, with Jira key
- **AC**: checklist with closed/open
- **Changes**: files added/modified, grouped by concern
- **Verification**: commands run and results (paste tails), or what could not run and why
- **Remaining slices**: ordered, with dependencies — or "none"
- **Reviewer notes**: assumptions, compatibility, anything non-obvious

## Constraints

- One concern per PR. Stop and re-scope when the plan grows.
- Follow existing conventions; do not introduce new ones in the same PR that adds a feature.
- Never skip, delete, or loosen an existing test to get green.
- Never edit `go.mod`/`go.sum` to work around a broken lint toolchain.
- Never run migrations or writes against a shared datastore.
- Do not commit or push — that is `/ship/pr`.
