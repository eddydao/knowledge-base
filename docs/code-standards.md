# Code Standards

## Core Principles
- **KISS**: Keep It Simple, Stupid. Prioritize logic readability and maintainability.
- **YAGNI**: You Aren't Gonna Need It. No speculative features or over-engineering.
- **DRY**: Don't Repeat Yourself. Extract reusable logic to specialized skills or common utilities.

## Implementation Standards
- **File Size**: Strictly enforced 200-line limit per code file. Split logic when exceeded.
- **Naming**: `kebab-case` for all files. `PascalCase` for classes/components. `camelCase` for functions/variables.
- **Architecture**: Modular approach with clear boundaries between agents, commands, skills, and hooks.
- **State Management**: Context-driven communication between agents using JSON-formatted reports.

## Documentation Standards
- **Source of Truth**: The `docs/` directory is the primary source of truth for architecture and requirements.
- **Synchronized Docs**: `codebase-summary.md` and `project-roadmap.md` must be updated after major architectural changes.
- **Clarity Over Grammar**: Conciseness and technical accuracy are prioritized over formal prose in reports.

## Testing & Verification Protocol
- **Zero Mocks**: Avoid mocks/stubs that mask real implementation failures.
- **Mandatory Verification**: Every implementation phase MUST be followed by a successful verification/testing phase.
- **Self-Correction**: Agents are expected to debug and fix their own test failures before claiming task completion.

## Git & Version Control
- **Conventional Commits**: `feat:`, `fix:`, `refactor:`, `docs:`, `chore:`.
- **Atomic Commits**: One distinct change per commit.
- **Secret Management**: Never commit credentials/keys. Hook-level privacy blocks enforce this.

## Unresolved Questions
- Standardized linting rules for Python skills in `.claude/skills/`.
- Uniform error handling and response schema across all subagent types.
