---
description: Create a well-structured git commit with conventional commit format
argument-hint: optional description of changes
allowed-tools: Bash(git status:*, git diff:*, git diff --staged:*, git log:*)
---

# Git Commit Generator

## Context
Current git status:
!`git status`

Staged changes:
!`git diff --staged`

Unstaged changes:
!`git diff`

Recent commit messages for reference:
!`git log -5 --pretty=format:"%h %s" --no-merges`

## Instructions

Create a well-structured, atomic git commit following these steps:

1. **Analyze Changes**
   - Understand what the changes do
   - Group related changes into logical units

2. **Commit Message Structure**
   - Use the Conventional Commits format:
     ```
     type(scope): summary
     
     body
     
     footer
     ```
   - Types: feat, fix, docs, style, refactor, perf, test, build, ci, chore
   - Keep summary under 50 chars, imperative mood
   - Body explains WHAT and WHY (not HOW)
   - Reference issues in footer

3. **Command Generation**

Generate the git commands needed to:
1. Add any missing files to staging if needed
2. Create a properly formatted commit
3. Verify the commit was successful

## Implementation Details
$ARGUMENTS