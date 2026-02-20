# Design Guidelines

## UX Philosophy
- **CLI-First**: Focus on efficient, text-based interactions for developers within the terminal.
- **Progressive Disclosure**: Only show complex details or large outputs when explicitly requested.
- **Instant Feedback**: Provide immediate confirmation for all commands and agent actions.

## AI Interaction Design
- **Conciseness**: Agents must speak technical, precise, and concise language.
- **Attribution**: Clearly indicate which agent (e.g., `planner`, `scout`, `tester`) is performing an action.
- **Safety**: Require user confirmation for destructive actions (e.g., force push, hard reset).
- **Tone**: Professional, senior-level expertise; objective and action-oriented.

## Code Design (Visual)
- **Kebab-Case File Naming**: Clean, consistent directory and file structure.
- **Markdown Formatting**: Use semantic headers and organized lists for all documentation.
- **Syntax Highlighting**: Label all code blocks in reports and documentation.
- **Case Consistency**: Follow project standards (`PascalCase` for classes, `camelCase` for variables).

## Subagent Persona Design
- **Action over Suggestion**: Focus on "doing" (implementing, testing) rather than just "suggesting" changes.
- **Cross-Pollination**: Agents should reference each other's findings and context.
- **Plan-First**: No implementation without a preceding plan in the `plans/` directory.

## Obsidian Workflow
- **Hierarchical Notes**: Organized by Date → Project → Note Type (e.g., Research, Plan).
- **Bi-directional Linking**: Use `[[links]]` to connect related knowledge nodes across the vault.
- **Project Tracking**: Dedicated folders for Brag, BetterBytes, Platesify, and other active projects.

## Unresolved Questions
- Design patterns for visual output (charts/graphs) within a CLI context.
- Standardized UI components for the web-based Kanban board (`/kanban`).
