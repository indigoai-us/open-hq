# Changelog

## [1.0.0] — 2026-04-15

### Initial Release

First public release of HQ by Indigo — Personal OS for AI Workers.

### Included

- **44 slash commands** for session management, workers, projects, content, and design
- **28+ AI workers** organized into dev team, content team, QA, security, and more
- **44+ skills** (design, animate, polish, review, audit, brainstorm, and more)
- **20+ knowledge bases** covering Ralph methodology, design styles, security frameworks
- **Orchestrator** — externalized Ralph loop for multi-story project execution
- **Hook system** — configurable hook profiles (minimal, standard, strict) via `HQ_HOOK_PROFILE`
- **Module management** — `modules/modules.yaml` for knowledge base registration and sync
- **Cross-session repo coordination** — active-run registry prevents edit conflicts
- **Two-stage context advisories** — 60% warning + 75% pre-compact checkpoint prompts
- **HQ Teams** — shared team workspaces via embedded git repos
- **Codex bridge** — 12 promoted skills available in OpenAI Codex via `scripts/codex-skill-bridge.sh`
