# Clean Unit Testing — Examples

## Good prompts (copy-paste)

### Test-first
```
Don't implement <Feature> yet. Write one failing unit test for <behavior>.
One concept only. Use the project's test framework. Stop when the test fails
to compile or fails at runtime — do not write production code yet.
```

### Behaviors → one test each
```
Here's <Type/function>. List the behaviors it claims to support, then write
exactly one test per behavior. No multi-assert kitchen-sink tests. Name each
test so a 2 a.m. CI failure explains what broke without opening the body.
```

### Refactor dirty tests
```
Refactor this test file to Clean Code Ch. 9 / F.I.R.S.T.: split multi-assert
tests into single-concept tests, replace print/log checks with assertions,
inject fakes for time/network/DB, rename tests to describe behavior.
```

### Hostile QA / edges
```
Act as hostile QA. Suggest 5 edge cases that would break <function> that a
happy-path test would miss. Then write one failing test for the most
important case only.
```

## Bad prompts (do not follow literally — rewrite)

| Bad | Rewrite toward |
|-----|----------------|
| Write unit tests for this class | List behaviors → one test each, fail-first |
| Generate 100% coverage | Meaningful behaviors + critical edges |
| Implement then add tests | Three Laws: failing test first |
| One comprehensive test | One concept per test |
| Mock everything | Assert outcomes; mock boundaries only |
| Print results for me to check | Self-validating asserts |

## Messy → clean

```
// BAD — multi-concept, opaque name
test test1() {
  assertTrue(validate(User("a@b.com", "pw123456")))
  assertFalse(validate(User("bad-email", "pw123456")))
}

// GOOD — one concept each
test valid_email_and_password_passes_validation() {
  assertTrue(validate(User("a@b.com", "pw123456")))
}

test invalid_email_fails_validation() {
  assertFalse(validate(User("bad-email", "pw123456")))
}
```

Always prefer the project's existing test framework over inventing a new one.
