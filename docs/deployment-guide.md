# Deployment Guide

## Prerequisites
- **Claude Code CLI**: Installed and authenticated (`auth` command).
- **Python 3.10+**: Required for the modular skill environment.
- **Node.js 18+**: Required for JavaScript-based hooks and commands.
- **Git**: Required for repository management and subagent collaboration.

## Environment Setup
1. **Clone Repository**:
   ```bash
   git clone <repo-url>
   cd brag
   ```
2. **Setup Skill Environment**:
   ```bash
   cd .claude/skills
   ./install.sh  # On Linux/macOS
   # OR ./install.ps1 on Windows
   ```
   This script creates a `.venv` and installs all necessary dependencies (google-genai, pypdf, etc.).
3. **Configure API Keys**:
   - Create a `.env` file in the root or `.claude/` directory.
   - Required: `ANTHROPIC_API_KEY`, `GOOGLE_GENAI_API_KEY`.
   - Optional: Keys for Polar, SePay, Shopify as needed.

## Development Workflow
1. **Initialize Session**: Run `claude-code` in the root. The `session-init` hook will fire automatically.
2. **Lifecycle Management**:
   - Use `/plan` to define tasks.
   - Use `/scout` to explore unknown codebase areas.
   - Use `/fix` or `/test` for implementation and verification.
3. **Documentation**: Run `/docs update` to synchronize documentation via the `docs-manager` agent.

## Deployment as a Service
1. **Containerization**: Use the `Dockerfile` for standardized environment replication.
2. **Infrastructure**: Deploy the agent server to GCP (Cloud Run) or AWS (App Runner).
3. **Notifications**: Configure `discord_notify.sh` or `telegram_notify.sh` in `.claude/hooks/notifications/` for real-time status updates.

## Security Controls
- **Privacy Blocks**: Ensure `.claude/hooks/privacy-block.cjs` is active to prevent secret leakage.
- **Scout Limits**: Configure allowed paths in `scout-block.cjs` for sensitive environments.

## Unresolved Questions
- Unified cross-platform installer script (`setup.sh`).
- Automated dependency resolution for new skills.
