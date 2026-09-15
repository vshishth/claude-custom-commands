---
description: Save a correction, gotcha, or verified fact as a named memory file in the right project dir and index it in MEMORY.md
argument-hint: the lesson in one or two sentences, or "from this session" to extract it from the conversation; optionally "global" to force the cross-project dir
allowed-tools: Read, Write, Edit, Grep, Glob, Bash(ls:*, cat:*, grep:*, git rev-parse:*, git log:*, git status:*, date:*, mkdir:*)
---

# Learn

Turn one lesson from this session into a memory file that a future session will find via `MEMORY.md`. Write only what was verified, name the trigger, and say how to apply it.

```
$ARGUMENTS
```

Repo root:
!`git rev-parse --show-toplevel 2>/dev/null || pwd`

Project memory dir and index:
!`d=~/.claude/projects/$(git rev-parse --show-toplevel 2>/dev/null | sed 's|/|-|g')/memory; echo "$d"; ls "$d" 2>/dev/null; echo "--- MEMORY.md ---"; cat "$d/MEMORY.md" 2>/dev/null || echo "(none yet)"`

Global memory index:
!`cat ~/.claude/projects/-Users-sachinvshishth-Documents-Source/memory/MEMORY.md 2>/dev/null`

## Process

1. **Isolate one lesson.** If `$ARGUMENTS` says "from this session", find the moment the user corrected you, a tool returned something that contradicted an assumption, or a workaround cost real time. One file per lesson; run again for a second one.

2. **Classify** — this picks the filename prefix and the section of `MEMORY.md`:
   - `feedback_` — a correction to how you work, or an approach the user validated ("smaller PRs", "trace the caller before claiming a repro").
   - `project_` — state or a fact about this codebase that grep will not reveal (a broken lint path, a config struct trap, a PR that is stale).
   - `reference_` — a pointer to an external system with the exact incantation that worked (a Loki datasource UID, a Datadog query form).

3. **Choose the directory.**
   - Repo-specific → the project dir above (create it if missing).
   - Applies across SpotOn repos (infra, Jira/GitHub conventions, tooling on this machine) → `~/.claude/projects/-Users-sachinvshishth-Documents-Source/memory/`.
   - Applies to every project regardless of employer → propose a one-line addition to `~/.claude/CLAUDE.md` instead of a memory file, and stop for approval.
   `$ARGUMENTS` containing "global" forces the second option.

4. **Check for an existing entry.** Grep the chosen dir for the key nouns. If one exists, update it in place (add the new evidence, fix the wrong claim, bump `modified`) rather than creating a near-duplicate. Say which you did.

5. **Write the file** as `<prefix>_<slug>.md`, slug in `snake_case`, ≤5 words, naming the *thing* not the session:

   ```markdown
   ---
   name: <slug-with-dashes>
   description: "<one line a future session can act on without opening the file>"
   metadata:
     type: <feedback|project|reference>
     modified: <ISO-8601 UTC>
   ---

   <What was believed / attempted, and what was actually true — 2–6 lines, with the concrete
   evidence: command + output tail, file:line, PR number, date.>

   **Why:** <the cost or failure mode if forgotten>

   **How to apply:** <the exact check, command, or rule to follow next time>
   ```

   Link related entries with `[[slug]]`. Include the exact command or query that worked; a paraphrase is not reusable.

6. **Index it.** Add one line to the dir's `MEMORY.md` under the matching section (`## Feedback`, `## Conventions`/project sections, `## Reference`), in the existing format: `- [Title](file.md) — <description>`. Create `MEMORY.md` with a `# Project Memory` header if it does not exist. Keep the index line under 200 characters.

7. **Show the result**: the file path, the frontmatter, and the index line. Do not commit — `~/.claude` is committed manually.

## When Information is Insufficient

- The lesson is an assumption, not a verified fact: do not save it. Say what would verify it.
- The lesson is really a task ("fix X later"): that belongs in Jira or `project_progress.md`, not a new file — say so.
- You cannot tell whether it is repo-specific or global: default to the repo dir and note in the file that it may generalize.
- No git repo in the working directory and no "global" flag: ask which project it belongs to.

## Constraints

- One lesson per file. No session logs, no summaries of work done.
- Facts only, with evidence. No "probably", no restating of documentation that grep would find.
- Never record secrets, tokens, credentials, or their locations beyond "in `~/.netrc`"-level pointers.
- Never delete an existing memory file; correct it in place and say what changed.
- Match the existing frontmatter and index format exactly — the index is what future sessions read first.
