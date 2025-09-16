---
allowed-tools: Read, Write, Bash, WebSearch, WebFetch, Glob, TodoWrite
description: Analyze a project idea, research architecture, and create feature breakdown
---

## Context

- Constitution Template: @.claude/templates/constitution.md
- Architecture Template: @.claude/templates/architecture.md
- Conventions Template: @.claude/templates/conventions.md
- Feature Template: @.claude/templates/feature.md
- This is PLANNING ONLY. No implementation, no dependencies, no package.json.

## Inputs

- $ARGUMENTS: raw project idea (string)
- User responses to structured questions (if needed)

## Your Task

Analyze and plan the project: $ARGUMENTS

## Execution Flow
```
1. Parse project idea from $ARGUMENTS
   → If empty: ERROR "No project idea provided"
2. Information gathering phase:
   → Ask for: Project name, type, brief description
   → If Greenfield: research stack, features, security
   → If Brownfield: read manifests, analyze structure
3. Analysis and validation:
   → Present overview, findings, proposed features
   → Wait for user confirmation
   → STOP until confirmed (no further actions)
4. Create foundation documents:
   → Copy and customize governance templates (constitution, architecture, conventions)
   → Validate: ≤3 top-level projects, simplicity compliance
5. Create shared resource structure:
   → Create src/shared/interfaces/, src/shared/utilities/, src/shared/database/, src/shared/types/
   → Set up cross-feature resource organization
6. Create feature structure:
   → Generate features/###-name/ folders
   → Populate feature.md from template
   → Validate: all template sections filled
7. Run constitution gate validation
8. Return: SUCCESS (ready for /pin:scaffold)
```

## Steps

1. **Information Gathering**
   - Parse and analyze project idea from $ARGUMENTS
   - Ask for: Project name, type (greenfield/brownfield), brief description
   - If Greenfield: research best practices, features list, stack recommendations, security
   - If Brownfield: read existing manifests; list features and structure

2. **Present Analysis and Get Confirmation**
   - Provide overview, research findings, proposed features, and technology decisions (documentation only)
   - Wait for user confirmation 
   - STOP further actions until user confirms (no automatic progression)

3. **Create Foundation Documentation**
   - Copy `@.claude/templates/constitution.md` and customize with project name, version, and date
   - Copy `@.claude/templates/architecture.md` and populate with technology stack and system design decisions
   - Copy `@.claude/templates/conventions.md` and customize with project-specific naming and workflow conventions
   - Validate constitution compliance during creation

4. **Create Shared Resource Structure**
   - Create `src/shared/interfaces/` directory for cross-feature TypeScript interfaces
   - Create `src/shared/utilities/` directory for reusable business logic functions
   - Create `src/shared/database/` directory for shared tables and schemas
   - Create `src/shared/types/` directory for common API request/response types

5. **Create Feature Structure**
   - Create `features/###-[feature-name]/` folders 
   - Copy contents of `@.claude/templates/feature.md` to newly created feature directories
   - Populate all sections in `feature.md` per template

6. **Validate and Finalize**
   - Run constitution gate checks
   - Validate all required documentation exists
   - Generate next step command

## Outputs

- `architecture.md`, `conventions.md`
- `features/###-name/feature.md` (filled)
- Next step: `/pin:scaffold`

## Constitution Gate (Pre‑Design)

- Simplicity: Confirm ≤3 top‑level projects (e.g., api, web, tests). If more, justify and STOP:
  "STOP: Simplicity violated (top‑level projects > 3). Add justification or reduce scope."
- Testing (NON‑NEGOTIABLE): Define intended test order Contract→Integration→E2E→Unit; plan failing contract tests first.
- NEEDS CLARIFICATION: Extract unknowns; if unresolved, STOP:
  "STOP: Resolve NEEDS CLARIFICATION items before proceeding. List: [items]."

## Next

- If gate passes and user confirms: `/pin:scaffold`
