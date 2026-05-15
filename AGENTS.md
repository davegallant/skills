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

<!-- origin: https://github.com/upstream/repo (rev: <sha>) -->

# My Skill

...body...
```

Required frontmatter fields:

- `name` — must match the parent directory name; lowercase letters,
  digits, and single hyphens only.
- `description` — what the skill does and when to invoke it. Be
  specific; this is what the agent sees when deciding to load the
  skill.

## Attribution

Skills in this repo are sourced from upstream projects and pinned to a
specific revision. Each `SKILL.md` carries a single-line attribution
comment **immediately after** the closing `---` of its frontmatter:

```markdown
<!-- origin: <upstream-url> (rev: <sha-or-tag>) -->
```

When syncing or adding a new skill, preserve (or add) this comment so
the upstream source stays traceable. Do **not** put it above the
frontmatter — see [SKILL.md Format](#skillmd-format).

### Current sources

| Upstream | Skills |
|----------|--------|
| [`mitsuhiko/agent-stuff`](https://github.com/mitsuhiko/agent-stuff) | `commit`, `github`, `librarian`, `native-web-search`, `sentry`, `summarize`, `web-browser` |
| [`googleworkspace/cli`](https://github.com/googleworkspace/cli) | `gws-calendar`, `gws-calendar-agenda`, `gws-calendar-insert`, `gws-docs`, `gws-docs-write`, `gws-gmail`, `gws-gmail-read`, `gws-shared` |
| [`mattpocock/skills`](https://github.com/mattpocock/skills) | `grill-me` |
| [`modem-dev/hunk`](https://github.com/modem-dev/hunk) | `hunk-review` |

When updating a skill from upstream:

1. Re-sync the file contents from the new upstream revision.
2. Update the `rev:` (or version tag) in the origin comment.
3. Keep the comment positioned **after** the frontmatter.
4. Update the README table if the skill's surface changes.

## Adding a New Skill

1. Create `skills/<name>/` matching the `name` field.
2. Write `SKILL.md` with the format shown above.
3. Add an origin comment if sourced from upstream; omit it for
   skills authored here.
4. Add a row to the table in `README.md`.

## Validation Checklist

Before committing changes to any `SKILL.md`:

- [ ] First line is `---` (no leading comment, BOM, or blank line).
- [ ] `name` matches the parent directory.
- [ ] `description` is present and specific.
- [ ] Origin comment (if any) sits between the closing `---` and the
      first content line.
- [ ] No stray shell-escape artifacts like `<\!--` (use plain `<!--`).
