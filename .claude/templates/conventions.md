# [PROJECT_NAME] Conventions

## Versioning Policy (SemVer MAJOR.MINOR.BUILD)
- BUILD increments on any behavior change (including performance or contract changes)
- MINOR adds backward‑compatible features
- MAJOR introduces breaking changes and requires migration notes + parallel contract tests (old vs new)

## Branch Discipline
- Feature branches: `features/###-name` (e.g., `features/001-auth`)
- One feature per branch; must map to folder `features/###-name/`

## Feature Folder Norms
- `features/###-name/feature.md`
- `requirements.md`, `design.md`, `database.md`, `api.md`, `frontend.md` (as needed), `tasks.md`, `journal.md`, `tldr.md`
- Concrete artifacts contain implementation-ready specifications

## Shared Resource Conventions

### When to Create Shared Resources
- **Interface**: When 2+ features need the same contract or data structure
- **Utility**: When 2+ features need the same business logic function
- **Database**: When multiple features access the same table or need common schemas
- **Types**: When multiple features use the same API request/response structures

### Naming Conventions
- **Interfaces**: `I[FeatureName][Purpose]` (e.g., `IUserAuth`, `IPaymentProcessor`)
- **Utilities**: `[domain][Action]` (e.g., `validateEmail`, `formatCurrency`)
- **Database**: `shared_[table_name]` for shared tables
- **Types**: `[Domain][Type]` (e.g., `UserRequest`, `PaymentResponse`)

### Provider/Consumer Model
- **Provider Feature**: Creates and owns the shared resource definition
- **Consumer Features**: Import and implement the shared resource
- **Documentation**: Provider documents interface in their `design.md` and `tldr.md`
- **Changes**: Provider coordinates breaking changes with all consumers

### File Organization
```
src/shared/
├── interfaces/
│   ├── IUserAuth.ts          # User authentication contract
│   └── IPaymentProcessor.ts  # Payment processing contract
├── utilities/
│   ├── validation.ts         # Common validation functions
│   └── formatting.ts         # Data formatting helpers
├── database/
│   ├── shared_users.sql      # User table used by multiple features
│   └── shared_audit.sql      # Audit logging table
└── types/
    ├── UserTypes.ts          # User-related API types
    └── PaymentTypes.ts       # Payment-related API types
```

## Test-Driven Development (Test‑First)
- RED evidence before implementation
- Ordered priorities: Contract → Integration → E2E → Unit
- Commit/order must reflect RED→GREEN→REFACTOR

## Coverage Policy
- Scope: Changed lines + impacted functions
- Thresholds: ≥90% statements, ≥90% branches, ≥90% functions on changed files
- Evidence: Diff‑aware coverage report validated in `/pin:complete`

## Observability
- Structured logs with correlation IDs; context propagation across boundaries
- Error taxonomy: Validation, AuthN, AuthZ, NotFound, ServerError
- Logs redact sensitive data; follow principle of least data
- Observability hooks updated when code paths change

## Accessibility (WCAG 2.2 AA)
- Keyboard navigable, contrast ≥ 4.5:1, correct ARIA roles/labels, screen reader flows

## Simplicity
- ≤3 top‑level projects unless justified (e.g., `api`, `web`, `tests`)
- Avoid unnecessary wrappers; prefer direct framework usage
- Prefer feature-specific code over premature abstraction

## [P] Parallelization Rules
- Allowed only when tasks modify different files and have no dependencies
- STOP on same‑file modification conflicts; merge or re‑sequence

## Concrete Artifacts
- **database.md**: Contains implementation-ready SQL schemas, indexes, migrations
- **api.md**: Contains TypeScript interfaces and endpoint specifications
- **frontend.md**: Contains component specifications and UX flows
- Tasks generated systematically from these concrete artifacts

---

Based on PINDEX Constitution v1.0.0