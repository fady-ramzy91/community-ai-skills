# Clean Classes

Encodes **Clean Code Chapter 10 (Classes)** so AI assistants can **run the rules on any class**:

- Small classes (25-word naming test)
- One reason to change (SRP)
- High cohesion
- Open for extension, closed for modification
- Depend on abstractions (DIP)

Point the agent at a type. If it has more than one responsibility, the skill **splits** it and re-audits every new type.

**Language-agnostic** — uses the project’s existing types, naming, and DI/composition patterns.

## Files

| File | Purpose |
|------|---------|
| [SKILL.md](SKILL.md) | Agent runbook (audit → split → re-audit) |
| [PORTABLE.md](PORTABLE.md) | Install on any AI platform |
| [examples.md](examples.md) | Invoke prompt and messy → split cases |

## Install

See [PORTABLE.md](PORTABLE.md) or the [repo README](../../README.md).
