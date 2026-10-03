---
title: "pre-commit end-of-file-fixer Gotcha"
type: concept
domain: ai
tags:
  - git
  - pre-commit
  - developer-experience
  - agentic-coding
  - tooling
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/dev-tooling-gotchas]]"
---

# pre-commit end-of-file-fixer Gotcha

The `end-of-file-fixer` pre-commit hook adds a trailing newline to files that lack one. When a commit fails for any reason, the hook has already modified the file on disk but the staged blob is still the unfixed version. On the next commit attempt, the staged and working-tree versions diverge, causing the hook to conflict with itself and fail again — even though the file already looks correct on disk. This bites agentic-coding workflows especially, where an agent retries a failed commit without re-staging.

## What triggers it

A file (e.g. `.env.example`) lacks a trailing newline. The first commit attempt fails (for any reason), leaving the on-disk file fixed but the staged blob unfixed. The next `git commit` runs the hook again — it tries to stash the unstaged diff, apply the fix, and restore, but the stash conflicts with the already-fixed working tree.

Symptoms: `end-of-file-fixer` reports `Failed` with exit code 1 and "files were modified by this hook", even though it already looks correct on disk.

## Fix

Re-stage the auto-fixed files so the staged blob matches the working tree, then commit:

```bash
git add -u            # pick up any auto-fixes pre-commit made to tracked files
git add <new files>   # for any untracked files
git commit -m "..."
```

Or run all hooks first to batch-fix everything, then stage and commit:

```bash
pre-commit run --all-files
git add -u
git commit -m "..."
```

## Why this happens

Pre-commit stashes unstaged changes before running hooks, then restores them afterward. If the hook already fixed the file on a prior run (and that fix is now in the working tree but not staged), the stash/restore cycle collides with the existing working-tree change — causing a rollback and false failure.

## Related Concepts

- [[wiki/concepts/agentic-coding]] — agent commit loops that trip this gotcha
- [[wiki/concepts/spec-driven-development]] — disciplined workflows around agent commits

## Sources

- [[wiki/sources/dev-tooling-gotchas]]
