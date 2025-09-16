---
allowed-tools: Read, Glob
description: List all features and their task statuses
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Features directory: @features/
- All feature journals: !`find features -name "journal.md" -exec echo {} \;`

## Inputs

- $ARGUMENTS: optional filters (`--feature`, `--status`, `--verbose`)

## Your Task

List all features and their implementation status.

## Steps

1. Scan features directory; sort folders numerically
2. Read `feature.md`, `tasks.md`, `journal.md` per feature
3. Generate status report with completion percentages
4. Detect issues (missing req/design, orphaned tasks, stalled updates)
5. Print one prioritized next action

## Status indicators

- Task status: [COMPLETE], [PENDING], [FAILED], [IN_PROGRESS]
- Feature status: [COMPLETE], [IN PROGRESS], [PENDING], [NOT STARTED]

## Constitution Indicators

- Missing RED evidence → "Needs tests‑first"
- [P] conflicts → "Resolve conflicting [P] tasks"
- Missing observability/versioning → "Add logs/version bump"
- CLI violations → "Fix CLI flags/outputs per conventions"
- Branch mismatch → "Align branch name with features/###-name"

## Output

- Summary table and indicators
- Single recommended next step that addresses the most critical violation
