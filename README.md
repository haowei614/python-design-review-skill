# Python Design Review Skill

A Codex skill for practical Python code review, focused on design quality and
engineering hygiene.

It reviews Python code through a conservative engineering lens:

- KISS: prefer the simplest solution that solves the current problem
- YAGNI: avoid speculative abstractions and unused extension points
- DRY: remove meaningful duplication without hiding clarity
- SOLID: check responsibility boundaries, substitutability, interfaces, and dependency direction
- Engineering quality: linting, formatting, typing, tests, and reproducible environments

## When To Use

Use this skill when asking Codex to review Python code for:

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

## What It Produces

The review output is intentionally concise and evidence-based:

- Summary of whether significant issues were found
- Design violations with principle, file, line, and severity
- Engineering issues such as missing tests, typing gaps, or unclear tool workflow
- Suggested verification commands adapted to the project

Severity is defined in `SKILL.md`:

- High: likely bug, security risk, data loss, broken public contract, or design flaw blocking safe change
- Medium: maintainability, extensibility, or testability issue with meaningful future cost
- Low: localized clarity, style, naming, typing, or hygiene issue

## Repository Contents

```text
.
├── SKILL.md
├── design-checklist.md
├── quality-checklist.md
├── examples.md
└── python-design-review.mdc
```

- `SKILL.md`: main Codex skill instructions and trigger metadata
- `design-checklist.md`: KISS, YAGNI, DRY, and SOLID review checklist
- `quality-checklist.md`: lint, format, typing, tests, and environment checklist
- `examples.md`: common review patterns with before/after examples
- `python-design-review.mdc`: optional Cursor-compatible mirror of the core rules

## Installation

Clone or copy this repository into your Codex skills directory as a skill folder.
The folder name should match the skill name:

```bash
python-design-review/
```

For example:

```text
~/.codex/skills/python-design-review/
```

The skill is discovered from the `name` and `description` fields in `SKILL.md`.

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
