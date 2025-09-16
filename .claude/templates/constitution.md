# [PROJECT_NAME] Constitution

## Core Principles

### I. Library-First
Every feature is a self-contained library or module that can be independently tested, documented, and reasoned about. Libraries must have a clear purpose; organizational-only wrappers are discouraged unless justified against Simplicity constraints.

### II. Test-First (NON-NEGOTIABLE)
TDD is mandatory: write tests → confirm they fail (RED) → make them pass (GREEN) → refactor for quality (REFACTOR). Commits reflect RED→GREEN ordering. Implementation before failing tests is prohibited.

### III. Integration Testing
Integration tests are required for: new library contracts, any contract changes, inter-service communication, and shared schemas. Prefer real dependencies over mocks in integration tests, with test environments isolated and repeatable.

### IV. Observability
Structured logging is required. Logs must include correlation IDs and sufficient context for triage. Errors follow an explicit taxonomy (Validation, AuthN, AuthZ, NotFound, ServerError) and are serialized consistently. Frontend logs should flow to a unified backend stream when applicable.

### V. Versioning & Breaking Changes
Use SemVer MAJOR.MINOR.BUILD. BUILD increments on any change to behavior, contracts, or performance characteristics. Breaking changes require: deprecation notes, migration steps, parallel contract tests (old vs new) until consumers are updated, and clear release notes.

### VI. Simplicity
Favor defaults and direct usage of frameworks. Avoid unnecessary patterns/wrappers (e.g., Repository/UoW) unless justified with concrete needs. Default to ≤3 top-level projects (e.g., `api`, `web`, `tests`) unless explicitly justified.

### VII. Concrete Artifacts
Features produce concrete specification documents (database.md, api.md, frontend.md) containing implementation-ready schemas, endpoints, and component specifications. Tasks are systematically generated from these concrete artifacts.

## Workflow & Quality Gates

- Plan (Pre-Design Gate)
  - Verify Simplicity limits (≤3 projects) and initial test ordering plan (Contract→Integration→E2E→Unit).
  - Identify all NEEDS CLARIFICATION items and block until resolved or justified.
  - Create shared resource structure and governance documents.
  - STOP if violations exist without justification; else record in Complexity Tracking.

- Design (Post-Design Gate)
  - Concrete artifacts (database.md, api.md, frontend.md as needed) MUST be defined.
  - Contracts, data model, and quickstart MUST be defined.
  - Generate failing contract tests (RED) for each contract; list locations.
  - STOP if concrete artifacts or failing tests are missing.

- Tasks (Planning Gate)
  - Tasks derive systematically from concrete artifacts (database.md entities, api.md endpoints, frontend.md components).
  - Mark [P] only when tasks touch different files and have no dependencies.
  - STOP if [P] tasks conflict on the same file or if tests are not scheduled before implementation.

- Align (Pre-Execution Gate)
  - Ensure requirements ↔ concrete artifacts ↔ tasks traceability is complete.
  - Verify shared resources provider/consumer mapping and contracts.
  - STOP if coverage gaps or contract ambiguities persist.

- Execute (Per-Task Gate)
  - Evidence of RED (failing tests) is required before any implementation.
  - Enforce ordered test priorities: Contract→Integration→E2E→Unit.
  - Implementation must follow concrete specifications (database.md schemas, api.md interfaces).
  - Observability and versioning hooks/checks must be added/updated as code changes.
  - STOP if RED evidence is missing or ordering is violated.

- Complete (Final Gate)
  - All tests pass; coverage on changed lines meets policy.
  - Implementation matches concrete artifact specifications.
  - Observability present with structured logs + error taxonomy.
  - Version bump (at least BUILD), and migration notes if breaking.
  - STOP if any of the above fails.

## Shared Resources

### Structure
- `src/shared/interfaces/` - Cross-feature TypeScript interfaces
- `src/shared/utilities/` - Reusable business logic functions
- `src/shared/database/` - Tables and schemas used by multiple features
- `src/shared/types/` - Common API request/response types

### Governance
- Create shared resources when 2+ features need the same contract
- Provider feature owns the interface definition
- Consumer features import and implement
- Document all shared resources in feature TLDRs

## Governance

- Versioning and Amendments
  - Constitution carries a version: MAJOR.MINOR.BUILD.
  - Amendments follow the "Constitution Update" command (`/pin:constitution`).
  - PRs that touch governance, templates, or command text must verify update steps completion and bump the Constitution version if rules change.

- Verification in PRs
  - PR reviewers verify: gates are satisfied, task ordering is correct, RED evidence exists, observability and versioning requirements are met, and migration notes exist for breaking changes.
  - Deviations must be documented in Complexity Tracking with justification.

**Version**: 1.0.0 | **Ratified**: 2025-09-16 | **Last Amended**: 2025-09-16

---

Based on PINDEX Constitution v1.0.0