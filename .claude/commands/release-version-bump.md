---
name: release-version-bump
description: Workflow command scaffold for release-version-bump in claude-mem.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /release-version-bump

Use this workflow when working on **release-version-bump** in `claude-mem`.

## Goal

Bump the project version for a new release, updating all relevant package and plugin files.

## Common Files

- `.claude-plugin/marketplace.json`
- `package.json`
- `plugin/.claude-plugin/plugin.json`
- `plugin/package.json`
- `plugin/scripts/mcp-server.cjs`
- `plugin/scripts/worker-service.cjs`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update version numbers in package.json and plugin/package.json
- Update .claude-plugin/marketplace.json and plugin/.claude-plugin/plugin.json
- Rebuild plugin/scripts/mcp-server.cjs and plugin/scripts/worker-service.cjs
- Optionally update plugin/ui/viewer-bundle.js

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.