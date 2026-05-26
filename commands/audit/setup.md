---
description: Senior-engineer review of the user's ~/.claude setup with prioritized improvements for coding, review, and engineering workflow
argument-hint: optional focus area (e.g. "memory", "commands", "hooks", "safety") — leave blank for full review
allowed-tools: Read, Grep, Glob, Bash(ls:*, find:*, wc:*, head:*, tail:*, jq:*, cat:*, du:*, stat:*, file:*)
---

# `~/.claude` Setup Review

Act as a Principal Engineer who has set up dozens of Claude Code environments for high-velocity teams. The user has asked you to review *their* `~/.claude` configuration and recommend concrete, prioritized improvements to their **coding, review, and overall engineering workflow** — not generic best-practice advice.

```
$ARGUMENTS
```

If `$ARGUMENTS` is non-empty, narrow the review to that axis only and skip the others.

## Review Axes

Evaluate the setup against these seven lenses. Don't just list what exists — find the gap between what's there and what a power-user setup looks like in practice.

1. **Workflow coverage** — For the loop *code → test → review → ship → learn*, is each step supported by configuration, hooks, or commands? Where is the user doing manually what their setup could automate?
2. **Signal-to-noise across commands** — Sample 8–12 command files spread across categories. Flag overlap (e.g. similar commands in different namespaces), inconsistent frontmatter, weak prompts, loose `allowed-tools`, and commands that are likely never used. For each weak command: retire / merge / keep.
3. **Automation depth (hooks)** — Inspect `settings.json` for the `hooks` key. Where would hooks add real leverage? Be concrete: name the event, the matcher, and the command. (Examples to consider, not prescribe: post-edit formatters, session-start context preload, pre-commit guards, tool-use logging, push notifications on long task completion.)
4. **Memory & compounding learning** — Inspect the user's memory directory and `MEMORY.md` index. If empty or sparse, this is almost certainly a P0 finding: the user is losing context between sessions. Suggest the *categories* of memories that should exist given an active engineer (preferences, project pointers, recurring corrections, references) — not specific entries.
5. **Safety, cost & footguns** — Check `settings.json` for aggressive defaults: `alwaysThinkingEnabled`, `skipAutoPermissionPrompt`, broad permission allowlists, custom model routing (Bedrock / proxy / API key helpers — rotation and audit story?), MCP config (intentional absence or oversight?). Each gets a verdict, not just a flag.
6. **Reproducibility & portability** — Is `~/.claude` itself under version control? If the laptop dies, what's lost? Distinguish *configuration* worth tracking (settings, commands, agents, skills, statusline scripts, keybindings, CLAUDE.md, MEMORY.md + memories) from *state* that should never be tracked (`projects/`, `cache/`, `shell-snapshots/`, `__store.db`, `history.jsonl`, `paste-cache/`, `file-history/`, `telemetry/`, `debug/`, `tasks/`, `sessions/`, `.last-cleanup`, `.DS_Store`).
7. **Onboarding & shareability** — Could a teammate adopt this setup in an afternoon? Is there a root `CLAUDE.md` or README explaining the conventions? Do all command files have meaningful `description:` frontmatter? Is any custom script (e.g. statusline) readable without spelunking?

## Surfaces to Examine

Read or inspect in roughly this order. Don't read transcripts (`~/.claude/projects/*/sessions/`) — that's out of scope and noisy.

- `~/.claude/settings.json` — every top-level key
- `~/.claude/settings.local.json`
- `~/.claude/CLAUDE.md` (if present)
- `~/.claude/keybindings.json` (if present)
- `~/.claude/.mcp.json` (if present)
- `~/.claude/statusline-command.sh` (if present) — readability + correctness
- `ls ~/.claude/commands/` (and any nested `commands/` subdirectory) — category structure
- Sample one command per category (`audit/*`, `build/*`, `ship/*`, `design/*`, `understand/*`, `automate/*`, `generate/*`, `manage/*`, `operate/*`, `onboard/*`) — check frontmatter quality, prompt quality, `allowed-tools` tightness
- `~/.claude/agents/` and `~/.claude/skills/` (if present) — count + names only
- `~/.claude/projects/<current-project-slug>/memory/` and `MEMORY.md` — count files, sample 1–2 if present
- `~/.claude/plugins/config.json` and `~/.claude/plugins/blocklist.json` — presence check only
- `git status` inside `~/.claude` and inside `~/.claude/commands/` — what's tracked, what isn't

You may also run `du -sh ~/.claude/* 2>/dev/null | sort -h` to spot anything bloated.

## Output

### Findings

Produce **5–10 findings, prioritized, no filler**. If you can't find 5 substantive issues, output fewer — don't pad. For each finding:

- **Severity**: P0 (do this week) / P1 (do this month) / P2 (nice to have)
- **Axis**: one of the seven above
- **Surface**: file path, config key, or command name
- **Current state**: cite directly, e.g. `settings.json:9 — alwaysThinkingEnabled: true`, or `~/.claude/.../memory/ — 0 files`
- **Recommendation**: a specific action, not "consider X". Name the change.
- **Effort**: S (< 30 min) / M (< 2 h) / L (half-day+)
- **Expected impact**: what tangibly changes for the user — workflow time saved, footgun closed, learning compounded, etc.

### Closing summary

End with three short sections:

- **Top 3 to do this week** — highest impact-to-effort, listed by finding ID
- **Top 1 to do this month** — the higher-effort, compounding change
- **What you should NOT change** — one or two things the user is doing right that they should preserve. Be specific so they know it was reviewed and validated, not skipped.

## When Information is Insufficient

- If `$ARGUMENTS` names an axis (e.g. "memory"), restrict findings to that axis. Don't repeat the framework — just deliver findings for that lens.
- If a surface is missing entirely (e.g. no `CLAUDE.md`), that *is* the finding — don't skip the axis because the file isn't there.
- If a finding requires reading a transcript or session history to verify, flag the assumption explicitly rather than reading them.

## Constraints

- **Read-only.** No `Edit`, no `Write`, no `git` mutations. Recommendations only — the user will apply them.
- **No flattery, no filler.** If an axis is genuinely solid, say "no changes needed" in one line and move on. Don't manufacture findings to hit a count.
- **Cite evidence.** Every finding MUST reference a specific file path, config key, or command. No "you should probably…" without a pointer.
- **Don't recommend things that already exist.** Before suggesting "add a security audit command", grep the commands directory. If `audit/security.md` is already there, the finding is invalid.
- **No generic best-practice advice.** Skip "add tests", "improve documentation", "use better naming" *unless* tied to a specific surface in this setup. The review is about THIS user's workflow, not engineering in general.
- **Bound the count.** 5–10 findings total. If you find more, drop the lower-impact ones — don't pad.
- **Don't read session transcripts.** Privacy and noise. Workflow tempo can be inferred from counts (`ls | wc -l`) on `plans/`, `tasks/`, `sessions/` if needed.
- **Honor `$ARGUMENTS`.** If the user passes a focus area, narrow scope. Don't smuggle in findings from other axes.
