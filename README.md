# agent-toolkit

Project-agnostic reference material for AI coding agents (Claude Code, Codex CLI, Cursor, etc.): templates and conventions meant to be copied into any project, not tied to a specific codebase.

## Contents

- `docs/agents/templates/user-story.md`: Jira-ready user story format to write before formalizing a feature with a spec-driven workflow
- `docs/agents/conventions/commit-messages.md`: commit message conventions (Conventional Commits, plus a few refinements)

## Usage

Copy the `docs/agents/` folder into your project as-is, then point to it from your project's `AGENTS.md`:

```markdown
## See also

`docs/agents/`: templates, conventions, and other reference material for agents working in this repo:
- `docs/agents/templates/user-story.md`: Jira-ready user story format
- `docs/agents/conventions/commit-messages.md`: commit message conventions
```

Everything under `docs/agents/` stays project-agnostic here. If a project needs its own examples, adapt a copy in that project rather than editing it here.
