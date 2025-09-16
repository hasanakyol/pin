# PINDEX

*A comprehensive feature development framework for Claude Code*

## What is PINDEX?

PINDEX (PIN Development Expert) is a Claude Code framework that transforms raw project ideas into production-ready features through systematic planning, concrete specifications, and strict quality gates. 

**Core Philosophy**: Every feature produces concrete, implementation-ready artifacts (database schemas, API specifications, component designs) with systematic task generation and test-first development.

### Key Principles

- **Library-First**: Each feature is a self-contained, testable module
- **Test-First**: RED→GREEN→REFACTOR with enforced ordering (Contract → Integration → E2E → Unit)
- **Concrete Artifacts**: Features generate database.md, api.md, frontend.md with implementation-ready specs
- **Shared Resources**: Systematic cross-feature resource management with provider/consumer contracts
- **Observability**: Structured logging with correlation IDs and explicit error taxonomy
- **Versioning**: SemVer with migration notes for breaking changes
- **Simplicity**: ≤3 top-level projects, direct framework usage

## Installation

Requires [Claude Code](https://claude.ai/code)

```bash
bunx gitpick hasanakyol/pin/tree/main/.claude
# or
npx gitpick hasanakyol/pin/tree/main/.claude
```

## Quick Start

```bash
# 1. Plan your project
/pin:plan "a task management app with user auth and projects"

# 2. Set up project structure  
/pin:scaffold

# 3. Define requirements for first feature
/pin:requirements 001-auth

# 4. Create concrete specifications
/pin:design 001-auth

# 5. Generate implementation tasks
/pin:tasks 001-auth

# 6. Validate alignment
/pin:align 001-auth

# 7. Implement with TDD
/pin:execute 001-auth task-01

# 8. Complete and validate
/pin:complete 001-auth

# 9. Generate documentation
/pin:tldr 001-auth
```

## System Architecture

### PINDEX Framework Structure
What you get when you install PINDEX:
```
.claude/
├── commands/pin/                # Workflow Commands
│   ├── plan.md                  # Project planning and setup
│   ├── scaffold.md              # Project structure creation
│   ├── requirements.md          # EARS requirements gathering
│   ├── design.md                # Concrete artifact generation
│   ├── tasks.md                 # Systematic task generation
│   ├── align.md                 # Document consistency validation
│   ├── execute.md               # TDD implementation cycle
│   ├── complete.md              # Feature completion validation
│   ├── tldr.md                  # Documentation generation
│   ├── list.md                  # Project status overview
│   └── constitution.md          # Governance management
└── templates/                   # Document Templates
    ├── constitution.md          # Project governance template
    ├── architecture.md          # System design template
    ├── conventions.md           # Development conventions template
    ├── feature.md               # Feature overview template
    ├── requirements.md          # EARS requirements template
    ├── design.md                # High-level design template
    ├── database.md              # Database specification template
    ├── api.md                   # API specification template
    ├── frontend.md              # Frontend specification template
    ├── tasks.md                 # Implementation tasks template
    ├── journal.md               # Execution tracking template
    └── tldr.md                  # Documentation summary template
```

### Your Project Structure
What your project looks like after using PINDEX:
```
your-project/
├── constitution.md              # Project governance (from template)
├── architecture.md              # System design (from template)  
├── conventions.md               # Development conventions (from template)
├── src/                         # Your application code
│   ├── src/shared/              # Cross-feature code
│   │   ├── interfaces/          # TypeScript contracts
│   │   ├── utilities/           # Reusable functions
│   │   ├── database/            # Shared schemas
│   │   └── types/               # Common API types
│   ├── auth/                    # Feature implementation code
│   └── projects/                # Another feature implementation
├── tests/                       # Your test suites
└── features/                    # Feature documentation
    └── 001-auth/                # Example feature
        ├── feature.md           # Business overview
        ├── requirements.md      # EARS format requirements
        ├── design.md            # High-level architecture
        ├── database.md          # Concrete SQL schemas
        ├── api.md               # Concrete API specifications
        ├── frontend.md          # Concrete component specs (if applicable)
        ├── tasks.md             # Generated implementation tasks
        ├── journal.md           # Execution tracking
        └── tldr.md              # Summary for other teams
```

**Note**: The `.claude/` directory contains the PINDEX framework and is automatically available in Claude Code. Your project focuses on the actual implementation and documentation.

### Concrete Artifacts System

**database.md** - Implementation-ready database specifications:
```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);
```

**api.md** - Complete API specifications with TypeScript interfaces:
```typescript
interface CreateUserRequest {
  email: string;
  password: string;
}

interface UserResponse {
  id: string;
  email: string;
  created_at: string;
}
```

**frontend.md** - Component specifications and UX flows:
```typescript
interface UserProfileProps {
  user: User;
  onUpdate: (user: User) => void;
}
```

## Workflow Overview

### 1) Plan
```bash
/pin:plan "project idea"
```
**Outputs:** 
- `constitution.md` - Project governance rules
- `architecture.md` - System design decisions  
- `conventions.md` - Development standards
- `src/shared/` directories for cross-feature resources
- `features/###-name/feature.md` - Feature overviews

**Gates:** Simplicity (≤3 projects), test ordering, unresolved clarifications

### 2) Scaffold
```bash
/pin:scaffold
```
**Outputs:** Project folders, configs, scripts (no implementation code)

**Gates:** No implementation beyond structure

### 3) Requirements
```bash
/pin:requirements 001-auth
```
**Outputs:** `requirements.md` with testable acceptance criteria

**Gates:** Non-testable requirements, unresolved [NEEDS CLARIFICATION] markers

### 4) Design
```bash
/pin:design 001-auth
```
**Outputs:**
- `design.md` - High-level architecture and integration points
- `database.md` - SQL schemas, indexes, migrations  
- `api.md` - TypeScript interfaces, endpoint specifications
- `frontend.md` - Component specs and UX flows (if applicable)

**Gates:** Missing concrete artifacts, undefined contracts

### 5) Tasks
```bash
/pin:tasks 001-auth
```
**Outputs:** `tasks.md` with TDD tasks, dependencies, [P] parallel markers

**Task Generation:**
- Each database entity → model creation task
- Each API endpoint → contract test + implementation task  
- Each frontend component → component implementation task
- Each user story → integration test task

**Gates:** File conflicts in [P] tasks, tests not scheduled before implementation

### 6) Align
```bash
/pin:align 001-auth
```
**Outputs:** Alignment report, fixed inconsistencies

**Gates:** Missing requirement→design→task traceability, contract gaps

### 7) Execute
```bash
/pin:execute 001-auth task-01
```
**TDD Enforcement:**
1. **RED**: Write failing tests first (validated)
2. **GREEN**: Implement following concrete specifications  
3. **REFACTOR**: Improve code quality

**Outputs:** Source changes, tests, updated `journal.md`

**Gates:** Missing RED evidence, test ordering violations, no concrete spec compliance

### 8) Complete
```bash
/pin:complete 001-auth
```
**Validation:**
- All tasks complete
- Tests pass with ≥90% coverage on changed files
- Implementation matches concrete specifications
- Observability and versioning requirements met

**Outputs:** Validation report, commit message, migration notes

### 9) TLDR
```bash
/pin:tldr 001-auth
```
**Outputs:** `tldr.md` with contracts, shared resources, usage examples

## Quality Gates & Governance

### Constitution-Based Gates
Every command enforces quality gates that prevent progression with incomplete work:

- **NEEDS CLARIFICATION**: All ambiguities must be resolved
- **Test-First**: Tests must precede implementation  
- **Concrete Artifacts**: Implementation specs must be complete
- **Shared Resources**: Provider/consumer contracts must be explicit
- **Coverage**: ≥90% on changed files with diff-aware measurement
- **Observability**: Structured logging and error taxonomy required

### Shared Resources Management

**Provider/Consumer Model:**
- Provider features own shared interface definitions
- Consumer features import and implement contracts
- All shared resources documented in feature TLDRs
- Changes coordinated through migration notes

**Organization:**
```
src/shared/interfaces/IUserAuth.ts     # Authentication contract
src/shared/utilities/validation.ts     # Common validation functions  
src/shared/database/shared_users.sql   # User table schema
src/shared/types/UserTypes.ts          # User API types
```

## Testing Strategy

### Ordered Test Priorities
1. **Contract Tests**: API/interface compliance (generated per endpoint)
2. **Integration Tests**: User journey validation (generated per story)  
3. **E2E Tests**: Critical path validation
4. **Unit Tests**: Local logic validation

### Test Generation
Tasks are systematically generated from concrete artifacts:
- `api.md` endpoints → contract test files
- `requirements.md` user stories → integration test scenarios
- Component specifications → frontend test cases

## Advanced Features

### Parallel Task Execution
Tasks marked `[P]` can run in parallel when they:
- Modify different files
- Have no dependencies
- Don't conflict on shared resources

### Error Taxonomy
Consistent error handling across all features:
- **Validation**: Input validation failures (400)
- **AuthN**: Authentication required (401)  
- **AuthZ**: Access denied (403)
- **NotFound**: Resource not found (404)
- **ServerError**: Internal failures (500)

### Observability Integration
Built-in structured logging with:
- Correlation ID propagation
- Context-aware error messages
- Performance metrics collection
- Error taxonomy mapping

## Contributing

PINDEX follows its own development methodology:

1. Use `/pin:plan` for new features
2. Follow the complete workflow for all changes
3. Maintain test-first discipline
4. Update constitution version for governance changes

## License

MIT - Use freely for any project.

---

*Based on PINDEX Constitution v1.0.0*
