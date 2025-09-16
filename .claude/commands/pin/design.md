---
allowed-tools: Read, Write, Edit, MultiEdit, Glob
description: Create technical design for feature implementation
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Feature: @features/$ARGUMENTS/feature.md
- Requirements: @features/$ARGUMENTS/requirements.md
- Database Template: @.claude/templates/database.md
- API Template: @.claude/templates/api.md
- Frontend Template: @.claude/templates/frontend.md
- Design Template: @.claude/templates/design.md
- Existing shared code: !`find shared -type f -name "*.ts" -o -name "*.js" 2>/dev/null || echo "No shared code yet"`

## Inputs

- $ARGUMENTS: feature id/name (e.g., 001-auth)

## Your Task

Design the technical implementation for: $ARGUMENTS

## Execution Flow
```
1. Load requirements from features/$ARGUMENTS/requirements.md
   → Validate: no [NEEDS CLARIFICATION] markers remain
   → Extract: entities, endpoints, user stories, constraints
2. Initialize design document:
   → Copy @.claude/templates/design.md if needed
   → Extract shared dependencies from requirements
3. Generate technical design:
   → Map requirements to components and data needs
   → Design database schema, API layer, component architecture
   → Define integration points and shared resources
4. Create concrete specification documents:
   → Copy database.md and api.md templates
   → For web apps: Copy frontend.md template
   → Extract entities → populate database.md with SQL schemas
   → Extract endpoints → populate api.md with TypeScript interfaces
   → Extract UI flows → populate frontend.md with component specs
5. Create required design sections:
   → Contracts (reference api.md endpoints)
   → Data Model (reference database.md schemas)
   → Quickstart section with setup instructions
6. Plan additional aspects:
   → Performance optimizations, security, observability
   → Testing approach (Contract→Integration→E2E→Unit)
7. Validate completeness:
   → All requirements covered by concrete artifacts
   → All contracts have failing test placeholders
   → Shared resources explicitly defined
7. Return: SUCCESS (ready for /pin:tasks)
```

## Steps

1. **Load and Validate Requirements**
   - Load requirements from `features/$ARGUMENTS/requirements.md`
   - Validate no [NEEDS CLARIFICATION] markers remain
   - Extract entities, endpoints, user stories, and constraints

2. **Initialize Design Document**
   - Ensure `features/$ARGUMENTS/design.md` exists by copying `@.claude/templates/design.md` if needed
   - Extract shared dependencies from requirements

3. **Generate Core Technical Design**
   - Map requirements to components and data needs; determine integration points
   - Design database schema (tables, indexes, migrations)
   - Design API layer (endpoints, schemas, error responses, rate‑limits)
   - Design component architecture (frontend hierarchy, state management, events)

4. **Create Concrete Specification Documents**
   - Copy `@.claude/templates/database.md` to `features/$ARGUMENTS/database.md`
   - Copy `@.claude/templates/api.md` to `features/$ARGUMENTS/api.md`
   - For web applications: Copy `@.claude/templates/frontend.md` to `features/$ARGUMENTS/frontend.md`
   - Extract entities from requirements → populate database.md with actual SQL schemas
   - Extract user actions from requirements → populate api.md with specific endpoints
   - Extract UI flows from requirements → populate frontend.md with component specifications
   - Generate TypeScript interfaces for all data types

5. **Create Required Design Sections**
   - **Contracts**: Reference concrete endpoints from api.md with failing test file references
   - **Data Model**: Reference concrete schemas from database.md
   - **Quickstart**: Setup and usage instructions

6. **Plan Supporting Systems**
   - Define integration points and Shared Resources (provided/consumed) with explicit contracts
   - Plan performance optimizations (caching, queries, lazy loading, CDN)
   - Design security (authN/Z, validation, encryption)
   - Define testing approach (Contract/Integration/E2E/Unit priorities)

7. **Complete and Validate Design**
   - Update `design.md` with architecture diagrams, deployment/rollback, Shared Resources
   - Reference concrete artifacts: database.md for schema, api.md for endpoints
   - Validate all requirements have corresponding design components in concrete files
   - Ensure all contracts identify failing tests to be written

## Outputs

- `features/$ARGUMENTS/design.md`
- `features/$ARGUMENTS/database.md`
- `features/$ARGUMENTS/api.md`
- `features/$ARGUMENTS/frontend.md`
- Next step: `/pin:tasks $ARGUMENTS`

## Constitution Gate (Design)

- REQUIRED: Contracts, Data Model section, and Quickstart section in `design.md`.
- For each contract, list failing test file(s) to be authored in Tasks (RED phase).
- Integration‑First: Identify integration tests for new/changed contracts.
- STOP if missing:
  "STOP: Contracts and Data Model/Quickstart sections must be defined before proceeding to tasks."
