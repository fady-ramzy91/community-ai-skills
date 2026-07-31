# Community AI Skills

A community catalog of reusable AI agent skills for Cursor, Claude, Copilot, and other assistants. Each skill is a self-contained set of instructions agents can load when writing code, tests, reviews, or docs — so teams share consistent practices across tools and projects.

Instead of rewriting the same prompts in every chat, you install a skill once and the agent applies those rules automatically. Skills are framework-agnostic where possible, portable across AI tools, and open for contribution.

## What’s here

| Skill | Description |
|-------|-------------|
| [clean-unit-testing](skills/clean-unit-testing/) | Clean Code Ch. 9 unit testing: Three Laws of TDD, one concept per test, F.I.R.S.T., readability — framework-agnostic |

More skills will land here over time. Contributions welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

## Quick install (Cursor)

Copy a skill into your personal or project skills folder:

```bash
# Personal (all your projects)
cp -R skills/clean-unit-testing ~/.cursor/skills/

# Or project-scoped (share with the team)
mkdir -p .cursor/skills
cp -R skills/clean-unit-testing .cursor/skills/
```

Then invoke with `@clean-unit-testing` or ask your agent to write unit tests — the skill description helps it auto-discover when relevant.

## Other tools

Each skill includes a `PORTABLE.md` with install snippets for Claude, GitHub Copilot, ChatGPT, and more.

## Skill layout

```text
skills/
  <skill-name>/
    SKILL.md       # Required — instructions the agent follows
    PORTABLE.md    # Recommended — install for any AI platform
    examples.md    # Optional — prompts / before-after examples
    README.md      # Optional — human-facing overview
```

## Principles for this repo

1. **One concern per skill** — don’t mix unrelated topics.
2. **Prefer principles over frameworks** — use the project’s existing tools when possible.
3. **Clear “when to use”** — every `SKILL.md` description should say what and when.
4. **Portable** — document how to use the skill outside Cursor.

## License

MIT — see [LICENSE](LICENSE).
