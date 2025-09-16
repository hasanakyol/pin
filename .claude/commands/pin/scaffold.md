---
allowed-tools: Bash, Read, Write, Glob
description: Intelligently scaffold project structure based on planned features and architecture
---

## Context

- Constitution: @constitution.md
- Architecture: @architecture.md
- Conventions: @conventions.md
- Features: @features/\*/feature.md

## Inputs

- $ARGUMENTS: optional flags (e.g., `--single`, `--monorepo`) – defaults come from docs

## Your Task

Scaffold the project structure: $ARGUMENTS

## Steps

1. Validate prerequisites (architecture.md, conventions.md exist)
2. Read decisions from architecture.md "Scaffold Configuration" section: language, runtime, package manager, framework, database, build tool, test framework, project structure
3. Analyze features: list `features/*/feature.md`
4. Detect project type (greenfield vs brownfield)
5. Create structure
   - Greenfield: initialize, add minimal dev dependencies, create directories, configs, scripts
   - Brownfield: preserve existing, add only missing elements (non‑destructive)
6. Setup scripts: dev/build/test/lint/format
7. Generate report: structure, dependencies installed, configs created, setup steps, next command

## Outputs

- Project folders/configs/scripts created or updated (no feature code)
- Report with next step: `/pin:requirements 001-[first-feature]`

## Constitution Gate (Scaffold Scope)

- Planning decisions must be documented in `architecture.md` and `conventions.md`.
- Implementation is disallowed here; only structure/configs/scripts.
- If `features/*/feature.md` missing: WARN and continue (do not STOP).
- STOP on implementation attempt:
  "STOP: Implementation is disallowed in scaffold. Proceed to /pin:requirements and /pin:design first."
