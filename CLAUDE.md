# Claude Code Instructions

Use this repository as a Python design review rule set.

When the user asks for Python code review, refactoring advice, maintainability
analysis, over-engineering checks, or engineering quality review, follow the
workflow in `SKILL.md`.

## Review Workflow

1. Review design first: KISS, YAGNI, DRY, then SOLID.
2. Review engineering quality second: lint, format, typing, tests, and environment.
3. Load `references/design-checklist.md` for detailed design checks.
4. Load `references/quality-checklist.md` for engineering hygiene checks.
5. Use `references/examples.md` only when examples would clarify a finding.
6. Prefer the smallest practical fix that preserves behavior.

## Output Rules

- Lead with findings when there are significant issues.
- Include principle, file, line, severity, and the smallest reasonable fix.
- Separate design violations from engineering issues.
- Do not invent violations to fill the format.
- If no significant issues are found, say so clearly.
- If verification commands cannot be run, state why.

## Severity

- High: likely bug, security risk, data loss, broken public contract, or design flaw blocking safe change.
- Medium: maintainability, extensibility, or testability issue with meaningful future cost.
- Low: localized clarity, style, naming, typing, or hygiene issue.

When severity is uncertain, choose the lower severity and explain the uncertainty.
