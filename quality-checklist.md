# Engineering Quality Checklist

Focus: tooling, hygiene, and reproducibility.
Design principle violations are in `design-checklist.md`.

---

## Lint & format
- [ ] `ruff check` passes (or project-equivalent linter)
- [ ] `ruff format --check` passes (or project-equivalent formatter)
- [ ] No ignored rules without a comment explaining why

## Type checking
- [ ] `mypy` (or `pyright`) passes, if configured
- [ ] Public functions have type hints
- [ ] No unexplained `# type: ignore` suppressions

## Tests
- [ ] Core logic has unit tests
- [ ] Edge cases and error paths are covered
- [ ] Tests are fast and deterministic (no uncontrolled I/O or time)
- [ ] `pytest` (or equivalent) passes cleanly

## Environment reproducibility
- [ ] Dependencies are pinned (lockfile present: `uv.lock`, `poetry.lock`, etc.)
- [ ] One clear command to install the environment
- [ ] No implicit system-level dependencies undocumented

## Tooling workflow
- [ ] There is one obvious command path for: install / lint / test / run
- [ ] If `uv`: commands are consistent (`uv run <tool>`)
- [ ] If not `uv`: project standard is clearly documented

## Suggested commands (uv-based project)
```
uv run ruff check .
uv run ruff format --check .
uv run mypy .
uv run pytest
```
Adjust to the project's actual toolchain if different.
