---
allowed-tools: Read, Write, Edit, MultiEdit, Glob
description: Define feature requirements in EARS format
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Feature overview: @features/$ARGUMENTS/feature.md
- Previous features (if any): !`find features -name "tldr.md" -exec echo {} \; 2>/dev/null || echo "No completed features yet"`

## Inputs

- $ARGUMENTS: feature id/name (e.g., 001-auth)

## Your Task

Create detailed requirements for feature: $ARGUMENTS

## Execution Flow
```
1. Ensure `features/$ARGUMENTS/requirements.md` exists by copying template
   → Initialize Clarification Status section
2. Read foundation documents and feature overview
   → Extract key concepts and actors
3. For each unclear aspect in feature overview:
   → Mark with [NEEDS CLARIFICATION: specific question]
   → Update Clarification Status counter
4. Review previous TLDRs for shared interfaces/utilities
5. Identify shared dependencies (provider/consumer, contracts)
6. Write 5–10 functional requirements in strict EARS format
   → Each requirement must be testable and measurable
   → Mark ambiguous requirements with [NEEDS CLARIFICATION]
7. Write non‑functional requirements (WCAG 2.2 AA, security, performance)
8. Run automated validation:
   → Count [NEEDS CLARIFICATION] markers
   → Validate EARS format compliance
   → Check requirement testability
9. Update Clarification Status:
   → If clarifications exist: Status = PENDING CLARIFICATION
   → If none: Status = CLARIFIED
10. Return status: SUCCESS/NEEDS_CLARIFICATION
```

## Steps

1. **Initialize Requirements Document**
   - Copy `@.claude/templates/requirements.md` to `features/$ARGUMENTS/requirements.md`
   - Set initial clarification counters to 0

2. **Gather and Analyze Information**
   - Read foundation documents and the feature overview
   - Review previous TLDRs for shared interfaces/utilities
   - Extract actors, actions, data, and constraints

3. **Mark Ambiguities Systematically**
   - For each unclear aspect, add [NEEDS CLARIFICATION: specific question]
   - Common ambiguous areas: user types, data retention, performance targets, error handling, security requirements
   - Don't make assumptions - mark uncertainties explicitly

4. **Generate Requirements**
   - Write 5–10 functional requirements in strict EARS format
   - Write non‑functional requirements including WCAG 2.2 AA, security, performance, reliability
   - Each requirement must be testable and measurable
   - Mark any ambiguous requirements

5. **Automated Validation**
   - Count total [NEEDS CLARIFICATION] markers
   - Validate EARS format compliance
   - Verify each requirement has testable acceptance criteria
   - Update Clarification Status section

6. **Finalize Document**
   - Fill in shared dependencies (provider/consumer, contracts)
   - Update status based on clarification count
   - Generate next step command

## Outputs

- `features/$ARGUMENTS/requirements.md`
- Next step: `/pin:design $ARGUMENTS`

## Constitution Gate (Requirements)

- EARS is mandatory; each requirement MUST be testable and measurable.
- Clarification Tracking: All [NEEDS CLARIFICATION] markers must be resolved before proceeding.
- Shared Dependencies: For cross‑feature needs, add REQ‑SHARED‑XXX with provider/consumer and contract notes.
- Accessibility: Include WCAG 2.2 AA acceptance criteria.
- STOP on unclear requirements:
  "STOP: [X] clarifications needed. Resolve [NEEDS CLARIFICATION] markers before proceeding to design."
- STOP on non‑testable requirements:
  "STOP: Non‑testable requirements found. Add acceptance criteria and test scenarios."
