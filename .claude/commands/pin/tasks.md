---
allowed-tools: Read, Write, Edit, MultiEdit, TodoWrite
description: Generate TDD implementation tasks from design
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Feature: @features/$ARGUMENTS/feature.md
- Requirements: @features/$ARGUMENTS/requirements.md
- Design: @features/$ARGUMENTS/design.md
- Database Schema: @features/$ARGUMENTS/database.md
- API Specification: @features/$ARGUMENTS/api.md
- Frontend Specification: @features/$ARGUMENTS/frontend.md

## Inputs

- $ARGUMENTS: feature id/name (e.g., 001-auth)

## Your Task

Create implementation tasks for: $ARGUMENTS

## Execution Flow
```
1. Load design documents from features/$ARGUMENTS/
   → design.md (required): Extract architecture, shared resources
   → database.md (required): Extract entities, schemas, migrations
   → api.md (required): Extract endpoints, request/response types
   → frontend.md (if web app): Extract components, UI flows, state management
   → requirements.md: Extract user stories, shared dependencies
   → Validate: no [NEEDS CLARIFICATION] markers remain
2. Generate tasks systematically:
   → From database.md: Each entity → model creation task [P]
   → From database.md: Each migration → migration task
   → From api.md: Each endpoint → contract test task [P]
   → From api.md: Each endpoint → implementation task
   → From requirements.md: Each user story → integration test [P]
   → From design.md: Each shared interface → shared resource task
3. Apply ordering rules:
   → Setup → Tests → Models → Services → Endpoints → Polish
   → Tests before implementation (TDD enforcement)
4. Validate parallel tasks ([P]):
   → Check file conflicts: same file = remove [P]
   → Validate dependencies: dependent tasks = remove [P]
   → Auto-fix conflicts and warn
5. Generate dependency graph and critical path
6. Number tasks sequentially with type prefixes
7. Populate tasks.md with generated tasks
8. Initialize execution journal from template
9. Return: SUCCESS (tasks ready for execution)
```

## Steps

1. **Load and Validate Design Documents**
   - Copy template from `@.claude/templates/tasks.md` to `features/$ARGUMENTS/tasks.md`
   - Load design.md, database.md, api.md (all required), requirements.md
   - Verify no [NEEDS CLARIFICATION] markers remain in requirements

2. **Systematic Task Generation from Concrete Artifacts**
   - **From database.md**: Each entity definition → model creation task [P]
   - **From database.md**: Each migration script → migration task
   - **From api.md**: Each endpoint specification → contract test task [P]  
   - **From api.md**: Each endpoint → API implementation task
   - **From requirements.md**: Each user story → integration test [P]
   - **From design.md**: Each shared interface → shared resource task

3. **Apply Systematic Ordering**
   - Phase 1: Setup tasks (project init, dependencies)
   - Phase 2: Test tasks (contract tests, integration tests) 
   - Phase 3: Implementation tasks (models, services, endpoints)
   - Phase 4: Polish tasks (unit tests, performance, docs)

4. **Validate and Fix Parallel Tasks**
   - Scan all [P] tasks for file path conflicts
   - Remove [P] from tasks modifying same files
   - Remove [P] from tasks with dependencies
   - Generate warnings for auto-fixes

5. **Generate Task Structure**
   - Build dependency graph with critical path
   - Number tasks sequentially (task-01, task-02...)
   - Add TDD cycle details for each task
   - Include file paths and acceptance criteria

6. **Populate and Validate**
   - Fill tasks.md with all generated tasks
   - Validate completeness: all contracts/entities/stories covered
   - Generate summary of created tasks

7. **Initialize Execution Journal**
   - Copy `@.claude/templates/journal.md` to `features/$ARGUMENTS/journal.md`
   - Initialize Summary section with feature name, start date, and total task count
   - Prepare journal for execution tracking

## Outputs

- `features/$ARGUMENTS/tasks.md`
- `features/$ARGUMENTS/journal.md`
- Next step: `/pin:align $ARGUMENTS`

## Constitution Gate (Tasks)

- **Concrete Artifact Generation**: Tasks must be generated from concrete artifacts (database.md entities, api.md endpoints, requirements user stories).
- **Required Documents**: STOP if database.md or api.md missing:
  "STOP: Missing concrete artifacts. Run /pin:design first to create database.md and api.md."
- **TDD Enforcement**: Tests MUST precede implementation. Contract tests → Integration → Implementation.
- **File Conflict Detection**: Auto-validate [P] tasks for file conflicts and dependencies.
- **Clarification Check**: STOP if requirements contain [NEEDS CLARIFICATION] markers:
  "STOP: Requirements contain unresolved clarifications. Complete requirements phase first."
- **File‑Conflict Validation**: STOP on any two [P] tasks modifying the same file:
  "STOP: Conflicting [P] tasks on file [file]. Auto-fixed by removing [P] from dependent tasks."
- **Coverage Validation**: STOP if any concrete artifact lacks corresponding tasks:
  "STOP: Incomplete task coverage. Missing tasks for [database entities/API endpoints/user stories]."
- **Ordering Enforcement**: Contract tests → Integration → E2E → Unit → Implementation.
