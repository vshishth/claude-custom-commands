---
description: Root-cause a bug or incident from symptoms, logs, a stack trace, or a Jira ticket — code + Datadog + Loki + git history
argument-hint: error text, stack trace, log snippet, Jira key, or symptom description (optionally with restaurant/location id and time window)
allowed-tools: Read, Grep, Glob, Bash(git log:*, git blame:*, git diff:*, git show:*, go test:*, go vet:*, go build:*, go run:*, npm test:*, gcx:*, cat:*, ls:*), mcp__datadog-mcp, mcp__atlassian__getJiraIssue, mcp__atlassian__searchJiraIssuesUsingJql, mcp__github__search_issues, mcp__github__get_pull_request
---

# Investigate

Find the mechanism, then a *confirmed* trigger. Investigation ends with evidence, not a fix — the fix is `/build/fix`.

```
$ARGUMENTS
```

Recent changes to this repo:
!`git log --since="14 days ago" --pretty=format:"%h %ad %s" --date=short --no-merges | head -25`

Project memory index:
!`cat ~/.claude/projects/$(pwd | sed 's|/|-|g')/memory/MEMORY.md 2>/dev/null || echo "(no memory dir for this project)"`

## Process

1. **Pin the symptom.** Extract concrete signals: exact error text, endpoint/RPC, restaurant or location id, first-seen time, frequency, environment (prod / staging / preview). If `$ARGUMENTS` is a Jira key, fetch it and pull these from the ticket. Classify severity: data corruption / money / crash / functional / cosmetic — it sets how much evidence is required before calling a cause.

2. **Check memory first.** Scan the index above for the error string, module, restaurant id, or a prior investigation of the same area. Prior investigations often already contain the mechanism, a dead end to skip, or a query that works. Read matches; cite them.

3. **Generate 3–5 hypotheses**, ranked by likelihood × blast radius. A low-probability cause that corrupts data outranks a likely cosmetic one.

4. **Gather evidence** — code and telemetry together, not code alone.
   - **Code**: grep the error string and the emitting function. Read the full path, including callers.
   - **History**: `git log -S'<error string>'` and `git blame` on the emitting lines. Correlate the first-seen time with deploys and merged PRs in the window.
   - **Datadog** (SeatNinja Server / Go services): search logs, monitors, and traces for the window. Scope by restaurant with the quoted free-text form `"RestaurantId=77172"` — `RestaurantId:77172` and `@RestaurantId:77172` silently match zero in this pipeline (see `project_datadog_restaurantid_facet_gotcha`). Hot retention is ~15 days; archives are not configured, so an empty result older than that proves nothing.
   - **Grafana Loki** (rPOS logs — not in Datadog): `gcx logs query '{service_name="restaurant-pos"} |= "Location8028" |= "<phrase>"' --datasource ddnnta7sagpogc --from <ISO> --to <ISO> --limit 1000 -o json`. `--to` is required, max range 30d, retention ~30d, `values[]` are objects with `line` as a JSON string. rPOS keys on SpotOn location id (`LocationNNNN`), not RestaurantId — map ids before querying (see `reference_rpos_grafana_loki`).
   - **Timeline**: when sources disagree, build a single table keyed on UTC timestamp with a column per source. Timestamp alignment across sources is the strongest evidence you can produce.

5. **Onset check.** Before saying "started on <date>", prove the instrument could have shown earlier data. A series that begins at the retention floor, or at the date a column/log line was introduced, is an instrument horizon, not a phenomenon onset (see `feedback_data_series_onset`). State the horizon explicitly.

6. **Trace the caller before claiming a repro.** Once the faulty mechanism is identified, `grep` every caller that reaches it and check each for an existing guard. Nominate a trigger only after confirming that path is unguarded. Label each trigger **confirmed** (observed in logs or reproduced) or **theoretical**. Where several callers reach one sink, recommend fixing at the sink (see `trace-the-caller-before-claiming-a-repro`).

7. **Narrow.** Eliminate hypotheses the evidence contradicts. Distinguish correlation from causation — a deploy at the same time is a lead, not a cause, until the diff explains the mechanism.

8. **Blast radius.** What else shares the mechanism: other callers, other restaurants/locations, other environments. Check whether it is still happening now.

## When Information is Insufficient

- No error text, time window, or identifier: ask for exact error text, first-seen time (UTC), environment, and a restaurant/location id. Do not query blind.
- Datadog or `gcx` are unavailable or return errors: say so and continue with code + git only, marking conclusions as *code-only, unverified against telemetry*.
- Evidence supports two mechanisms equally: present both with the single query or test that would discriminate them. Do not pick one to sound decisive.
- The cause is in a dependency or another team's service: name the exact version/service and what to hand them.

## Output

- **Symptom**: one line, with severity and environment
- **Mechanism**: why it happens, with file:line and the log lines that prove it
- **Trigger(s)**: each labelled *confirmed* or *theoretical*, with the caller path
- **Timeline**: table across sources if more than one source was used
- **Onset**: first observed, with the instrument horizon stated
- **Ruled out**: hypotheses eliminated and the evidence that eliminated them
- **Blast radius**: other paths / tenants / environments affected; still occurring?
- **Recommended fix**: minimal, at the sink where possible — for `/build/fix`
- **Verification**: the query or test that proves the fix worked
- **Memory**: if this investigation produced a reusable gotcha or a corrected assumption, say so — save it with `/manage/learn`

## Constraints

- Evidence over confidence. Every causal claim cites a file:line, a log line, or a commit.
- Do not modify code. Do not run migrations or anything that writes to a datastore.
- Do not re-enable a mitigation or feature flag that memory says to leave off.
- Read-only telemetry queries only. Do not create, edit, or mute monitors.
- If the evidence is inconclusive, say so and say what would settle it.
