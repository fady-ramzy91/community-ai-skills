# Portable install — run Chapter 10 on any class

This skill **executes** Clean Code Chapter 10 on a named type: audit, then split if it has more than one responsibility.

## Cursor

**Personal (every project):**
```
~/.cursor/skills/clean-classes/SKILL.md
```

**Project (share with the team):**
```
.cursor/skills/clean-classes/SKILL.md
```

Optional rule (ViewModel / UseCase / Manager files):
```
.cursor/rules/clean-classes.mdc
```

**Run it:** `@clean-classes` on a file, or:

```
Run clean-classes on <Type>. Split if it has more than one responsibility.
```

## Claude / Claude Code

Add to `CLAUDE.md`:

```markdown
## Classes (Clean Code Ch. 10) — run on a named type
When asked to clean/split a class:
1. Inventory methods, fields, concretes, switches.
2. Naming test: ~25 words, no and/or/but.
3. List reasons to change. If 2+, split — one type per reason.
4. Map cohesion; extract clusters that do not share fields.
5. Replace kind-switches with a protocol + one type per variant.
6. Policy depends on abstractions; inject via init; wire concretes at composition root.
7. Re-audit every new type until each has one responsibility.
8. Do not dump leftovers into a Helper/Manager/ViewModel.
```

Paste `SKILL.md` if the tool allows longer instructions.

## GitHub Copilot

`.github/copilot-instructions.md`:

```markdown
When splitting or reviewing a class:
1. One reason to change per type; split if more.
2. Naming test without and/or/but; no Manager/Helper dumps.
3. Methods must share fields; extract clusters.
4. New variants = new types, not switch cases.
5. Depend on abstractions; inject; fake in tests.
6. Re-check each extracted type.
```

## ChatGPT / Gemini / other chat

Start with:

```
You are running Clean Code Chapter 10 on one class I will paste.
Always: naming test, list reasons to change, cohesion map, Open/Closed, DIP.
If more than one responsibility, split into types with honest names.
Re-audit every new type. Do not put leftovers in a Helper or ViewModel.
Show a short audit report, then the code.
```

Then paste the class and the checklist from `SKILL.md`.

## Team distribution

1. Copy from this catalog: `skills/clean-classes/` (https://github.com/fady-ramzy91/community-ai-skills).
2. Commit `.cursor/skills/clean-classes/` (and optionally `.cursor/rules/clean-classes.mdc`) to the consuming repo.
3. Onboarding: “Point the agent at a type and run `@clean-classes`.”
4. PR review: reject god classes, kind-switches, and use cases glued to concrete I/O.
