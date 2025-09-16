---
allowed-tools: Read, Edit, MultiEdit, Grep
description: Validate consistency across all feature documents
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
- Tasks: @features/$ARGUMENTS/tasks.md

## Inputs

- $ARGUMENTS: feature id/name (e.g., 001-auth)

## Your Task

Validate and align all documents for: $ARGUMENTS

## Execution Flow
```
1. Load all feature documents from features/$ARGUMENTS/
   → feature.md, requirements.md, design.md, database.md, api.md, tasks.md (all required)
   → Validate: all documents exist and complete
2. Check requirements coverage:
   → Every requirement ↔ design component ↔ task mapping
   → Identify uncovered requirements or orphaned tasks
3. Validate design consistency:
   → Design components align with architecture/conventions
   → Database.md entities match requirements data needs
   → API.md endpoints match requirements user actions
   → All contracts have corresponding failing tests in tasks
   → Shared resources properly defined (provider/consumer)
4. Verify task completeness:
   → Tasks cover all entities from database.md
   → Tasks cover all endpoints from api.md
   → Tasks cover all user stories from requirements.md
   → Dependencies correct, no circular references
   → [P] markings validated for file conflicts
5. Identify systematic gaps:
   → Error handling, edge cases, performance, security
   → Observability, accessibility, versioning coverage
6. Validate implementation readiness:
   → External dependencies (email, config, migrations)
   → Infrastructure tasks completeness
   → Technical implementation gaps
7. Fix inconsistencies automatically:
   → Renumber, update traceability, align naming
   → Document changes made
8. Generate alignment report:
   → Coverage matrices, gap analysis, next actions
9. Return: SUCCESS/STOP + next command
```

## Steps

1. **Load and Validate Documents**
   - Load all feature documents from `features/$ARGUMENTS/`
   - Validate that feature.md, requirements.md, design.md, tasks.md all exist
   - Check document completeness and format compliance

2. **Check Requirements Coverage**
   - Verify every requirement has corresponding design component and task
   - Identify uncovered requirements or orphaned tasks
   - Validate requirement-to-task traceability

3. **Validate Design Consistency**
   - Ensure design completeness and consistency with architecture/conventions
   - Verify all contracts have corresponding failing tests identified in tasks
   - Validate shared resources (provider/consumer, contracts) across documents

4. **Verify Task Completeness**
   - Check tasks cover all design components and requirements
   - Verify task dependencies are correct with no circular references
   - Validate [P] markings for file conflicts and independence

5. **Identify Systematic Gaps**
   - Check for missing: error handling, edge cases, performance, security
   - Verify observability, accessibility, and versioning coverage
   - Identify missing shared resource contracts

6. **Validate Implementation Readiness**
   - **External Dependencies**: Check for missing infrastructure (email service, database migrations, config files)
   - **Technical Completeness**: Validate authentication flows, token management, security middleware
   - **Environment Setup**: Verify environment variables, secrets management, deployment requirements
   - **Third-party Integrations**: Confirm all external services (SMTP, databases) properly specified
   - **Implementation Gaps**: Identify missing technical details that would block development

7. **Fix Inconsistencies**
   - Automatically fix: renaming, renumbering, traceability issues
   - Update cross-references between documents
   - Document all changes made during alignment

8. **Generate Alignment Report**
   - Create coverage matrices showing requirement→design→task mapping
   - Report gaps and inconsistencies found
   - **Implementation readiness assessment** with specific blockers
   - Provide specific next actions to resolve issues

## Outputs

- Alignment report (inline)
- Next step: `/pin:execute $ARGUMENTS task-01` when aligned

## Constitution Gate (Alignment)

- Full traceability: Every requirement ↔ design component ↔ task.
- Shared Resources: Provider/consumer mapping with explicit contracts present.
- **Implementation readiness**: All external dependencies, infrastructure, and technical details specified.
- STOP if gaps remain:
  "STOP: Alignment gaps detected: [list]. Update documents and re‑run /pin:align."
- STOP if implementation blockers found:
  "STOP: Implementation blockers detected: [list]. Address technical gaps and re‑run /pin:align."
