---
name: python-design-review
description: >
  Review Python code using YAGNI, KISS, DRY, SOLID, plus engineering quality
  checks (lint, format, typing, tests, reproducible env).
  Use when the user asks for: code review, refactoring advice, design critique,
  maintainability analysis, Python engineering best practices,
  代码审查, 重构, 设计评审, 代码质量, 是否过度设计.
---

# Python Design Review Skill

## When to use
- User asks to review Python code
- User asks if code is over-engineered
- User asks for refactoring suggestions
- User wants pre-merge / pre-commit quality review
- User asks about Python design or maintainability (in any language)

## Core principles

Use these definitions as the source of truth for the Codex skill. Other agent
entrypoints in this repository should follow the same review workflow.

### KISS
- Prefer the simplest solution that solves the current problem.
- Avoid unnecessary abstraction, cleverness, wrappers, and indirection.
- Keep functions small; prefer early returns over deep nesting.
- Separate responsibilities when mixed concerns make code hard to follow.

### YAGNI
- Do not add functionality for hypothetical future needs.
- Remove dead code, unused arguments, unused extension points, and speculative
  abstractions.
- Reintroduce abstractions only when real change pressure exists.

### DRY
- Avoid duplicating business rules, validation rules, and constants.
- Follow the rule of three before extracting abstractions.
- Do not merge superficially similar code if the abstraction hurts clarity.

### SOLID
- **SRP**: each module, class, or function should have one clear reason to change.
- **OCP**: stable, tested behavior should be extended without repeated risky edits.
- **LSP**: subclasses must preserve parent contracts and invariants.
- **ISP**: avoid broad interfaces that force implementers to define unused methods.
- **DIP**: high-level logic should depend on injected collaborators or protocols
  when that improves testability and decoupling.

## Review order
1. KISS → 2. YAGNI → 3. DRY → 4. SOLID → 5. Engineering quality

Design issues and engineering issues are distinct:
- **Design issues** (steps 1–4): structural, architectural, principle violations.
- **Engineering issues** (step 5): lint, format, typing, tests, environment.

Review design first. Note engineering issues separately at the end.

## Severity rubric

- **High**: likely bug, security risk, data loss, broken public contract, or design
  flaw that blocks safe change or testing in important code paths.
- **Medium**: maintainability, extensibility, or testability issue that creates
  meaningful future cost, repeated churn, or confusing ownership boundaries.
- **Low**: localized clarity, style, naming, typing, or hygiene issue with little
  behavioral risk and an obvious small fix.

When severity is uncertain, choose the lower severity and explain the uncertainty.
Do not invent high-severity findings from principle preferences alone.

## How to run
1. Load `references/design-checklist.md` and apply each section.
2. Load `references/quality-checklist.md` and check engineering hygiene.
3. Reference `references/examples.md` for common violation patterns and before/after code.
4. Produce output in the format below.

## Output format

```
### Design violations
<principle> | <file>:<line> | <severity: high / medium / low>
Brief explanation + smallest reasonable fix.
[Optional: before/after code snippet]

### Engineering issues
List lint / format / type / test / env gaps found.

### Suggested verification commands
Commands appropriate for this project's toolchain.

### Summary
2–3 lines covering the overall review result and residual risk.
```

**If no significant violations found**: state that explicitly, skip empty
sections, and optionally note one minor improvement if relevant.

## Review rules
- Prefer minimal, practical refactors.
- Don't recommend abstractions unless duplication or change pressure justifies it.
- Treat `uv` as recommended, not mandatory.
- Align with existing project workflow if one exists.
- Distinguish style issues (low) from design issues (medium/high).
- Never invent violations to fill the output format.
