---
allowed-tools: Read, Write, Edit, MultiEdit, Grep
description: Apply and validate Constitution updates across commands and templates
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Commands: @.claude/commands/pin/\*
- Templates: @.claude/templates/\*

## Inputs

- $ARGUMENTS: version bump (e.g., 1.0.1) and summary of changes

## Your Task

Update governance and ensure consistency across PINDEX.

## Steps

1. Identify affected areas from Constitution changes (principles, gates, policies)
2. Update templates:
   - `feature.md` (shared resources)
   - `requirements.md` (gates, shared deps, accessibility)
   - `design.md` (contracts, testing, observability)
   - `tasks.md` ([P] rules, test ordering, acceptance criteria)
   - `journal.md` (logging/metrics notes)
   - `tldr.md` (observability/versioning summaries)
3. Update commands if workflow/gates changed:
   - `plan.md`, `requirements.md`, `design.md`, `tasks.md`, `align.md`, `execute.md`, `complete.md`, `tldr.md`, `list.md`, `scaffold.md`
4. Walk a sample feature through all gates to validate RED appears before implementation
5. Bump Constitution version in `constitution.md` and footers referencing the Constitution
6. Produce a concise change log of governance updates

## Outputs

- Updated files across commands/templates
- Version bump applied in `constitution.md`
- Change log summary

## Constitution Gate (Update)

- STOP if any updated rule is not reflected across commands/templates:
  "STOP: Constitution drift detected. Sync all commands/templates with updated rules."
- STOP if RED evidence or ordered testing is weakened anywhere:
  "STOP: Test‑First ordering must remain Contract→Integration→E2E→Unit."
- STOP if version bump is missing after governance changes:
  "STOP: Version bump required. Update Constitution version and footers."
