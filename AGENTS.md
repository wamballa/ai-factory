# AI Factory Agents

This repository contains multiple AI agents used by the AI Factory system.

General rules for agents:

1. Prefer modifying existing files over creating new ones.
2. Use `TODO.md` as the single task board for all work tracking.
3. Store discoveries and learnings in `memory/`.
4. Documentation updates belong in docs/.
5. Project-specific work belongs in projects/.
6. Do not create additional task files (for example, extra `TODO.md` files or `tasks.md` files).
7. Scaffold new micro-SaaS projects from `templates/project-template/`.

Agents may also contain their own AGENTS.md files that override these rules.

## Task Board Policy

Agents must:
- use root `TODO.md` for task state changes
- move tasks between `Backlog` -> `In Progress` -> `Completed`
- avoid using `TODO.md` as a narrative changelog
- avoid creating any additional task tracking files

## Work Tracking

After completing any task:

1. Update TODO.md
   - Mark completed tasks
   - Add newly discovered tasks

2. Record important learnings in `memory/`

Use these files:

- `memory/inbox.md` for temporary notes and discoveries
- `memory/knowledge.md` for stable facts
- `memory/decisions.md` for architectural decisions

Entries must include:
- timestamp
- agent
- short description
