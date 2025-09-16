---
allowed-tools: Read, Write, Edit, MultiEdit, Bash, TodoWrite, Grep
description: Implement feature using TDD cycle (RED-GREEN-REFACTOR)
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Current task: @features/$ARGUMENTS/tasks.md
- Design: @features/$ARGUMENTS/design.md
- Database Schema: @features/$ARGUMENTS/database.md
- API Specification: @features/$ARGUMENTS/api.md
- Frontend Specification: @features/$ARGUMENTS/frontend.md
- Requirements: @features/$ARGUMENTS/requirements.md
- Journal: @features/$ARGUMENTS/journal.md

## Inputs

- $ARGUMENTS: "feature-id task-id" (e.g., "001-auth task-01")

## Your Task

Execute task using TDD: $ARGUMENTS

## Execution Flow
```
1. Load task details from features/$ARGUMENTS/tasks.md
   → Parse task ID, type, dependencies, file paths
   → Validate task exists and status is PENDING
   → Load concrete specs: database.md, api.md for implementation reference
2. Verify prerequisites:
   → Dependencies marked [COMPLETE]
   → Required files exist; shared utilities available
3. TDD Phase Validation:
   → If task type = test: Enforce RED phase
   → If task type = implementation: Validate tests exist and FAIL
   → Auto-detect test files for implementation tasks
4. Execute TDD Cycle:
   → RED: Write/run failing tests; confirm failure count > 0
   → GREEN: Implement minimum code; run tests until pass
   → REFACTOR: Improve code; maintain passing tests
5. Validate completion:
   → All tests pass; no lint/type errors
   → File changes align with task specification
6. Update tracking:
   → Mark task [COMPLETE] in tasks.md
   → Update journal.md with detailed notes
7. Return: SUCCESS + next task/complete command
```

## Steps

1. **Load and Validate Task**
   - Parse task details from `features/$ARGUMENTS/tasks.md`
   - Verify task exists and has status [PENDING] or [IN_PROGRESS]
   - Load execution journal from `features/$ARGUMENTS/journal.md`
   - Extract task type, dependencies, files, and shared resource role
   - Load concrete specifications: `database.md` and `api.md` for implementation reference

2. **Verify Prerequisites**
   - Check all dependency tasks marked [COMPLETE]
   - Verify required files exist and shared utilities available
   - For shared resources: validate existing or prepare to create as provider

3. **Task Type Validation and TDD Enforcement**
   - **Parse Task Type**: Extract "Type" and "TDD Required" fields from task definition
   - **For Infrastructure Tasks (TDD Required: No)**: Skip TDD enforcement, validate against specifications
   - **For Behavior Tasks (TDD Required: Yes)**: Enforce full TDD cycle
     - Test Tasks: Must write failing tests first (RED phase)
     - Implementation Tasks: Must have existing failing tests
     - Auto-detect corresponding test files based on implementation paths
     - Validate tests actually FAIL before allowing implementation

4. **Execute Implementation Cycle**

   **For Behavior Tasks (TDD Required: Yes):**
   - **RED Phase**: Write failing tests first; run to confirm failure; output failure count
   - **GREEN Phase**: Implement minimum code following concrete specifications
     - Model tasks: Follow `database.md` entity schemas and field definitions
     - API tasks: Follow `api.md` endpoint specifications and request/response types
     - Focus on functionality; keep tests passing
   - **REFACTOR Phase**: Improve naming/structure/types; confirm tests pass

   **For Infrastructure Tasks (TDD Required: No):**
   - **Implementation Phase**: Create infrastructure following concrete specifications
     - Database tasks: Execute SQL from `database.md` schemas
     - Setup tasks: Follow configuration requirements from design documents
     - Validate setup works correctly without requiring test-first approach

5. **Validate and Complete**
   - Run full test suite, lint, and type checks
   - Verify requirements coverage and acceptance criteria met
   - Ensure file changes align with task specification

6. **Update Tracking**
   - Mark task [COMPLETE] in tasks.md
   - Update `journal.md` with structured details (files, why, tests, coverage, notes)
   - Handle failures: mark [FAILED] and document; prompt user for next action

7. **Generate Next Step**
   - Print next task command or `/pin:complete` if all tasks done

## Outputs

- Source changes + tests
- `journal.md` updated with coverage and notes
- Next step message

## Constitution Gate (Execution per Task)

- **Task Type Detection**: Parse task "Type" and "TDD Required" fields to determine execution approach.
- **TDD Phase Validation**: Enforce TDD only for Behavior Tasks (TDD Required: Yes).
- **Infrastructure Task Validation**: For Infrastructure Tasks, validate against concrete specifications without requiring tests.
- **RED Evidence**: For Behavior Tasks only, provide test files and confirm they FAIL before implementation.
- **Test Existence Check**: For Behavior implementation tasks, validate corresponding test files exist and fail.
- **Ordered Tests**: Contract→Integration→E2E→Unit before GREEN phase (Behavior Tasks only).
- **Observability**: Add structured logs + error taxonomy placements where code paths changed.
- **Versioning**: For contract changes, note intended version bump (≥ BUILD) and draft migration notes.
- **STOP on missing TDD for Behavior Tasks**:
  "STOP: Behavior task attempted without existing failing tests. Write tests first."
- **STOP on missing RED for Behavior Tasks**:
  "STOP: No failing tests detected for Behavior task. Write and run tests (RED) before implementing."
- **STOP on passing tests for Behavior Tasks**:
  "STOP: Tests already pass for Behavior task. Implementation may be unnecessary or tests insufficient."
- **STOP on ordering violations**:
  "STOP: Tests must be authored and executed in order: Contract→Integration→E2E→Unit before implementation."
- **STOP on dependency violations**:
  "STOP: Task dependencies not met. Complete prerequisite tasks: [list]."
