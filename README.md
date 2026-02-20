# Brag

Advanced AI Agent Orchestration System powered by Claude Code.

## Overview
Brag is a sophisticated development environment that leverages specialized AI agents, structured workflows, and extensible skills to automate complex software engineering tasks. It follows a "Plan-First" methodology and strictly adheres to KISS, YAGNI, and DRY principles.

## Key Features
- **25+ Specialized Agents**: Dedicated agents for planning (`planner`), testing (`tester`), reviewing (`code-reviewer`), and more.
- **Structured Workflows**: Enforced protocols in `.claude/workflows/` (Primary, Orchestration, Development Rules).
- **Extensible Skill System**: 25+ dynamic modules including `repomix`, `ai-multimodal`, `chrome-devtools`, and `payment-integration`.
- **Slash Commands**: Powerful CLI interface with commands like `/plan`, `/cook`, `/fix`, `/scout`, and `/docs`.
- **Integrated Infrastructure**: Deeply integrated with an Obsidian vault for knowledge management and lifecycle hooks for session management.

## Project Structure
- `.claude/`: Core configuration, agents, skills, and workflows.
- `docs/`: Technical documentation (source of truth).
- `plans/`: Execution plans and subagent reports.
- `Obsidian/`: Knowledge vault and personal projects (Brag, BetterBytes, Platesify).
- `CLAUDE.md`: AI behavior and project instructions manual.

## Quick Start
1. **Explore Commands**: Run `/help` in Claude Code to see available slash commands.
2. **Start Planning**: Use `/plan` to initiate a new feature or bug fix.
3. **Implementation**: Follow the `primary-workflow.md` protocol (Plan → Implement → Test → Review).
4. **Documentation**: Refer to `docs/` for architecture and standards.

## Development Rules
- **Keep it Simple**: Follow KISS/YAGNI/DRY.
- **File Limits**: Maintain code files under 200 lines strictly.
- **Security**: Privacy blocks in `.claude/hooks/` prevent secret/credential commits.
- **Verification**: Zero-mock testing policy; all changes must be verified.

## Documentation
Full documentation is available in the `docs/` directory:
- [Project Overview & PDR](docs/project-overview-pdr.md)
- [Code Standards](docs/code-standards.md)
- [System Architecture](docs/system-architecture.md)
- [Codebase Summary](docs/codebase-summary.md)
- [Project Roadmap](docs/project-roadmap.md)

## Unresolved Questions
- None.
