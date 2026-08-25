---
name: clean-classes
description: >-
  Run Clean Code Chapter 10 on any class: inventory methods and fields, apply
  the 25-word naming test, list reasons to change, check cohesion, Open/Closed,
  and Dependency Inversion, then split the type if it has more than one
  responsibility. Use when the user points at a class, ViewModel, use case,
  Manager, Helper, or Processor; asks to split a class, apply SRP, reduce
  responsibilities, fix a god class, or run clean-classes / Chapter 10 on a type.
---

# Clean Classes (Clean Code, Ch. 10)

Run this skill on **one target type** at a time. Language may be Swift, Kotlin, Java, TypeScript, or anything else — the procedure does not change.

If the user did not name a type, ask which class (or file) to run on. Do not scan the whole repo unless they asked for that.

Copy and track:

```
Clean Class Run:
- [ ] Target type identified
- [ ] Inventory (methods, fields, concretes, switches)
- [ ] Naming test (25 words, no and/or/but)
- [ ] Reasons to change listed
- [ ] Cohesion clusters mapped
- [ ] Open/Closed (switch-on-kind) checked
- [ ] DIP (concretes in policy) checked
- [ ] Split executed if more than one responsibility
- [ ] Each new type re-audited (must pass)
- [ ] Report delivered
```

## Rules that decide a split

A type **must be split** if any of these fail:

1. **Naming test** — cannot describe it in ~25 words without "and," "or," or "but."
2. **SRP** — more than one reason to change (product, network, cache, format, analytics, validation, persistence are different reasons).
3. **Cohesion** — methods form clusters that barely share fields.
4. **Open/Closed** — a `switch` / `when` / if-else on `kind` / `type` / enum grows for every new variant.
5. **DIP** — high-level policy names concretes (`URLSession`, `Retrofit`, `UserDefaults`, Room, shared prefs) or hidden singletons.

Vague names (`Manager`, `Helper`, `Processor`, `Super…`, `Util`) are a smell, not proof — still run the tests above.

A type **must not** dump leftover jobs into one "helper." Orchestrators (ViewModel, use case) **delegate**; they do not own networking, cache, formatting, or analytics.

Do not expose private methods just to test them. Extract a type and test that.

## Procedure

### 1. Inventory

From the target type, list:

- Public API (methods the callers use)
- Private helpers
- Instance/static fields
- Concrete types it constructs or calls (`URLSession.shared`, `Retrofit`, disk, analytics SDK)
- `switch` / `when` / if-else on kind

### 2. Naming test

Write one sentence: "This type _____."

- Pass: one job, no and/or/but.
- Fail: split until each name passes.

### 3. Reasons to change

List each actor/force that would force an edit (API shape, date format, analytics vendor, payment method, storage…).

- **1 reason** → keep, still run cohesion / OCP / DIP.
- **2+ reasons** → split. One new type per reason. The original type, if it remains, only orchestrates.

### 4. Cohesion map

For each method, note which fields it uses.

- One cluster → cohesive.
- Two or more clusters → each cluster is a missing class (extract it).
- Locals always passed together after an extract → those locals are a missing class, not a long parameter list.

### 5. Open/Closed

If a switch on kind must grow for every new case: replace it with a small protocol/interface and **one type per variant**. Adding a variant must be a new type, not an edit to a working class.

### 6. Depend on abstractions

If policy knows a concrete I/O type:

- Introduce a small protocol/interface for the role (e.g. `AuthClient`, `UserLoading`).
- Inject it through `init` / constructor.
- Wire the concrete only at the composition root (app factory / DI graph).
- In tests, pass a fake. Never make private methods internal "so we can test them."

### 7. Execute the split

Use the **project’s** language, naming, and existing patterns (protocol vs interface, `final class` vs `data class`). Do not invent a new architecture layer.

For each extracted type:

- Honest name (the 25-word sentence).
- One reason to change.
- Collaborators injected, not constructed as hidden singletons.

Then **re-run steps 2–6 on every new type**. Stop only when each one passes. If a new type still fails, split again.

Do not stop at a plan when the user asked to clean/split the class. Write the code.

### 8. Report

Use this shape (short):

```
## Class audit: <OriginalName>

Naming test: PASS | FAIL — <one sentence>
Reasons to change: <N>
- <reason> → <NewType>
- …

Cohesion: one cluster | split <cluster> → <NewType>
Open/Closed: no kind-switch | replaced switch with <Protocol>
DIP: already abstract | extracted <Protocol>, wired at <composition root>

Split: yes | no
Types now:
- <Type> — <one reason>
- …

Call sites updated: <files>
```

## Refuse and rewrite

| Request | Do this instead |
|---------|-----------------|
| "Just put it in the ViewModel" | Split by reason to change; ViewModel orchestrates |
| "One helper for all of this" | One type per job, honest names |
| "Keep it in a single file" | Many small types; moving parts you can see |
| "Make private methods internal to test them" | Extract the missing type; test that |
| "Add another case to the switch" | New type honoring the protocol |
| "Call URLSession/Retrofit in the use case" | Inject an abstraction; fake it in tests |

## Additional resources

- Worked messy → split examples: [examples.md](examples.md)
- Install on other tools: [PORTABLE.md](PORTABLE.md)
