# Codebase Summary

## Project Overview
Brag is a sophisticated AI agent orchestration system powered by Claude Code. It features a modular architecture with specialized agents, advanced workflows, and a comprehensive skill system to handle complex software development tasks.

## Directory Structure
```
.
├── .claude/               # Core agent configuration and workflows
│   ├── agents/            # Specialized agent definitions (17 agents found)
│   ├── commands/          # Slash command implementations (/plan, /fix, /cook, etc.)
│   ├── hooks/             # Lifecycle hooks (privacy-block, scout-block, session-init)
│   ├── scripts/           # Management scripts (generate_catalogs, resolve_env)
│   ├── skills/            # Extensible capabilities (25+ modular skills)
│   └── workflows/         # Global protocols (primary, orchestration, dev-rules)
├── docs/                  # Project documentation source of truth
├── plans/                 # Planning and execution reports
│   ├── reports/           # Subagent execution logs (naming: docs-manager-YYMMDD-slug.md)
│   └── templates/         # Standardized planning templates
├── Obsidian/              # Integrated knowledge vault
│   ├── Eddy/Project/      # Project management command center (Dashboard, Templates, Marketing)
│   └── ...                # Individual project vaults (Brag, BetterBytes, Platesify)
├── repomix-output.xml     # Packed codebase context for AI consumption
├── CLAUDE.md              # Root configuration and agent instructions
└── README.md              # Project entry point and overview
```

## Core Components

### 1. Agent System (.claude/agents/)
- **17 Specialized Agents**: Includes `planner`, `tester`, `code-reviewer`, `debugger`, `docs-manager`, `scout`, `git-manager`, `mcp-manager`, and more.
- **Protocol**: Agents follow strict behavioral guidelines defined in their respective markdown files.

### 2. Workflow Engine (.claude/workflows/)
- **Primary Workflow**: Mandatory Plan → Implement → Test → Review cycle.
- **Development Rules**: Enforces KISS, YAGNI, DRY, and 200-line file limits.
- **Orchestration**: Manages subagent delegation and task sequencing.

### 3. Command System (.claude/commands/)
- **Productivity Commands**: `/plan`, `/fix`, `/cook`, `/scout`, `/test`, `/docs`, `/journal`, `/kanban`.
- **Infrastructure**: Bootstrap and optimization commands for environment maintenance.

### 4. Skill System (.claude/skills/)
- **25+ Modular Capabilities**:
  - **DevOps**: `devops`, `repomix`, `cloudflare-d1-kv`, `docker-basics`.
  - **AI/Multimodal**: `ai-multimodal` (Gemini API), `ai-artist`, `media-processing`.
  - **Testing/Debugging**: `debugging`, `sequential-thinking`, `chrome-devtools`.
  - **Domain Specific**: `better-auth`, `payment-integration` (Polar/SePay), `shopify`.

### 5. Hook System (.claude/hooks/)
- **Security**: `privacy-block` (secret detection), `scout-block` (path extraction and filtering).
- **Session**: `session-init`, `session-end`, `subagent-init` for context synchronization.

## Documentation Context
- **docs/**: Architectural source of truth (`project-overview-pdr.md`, `system-architecture.md`).
- **Obsidian/**: Real-time project tracking and long-term knowledge retention.

## Unresolved Questions
- None.
