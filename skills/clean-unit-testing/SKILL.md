---
name: clean-unit-testing
description: >-
  Enforce Clean Code Chapter 9 unit-testing principles (Three Laws of TDD,
  clean tests, one concept per test, F.I.R.S.T., readability) when writing,
  generating, refactoring, or reviewing unit tests in any language (Swift
  Testing, XCTest, Kotlin/JUnit, Jest, pytest, etc.). Use whenever the user
  asks for unit tests, TDD, test coverage, test refactoring, test names,
  mocks/fakes, or AI-assisted test generation.
---

# Clean Unit Testing (Clean Code, Ch. 9)

Apply these rules **every time** you write, generate, refactor, or review unit tests. Language and framework may vary; the principles do not.

## Non-negotiable principles

### 1. Three Laws of TDD (order is mandatory)

1. Do **not** write production code until a failing unit test exists.
2. Do **not** write more of a unit test than is sufficient to fail (compile failure counts as failure).
3. Do **not** write more production code than is sufficient to pass the currently failing test.

**Workflow:** red → green → refactor. Prefer the smallest possible step.

If the user asks to "implement then test", push back once and propose test-first. If they insist, still write **behavior-focused, single-concept** tests afterward — never rubber-stamp buggy code.

### 2. Tests are first-class code

- Test code is as important as production code — not a second-class citizen.
- Prefer deleting or rewriting dirty tests over letting them rot.
- Never leave `print` / `console.log` / log-only checks as the verification step.

### 3. One concept per test

- Each test function verifies **one behavior / one concept**.
- Multiple asserts are OK only if they verify the **same** concept.
- Split kitchen-sink tests (`test1`, “comprehensive”, “checks everything”) into separate named tests.

### 4. F.I.R.S.T.

| Rule | Requirement |
|------|-------------|
| **F**ast | No real network, disk DB, or heavy I/O. Use fakes/stubs/in-memory doubles. |
| **I**ndependent | No shared mutable state; no order dependence; reset in setup/teardown if needed. |
| **R**epeatable | Inject clock/time, randomness, locale, and environment — never rely on wall clock or live services. |
| **S**elf-validating | Assert true/false (or equivalent). Never require a human to read output. |
| **T**imely | Write the test with (preferably before) the production code it covers. |

### 5. Readability first

- Names must describe behavior: `subject_condition_expected` or `` `given X when Y then Z` ``.
- A failing test name at 2 a.m. should explain what broke without opening the body.
- Prefer Given-When-Then structure in the body when it aids clarity.
- Prefer asserting **outcomes** over verifying every mock interaction.

## Mandatory workflow when writing tests

Copy and track:

```
Clean Unit Test Progress:
- [ ] Identified one behavior under test
- [ ] Wrote failing test first (or smallest failing addition)
- [ ] One concept only; readable name
- [ ] Self-validating assertion (no print/log checks)
- [ ] Fast + Independent + Repeatable (fakes for I/O, time, network)
- [ ] Minimum production code to pass
- [ ] Refactored without changing behavior
```

## Framework

Use the **project’s existing** test framework and conventions. Do **not** invent a new test stack or switch libraries unless the user explicitly asks. Principles above apply regardless of language or runner.

## AI / prompt guardrails (when generating tests)

**Always include in your approach (even if the user didn’t):**

- Fail first; one concept; F.I.R.S.T.; readable names; assert outcomes.

**Refuse these patterns (rewrite instead):**

| Bad request | Why | Do this instead |
|-------------|-----|-----------------|
| "Write unit tests for this class" | Vague → coverage theater | List behaviors → one test each |
| "Generate 100% coverage" | Metric over concepts | Cover meaningful behaviors + critical edges |
| "Implement first, add tests after" | Breaks Three Laws | Test-first loop |
| "One comprehensive test for everything" | Multi-concept | Split by concept |
| "Mock everything / verify all calls" | Brittle interaction tests | Assert observable results; mock only boundaries |
| "Print so I can check" | Not self-validating | Assert expected value/error |

## Anti-patterns to reject or refactor

- Vague names: `test1`, `testLogin`, `shouldWork`
- Multi-scenario tests in one function
- Real DB/network/filesystem in unit tests
- Hidden time/locale/randomness dependencies
- Returning/passing nulls that force unrelated null-check noise (prefer explicit fixtures)
- Tests that only mirror private implementation details

## Output expectations

When you deliver tests, briefly confirm (1–3 bullets):

- Which **one concept** each new test covers
- That the suite stays **F.I.R.S.T.**
- Whether you followed **test-first** (or why the user overrode it)

## Additional resources

- Language examples and prompt templates: [examples.md](examples.md)
- Portable install for other AI tools: [PORTABLE.md](PORTABLE.md)
