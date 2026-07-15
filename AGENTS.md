# AGENTS.md

Guidance for AI agents working in this repository.

## Repository Layout

```
skills/
  <skill-name>/
    SKILL.md          # frontmatter + instructions (required)
    ...               # optional helper scripts, references, assets
```

Every skill lives in its own directory under `skills/` and contains a
`SKILL.md` file conforming to the [Agent Skills
specification](https://agentskills.io/specification).

## SKILL.md Format

The very first line of every `SKILL.md` **must** be the opening `---`
of the YAML frontmatter. Anything before it (including HTML comments)
breaks frontmatter parsing in pi and other harnesses, which causes the
skill to fail to load with `description is required`.

Correct shape:

```markdown
---
name: my-skill
description: One-line description of what the skill does and when to use it.
---

# My Skill

...body...
```

Required frontmatter fields:

- `name` — must match the parent directory name; lowercase letters,
  digits, and single hyphens only.
- `description` — what the skill does and when to invoke it. Be
  specific; this is what the agent sees when deciding to load the
  skill.

## Adding a New Skill

1. Create `skills/<name>/` matching the `name` field.
2. Write `SKILL.md` with the format shown above.
3. Add a row to the table in `README.md`.

## Validation Checklist

Before committing changes to any `SKILL.md`:

- [ ] First line is `---` (no leading comment, BOM, or blank line).
- [ ] `name` matches the parent directory.
- [ ] `description` is present and specific.
- [ ] No stray shell-escape artifacts like `<\!--` (use plain `<!--`).
