---
allowed-tools: Read, Write, Edit, Bash, TodoWrite
description: Validate feature completion and prepare for commit
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Feature Journal: @features/$ARGUMENTS/journal.md
- Tasks: @features/$ARGUMENTS/tasks.md
- Requirements: @features/$ARGUMENTS/requirements.md
- Database Schema: @features/$ARGUMENTS/database.md
- API Specification: @features/$ARGUMENTS/api.md
- Frontend Specification: @features/$ARGUMENTS/frontend.md
- Current git status: !`git status --short`
- Current branch: !`git branch --show-current`

## Inputs

- $ARGUMENTS: feature id/name (e.g., 001-auth)

## Your Task

Complete and validate feature: $ARGUMENTS

## Execution Flow
```
1. Load feature documents from features/$ARGUMENTS/
   → tasks.md, journal.md, requirements.md, database.md, api.md (all required)
   → Validate: all documents exist and accessible
2. Verify task completion:
   → All tasks marked [COMPLETE], none [FAILED]/[IN_PROGRESS]
   → Journal entries align with task status
3. Run comprehensive validation:
   → Execute full test suite; capture passing count
   → Compute diff-aware coverage on changed files (≥90%)
   → Run lint, type, security checks
4. Validate requirements coverage:
   → All acceptance criteria met
   → Generate coverage matrix: requirement→test→passing
5. Validate implementation against specifications:
   → Database implementation matches database.md schemas
   → API implementation matches api.md endpoint specifications
   → Entity models reflect database.md field definitions
   → API responses match api.md TypeScript interfaces
6. Validate shared resources:
   → Created/consumed resources match contracts
   → Integration tests validate shared interfaces
7. Generate completion artifacts:
   → Update journal with completion summary
   → Generate commit message with version bump
   → Create migration notes if breaking changes
8. Final gate validation:
   → Coverage ≥90%, observability implemented, version bumped
   → Branch name matches feature folder
   → Implementation matches concrete specifications
9. Return: SUCCESS + next step/STOP + failure details
```

## Steps

1. **Load and Validate Feature State**
   - Load feature documents from `features/$ARGUMENTS/`
   - Verify tasks.md, journal.md, requirements.md exist and are accessible
   - Check current git status and branch alignment

2. **Verify Task Completion**
   - Verify all tasks are [COMPLETE] in `tasks.md`/`journal.md`, none [FAILED]/[IN_PROGRESS]
   - Validate journal entries align with task completion status
   - Check that all implementation matches task specifications

3. **Run Comprehensive Testing and Quality Checks**
   - Run comprehensive tests; capture total passing count
   - Compute diff‑aware coverage on changed files (target ≥90%)
   - Run code quality checks (lint, type, security) and generate reports

4. **Validate Requirements and Acceptance**
   - Validate requirements coverage and acceptance criteria fulfillment
   - Generate coverage matrix: requirement→design→task→test→passing
   - Verify all user stories have corresponding passing tests

5. **Validate Shared Resources and Integration**
   - Validate shared resources (created/consumed, contracts match, tested)
   - Ensure integration tests validate shared interfaces
   - Verify observability and versioning requirements met

6. **Generate Completion Artifacts**
   - Update Journal with completion summary and lessons learned
   - Generate commit message with appropriate version bump
   - Create migration notes if breaking changes detected

7. **Final Validation and Next Steps**
   - Run final constitution gate checks
   - Suggest git commands (only if all checks pass)
   - Generate next step command or detailed failure report

## Outputs

- Final validation summary, commit message suggestion, next command

## Constitution Gate (Final)

- Coverage (diff‑aware): ≥90% statements/branches/functions on changed files; changed lines + impacted functions covered.
- Observability: Structured logs + correlation IDs + error taxonomy implemented in changed paths.
- Versioning: Version bump applied (SemVer; at least BUILD). For breaking changes: migration notes and parallel contract tests validated.
- Branch discipline: Current branch matches `features/###-name` folder.
- STOP on any failure:
  "STOP: Final gate failed: [coverage/observability/version/migration notes/branch]. Address and re‑run /pin:complete."
