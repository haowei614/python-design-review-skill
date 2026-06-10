# Design Checklist

Focus: structural and architectural issues (KISS / YAGNI / DRY / SOLID).
Engineering hygiene is in `quality-checklist.md`.

---

## KISS
- [ ] Is there a simpler solution that solves the same problem?
- [ ] Is control flow easy to follow? (early returns used where appropriate?)
- [ ] Is nesting too deep (>3 levels)?
- [ ] Are there unnecessary patterns, wrappers, or indirections?
- [ ] Are function/method responsibilities small and clear?

## YAGNI
- [ ] Was any code added for a hypothetical future need?
- [ ] Are there unused parameters, extension points, or base classes?
- [ ] Are there hooks or config options that nothing uses yet?
- [ ] Is there dead code or premature generalization?

## DRY
- [ ] Is any business logic or validation rule duplicated?
- [ ] Are constants or rules repeated across layers?
- [ ] Does the duplication occur 3+ times? (rule of three)
- [ ] Would an abstraction make this clearer — or harder to follow?

## SOLID

### SRP (Single Responsibility)
- [ ] Does each class/module have one clear reason to change?
- [ ] Are I/O, persistence, and business logic mixed in one unit?

### OCP (Open/Closed)
- [ ] Can new behavior be added without editing stable, tested code?
- [ ] Is there an `if/elif` chain that grows every time a new case is added?

### LSP (Liskov Substitution)
- [ ] Do subclasses preserve the parent's contracts and invariants?
- [ ] Is inheritance used where composition would be safer and simpler?

### ISP (Interface Segregation)
- [ ] Are interfaces or abstract base classes too broad?
- [ ] Are implementers forced to define methods they don't need?

### DIP (Dependency Inversion)
- [ ] Does high-level logic depend directly on concrete implementations?
- [ ] Could dependencies be injected to make the unit independently testable?
