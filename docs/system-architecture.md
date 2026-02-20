# System Architecture

## Overview
Brag utilizes a multi-layered agentic architecture designed for high autonomy, reliability, and security. Built on Anthropic's Claude Code, the system extends capabilities through specialized agents, complex lifecycle hooks, and a modular skill system.

## Architectural Layers

### 1. Orchestration Layer (.claude/workflows/)
- **State Machine**: Defines the global development cycle via `primary-workflow.md`.
- **Protocol**: `orchestration-protocol.md` manages subagent delegation, task sequencing, and parallelization.
- **Rules Engine**: `development-rules.md` enforces core principles (KISS, YAGNI, 200-line limits).

### 2. Agent Layer (.claude/agents/)
- **Autonomous Agents**: 17+ specialized personas (e.g., `planner`, `scout`, `tester`, `code-reviewer`).
- **Communication**: Contextual report-passing via the `plans/reports/` directory.
- **Context Injection**: Hooks automatically inject relevant subagent context during initialization.

### 3. Capability Layer (.claude/skills/)
- **Modular Skills**: 25+ dynamic capabilities implemented in Python or JavaScript.
- **Multimodal Stack**: Advanced image/video/PDF analysis leveraging Gemini 3 Flash/Pro.
- **Tools**: Repomix for codebase compaction, Chrome DevTools for browser automation, and Shopify/Better-Auth integrations.

### 4. Integration & Security Layer (.claude/hooks/ & .claude/commands/)
- **Lifecycle Hooks**: Automated triggers for session start/end, privacy blocking (secrets), and scout blocking (unauthorized pathing).
- **Slash Commands**: CLI interface extending Claude Code (`/plan`, `/cook`, `/fix`, `/scout`, `/journal`).
- **Knowledge Base**: Deep integration with Obsidian for cross-project intelligence. Includes a centralized `Project-Portfolio-Dashboard.md` using Dataview for real-time tracking of status, deadlines, and marketing ROI.

## Data & Context Flow
1. **Request**: User issues a slash command or requirements.
2. **Analysis**: `planner` agent generates a hierarchical plan in `plans/`.
3. **Execution**: Relevant subagents are activated; `scout` explores the codebase.
4. **Compaction**: `repomix` generates `repomix-output.xml` to optimize LLM context.
5. **Validation**: `tester` and `code-reviewer` verify the implementation.
6. **Closing**: `docs-manager` updates technical documentation and roadmap.

## Security Controls
- **Privacy Blocks**: Regex-based detection of API keys and credentials in code/commits.
- **Scout Blocks**: Restrictions on agent exploration to prevent accidental modification of critical infrastructure.

## Unresolved Questions
- Dynamic agent scaling based on real-time task complexity.
- Cross-platform unified installer for unified environment setup.
