# Project Overview & PDR

## Project Vision
To create the most efficient and robust AI-native development environment by orchestrating specialized agents through structured protocols, ensuring high-quality software delivery with minimal human overhead.

## Product Development Requirements (PDR)

### 1. Functional Requirements
- **Multi-Agent Orchestration**: Seamless delegation and communication between 25+ specialized agents (planner, scout, tester, etc.).
- **Automated Workflows**: Strict enforcement of the Planning → Implementation → Testing → Review cycle via `primary-workflow.md`.
- **Skill Integration**: Dynamic loading and execution of 25+ Python/JS skills (e.g., `repomix`, `ai-multimodal`, `chrome-devtools`).
- **Slash Command System**: Unified CLI interface for lifecycle management (`/plan`, `/cook`, `/fix`, `/scout`).
- **Lifecycle Hooks**: Automated session initialization, privacy blocks, and context management in `.claude/hooks/`.
- **Knowledge Management**: Integration with Obsidian vault for cross-project tracking (Brag, BetterBytes, Platesify).

### 2. Non-Functional Requirements
- **Performance**: Rapid subagent response times and efficient token usage via context optimization.
- **Reliability**: Zero-mock testing policy; all implementations must be verified with real code.
- **Security**: Mandatory privacy blocks for secrets and credentials; strict file exploration controls (scout blocks).
- **Scalability**: Support for complex multi-phase projects via hierarchical planning and subagent delegation.
- **Simplicity**: Strict adherence to KISS, YAGNI, and DRY principles.

### 3. Technical Constraints
- Powered by Claude Code (Anthropic).
- Skill environment requires Python venv with dependencies in `.claude/skills/`.
- Codebase constraints: 200-line limit per file strictly enforced.
- Directory structure must follow `.claude/`, `docs/`, `plans/`, and `Obsidian/` patterns.

## Success Metrics
- **Development Velocity**: Significant reduction in time from requirement definition to verified production code.
- **Code Quality**: High test coverage and minimal regressions through mandatory review/test phases.
- **Documentation Accuracy**: Automated synchronization of `codebase-summary.md` and `project-roadmap.md`.

## Unresolved Questions
- Integration with external CI/CD providers beyond GitHub Actions.
- Performance impact of running 10+ agents in parallel on various hardware.
- Long-term memory persistence for agents across disparate development sessions.
