---
allowed-tools: Read, Write, Edit, MultiEdit
description: Generate comprehensive TLDR summary for LLM agents
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Feature documents: @features/$ARGUMENTS/feature.md
- Requirements: @features/$ARGUMENTS/requirements.md
- Design: @features/$ARGUMENTS/design.md
- Database Schema: @features/$ARGUMENTS/database.md
- API Specification: @features/$ARGUMENTS/api.md
- Frontend Specification: @features/$ARGUMENTS/frontend.md
- Tasks: @features/$ARGUMENTS/tasks.md
- Journal: @features/$ARGUMENTS/journal.md
- TLDR: @.claude/templates/tldr.md
- Previous features: !`find features -type d -name "0*" | grep -v $ARGUMENTS | sort`

## Inputs

- $ARGUMENTS: feature id/name (e.g., 001-auth)

## Your Task

Generate TLDR summary for feature: $ARGUMENTS

## Steps

1. Read all feature documents
2. Read prior TLDRs for dependencies and interfaces
3. Use the template from @.claude/templates/tldr.md; fill all sections with actual data
4. Ensure clarity, explicit references, and self‑containment
5. Save to `features/$ARGUMENTS/tldr.md`
6. Print Next step

## Outputs

- `features/$ARGUMENTS/tldr.md` ready for other agents
- Next step: `/pin:requirements [next-feature-number]-[feature-name]`

## Constitution Gate (TLDR)

- Include: contracts (provided/consumed), observability practices, coverage %, version bumped, and migration notes.
- STOP if missing:
  "STOP: TLDR incomplete. Add contracts/shared sections, coverage, and version details."
