# Python Design Review Skill

A reusable Python design review rule set for AI coding agents, focused on design
quality and engineering hygiene.

It reviews Python code through a conservative engineering lens:

- KISS: prefer the simplest solution that solves the current problem
- YAGNI: avoid speculative abstractions and unused extension points
- DRY: remove meaningful duplication without hiding clarity
- SOLID: check responsibility boundaries, substitutability, interfaces, and dependency direction
- Engineering quality: linting, formatting, typing, tests, and reproducible environments

## When To Use

Use this project when asking an AI coding agent to review Python code for:

- Code review before merge or commit
- Refactoring advice
- Over-engineering checks
- Maintainability analysis
- Python design critique
- Engineering quality review

Example prompts:

```text
Use python-design-review to review this Python package for over-engineering.
```

```text
Review this PR for KISS, YAGNI, DRY, SOLID, and missing tests.
```

```text
Can this module be simplified without losing behavior?
```

## Agent Support

This repository is organized so different coding agents can use the same review
workflow:

- Codex: `SKILL.md`
- Claude Code: `CLAUDE.md`
- Cursor: `.cursor/rules/python-design-review.mdc`
- Other agents: `AGENTS.md`

The detailed checklists and examples live in `references/` so each agent can load
only the context it needs.

## What It Produces

The review output is intentionally concise and evidence-based:

- Design violations with principle, file, line, and severity
- Engineering issues such as missing tests, typing gaps, or unclear tool workflow
- Suggested verification commands adapted to the project
- Summary of the overall review result and residual risk

Severity is defined in `SKILL.md`:

- High: likely bug, security risk, data loss, broken public contract, or design flaw blocking safe change
- Medium: maintainability, extensibility, or testability issue with meaningful future cost
- Low: localized clarity, style, naming, typing, or hygiene issue

## Repository Contents

```text
.
├── AGENTS.md
├── CLAUDE.md
├── SKILL.md
├── LICENSE
├── README.md
├── .cursor/
│   └── rules/
│       └── python-design-review.mdc
└── references/
    ├── design-checklist.md
    ├── quality-checklist.md
    └── examples.md
```

- `SKILL.md`: main Codex skill instructions and trigger metadata
- `CLAUDE.md`: Claude Code project instructions
- `AGENTS.md`: generic agent instructions
- `.cursor/rules/python-design-review.mdc`: Cursor-compatible rule file
- `references/design-checklist.md`: KISS, YAGNI, DRY, and SOLID review checklist
- `references/quality-checklist.md`: lint, format, typing, tests, and environment checklist
- `references/examples.md`: common review patterns with before/after examples

## Installation

For Codex, clone or copy this repository into your Codex skills directory as a
skill folder. The folder name should match the skill name:

```bash
python-design-review/
```

For example:

```text
~/.codex/skills/python-design-review/
```

The skill is discovered from the `name` and `description` fields in `SKILL.md`.

For Claude Code, keep `CLAUDE.md` at the repository root or copy its contents
into the target project's Claude instructions.

For Cursor, copy `.cursor/rules/python-design-review.mdc` into the target
project's `.cursor/rules/` directory.

## Design Philosophy

This skill is intentionally pragmatic. It should not reward abstract purity over
useful software.

It prefers:

- Small, local refactors over broad rewrites
- Evidence-based findings over principle-driven nitpicks
- Project conventions over personal taste
- Lower severity when impact is uncertain
- Clear verification commands over vague advice

## License

This project is released under the MIT License. See `LICENSE` for details.
