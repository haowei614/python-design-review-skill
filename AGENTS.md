# Agent Instructions

This repository contains a reusable Python design review rule set for AI coding
agents.

Primary entrypoints:

- Codex: use `SKILL.md`.
- Claude Code: use `CLAUDE.md`.
- Cursor: use `.cursor/rules/python-design-review.mdc`.
- Other agents: follow this file and load `SKILL.md` for the full workflow.

## Default Behavior

When reviewing Python code, prioritize:

1. KISS
2. YAGNI
3. DRY
4. SOLID
5. Engineering quality

Use the supporting references as needed:

- `references/design-checklist.md`
- `references/quality-checklist.md`
- `references/examples.md`

Prefer practical, minimal recommendations. Do not recommend abstractions unless
duplication, ownership boundaries, or real change pressure justify them.
