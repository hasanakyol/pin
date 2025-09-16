# [PROJECT_NAME] Architecture

## System Overview
- **Purpose**: [Brief description of what this system does]
- **Scope**: [What's included and what's not]
- **High‑level component boundaries**: [Major system divisions]
- **Component responsibilities**: [What each major component handles]

## Technology Stack (with rationale)
- **Language/Runtime**: [Language and version with reasoning]
- **Web/API frameworks**: [Framework choices and why]
- **Data storage**: [Database/storage choices and rationale]
- **Messaging/Events**: [Event system if applicable]
- **Build/Test/CI**: [Build pipeline and testing tools]

## Scaffold Configuration
*Machine-readable section for project setup*
- **Language**: [e.g., TypeScript, JavaScript, Python, Go]
- **Runtime**: [e.g., Node.js 18+, Python 3.11+, Go 1.21+]
- **Package Manager**: [e.g., npm, yarn, pnpm, pip, go mod]
- **Framework**: [e.g., Express.js, FastAPI, Gin, Next.js]
- **Database**: [e.g., PostgreSQL, MySQL, MongoDB, SQLite]
- **Build Tool**: [e.g., Vite, Webpack, esbuild, Rollup]
- **Test Framework**: [e.g., Jest, Vitest, pytest, go test]
- **Project Structure**: [e.g., monorepo, single, microservices]

## Component Architecture
- **Modules/libraries and their contracts**: [Internal component interfaces]
- **Shared resources**: providers and consumers (explicit mapping)
- **Data flow and key integration points**: [How data moves through system]

## Shared Resources Architecture

### Directory Structure
```
src/shared/
├── interfaces/      # Cross-feature TypeScript interfaces
├── utilities/       # Reusable business logic functions  
├── database/        # Tables and schemas used by multiple features
└── types/           # Common API request/response types
```

### Resource Categories
- **Interfaces**: TypeScript contracts shared between features
- **Utilities**: Pure functions usable across features
- **Database**: Shared tables, views, stored procedures
- **Types**: Common data structures for API requests/responses

### Provider/Consumer Model
- **Provider Features**: Own and maintain shared resource definitions
- **Consumer Features**: Import and use shared resources
- **Contracts**: Explicit interfaces documented in provider's design.md

## Security Architecture
- **Authentication/Authorization model**: [How users are authenticated and authorized]
- **Input validation and sanitization**: [Validation strategy]
- **Secrets management**: [How secrets are stored and accessed]

## Observability Standards
- **Structured logging with correlation IDs**: [Logging format and correlation strategy]
- **Error taxonomy**: Validation, AuthN, AuthZ, NotFound, ServerError
- **Logging sinks and retention expectations**: [Where logs go and how long kept]
- **Metrics/SLIs/alerts**: [Key metrics to track, platform‑agnostic]

## Performance
- **Target latencies/throughput (P95)**: [Performance goals]
- **Caching strategy and TTLs**: [What's cached and for how long]
- **Indexing and query performance goals**: [Database performance targets]

## Deployment & Operations
- **Environments and promotion flow**: [Dev → staging → prod pipeline]
- **Feature flags and rollbacks**: [How features are controlled and rolled back]
- **Backups and migration plans**: [Data protection and schema evolution]

## Testing Topology
- **Contract and Integration test surfaces**: [Integration‑First approach]
- **E2E critical journeys**: [Key user flows to test end-to-end]
- **Unit tests for local logic**: [What gets unit tested]

## Feature Implementation Model
- **Concrete Artifacts**: Features generate database.md, api.md, frontend.md with implementation-ready specifications
- **Task Generation**: Tasks systematically generated from concrete artifacts
- **Shared Resource Integration**: Features reference and extend shared resources as needed

---

Based on PINDEX Constitution v1.0.0