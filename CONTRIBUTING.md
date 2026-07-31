# Contributing

Thanks for helping grow **Community AI Skills**.

## Contribution workflow (required)

**Direct pushes to `main` are not allowed.** All changes must go through a pull request (merge request).

1. Fork the repository (or create a branch from `main` if you have write access).
2. Make your changes on a feature branch.
3. Open a pull request against `main`.
4. Wait for review and merge.

Do not push commits straight to `main`.

## Add a new skill

1. Create a folder: `skills/<skill-name>/` (lowercase, hyphens).
2. Add at least `SKILL.md` with YAML frontmatter:

```markdown
---
name: skill-name
description: >-
  What it does. Use when the user asks for X, Y, or Z.
---

# Skill Title

## Instructions
...
```

3. Prefer adding `PORTABLE.md` (how to install on Cursor / Claude / Copilot / others).
4. Optionally add `examples.md` and a short `README.md`.
5. List the skill in the root [README.md](README.md) table.
6. Open a PR with a short description of the problem the skill solves.

## Skill quality bar

- **One concern** — split large topics into separate skills.
- **Actionable** — agents should know exactly what to do / refuse.
- **Framework-agnostic** when possible — “use the project’s existing stack.”
- **Description includes triggers** — keywords that help discovery.
- Keep `SKILL.md` focused (aim under ~500 lines); put long examples in `examples.md`.

## Improve an existing skill

PRs that clarify instructions, fix contradictions, or improve portability are welcome. Keep changes focused.
