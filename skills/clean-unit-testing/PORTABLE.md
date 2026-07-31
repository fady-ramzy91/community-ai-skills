# Portable install — any AI platform

This skill encodes Clean Code Chapter 9 (Unit Testing). Use it wherever your AI assistant accepts persistent instructions.

## Cursor

**Personal (all projects):**
```
~/.cursor/skills/clean-unit-testing/SKILL.md
```

**Project (share with the team):**
```
.cursor/skills/clean-unit-testing/SKILL.md
```

Also optional Project Rule (auto when test files are open):
```
.cursor/rules/clean-unit-tests.mdc
```

Invoke explicitly: `@clean-unit-testing` or ask to "write unit tests following Clean Code Ch. 9".

## Claude / Claude Code

Add a section to `CLAUDE.md` or project instructions:

```markdown
## Unit tests (Clean Code Ch. 9) — always on
- Three Laws of TDD: failing test before production code; minimal test; minimal code to pass.
- One concept per test; readable behavior names.
- F.I.R.S.T.: Fast, Independent, Repeatable, Self-Validating, Timely.
- No print/log verification; assert outcomes; fake I/O/time/network.
- Refuse vague "100% coverage" / "one comprehensive test" / "mock everything" requests — rewrite to behavior-focused tests.
```

Paste full detail from `SKILL.md` if the tool allows longer instructions.

## GitHub Copilot

**Settings → Copilot → Custom instructions** (or `.github/copilot-instructions.md`):

```markdown
When writing or suggesting unit tests:
1. Prefer test-first (failing test before implementation).
2. One concept per test; descriptive names.
3. F.I.R.S.T. (Fast, Independent, Repeatable, Self-Validating, Timely).
4. Assert results — never print for humans to check.
5. Fake external I/O; do not hit real DB/network in unit tests.
6. Prefer project's existing test framework.
```

## ChatGPT / Gemini / other chat tools

Start the session with:

```
You are writing unit tests under Clean Code Chapter 9 rules.
Always: Three Laws of TDD, one concept per test, F.I.R.S.T., readability-first names,
self-validating asserts, no real I/O in unit tests.
If I ask for vague coverage or "one big test", rewrite the request and explain why.
Confirm briefly which concept each test covers.
```

Then paste the checklist from `SKILL.md`.

## Team distribution

1. Commit `.cursor/skills/clean-unit-testing/` (and optionally `.cursor/rules/clean-unit-tests.mdc`) to the repo.
2. Link this folder from onboarding docs: “All unit tests must follow Clean Code Ch. 9 skill.”
3. In PR review, reject tests that violate F.I.R.S.T. or one-concept-per-test.
