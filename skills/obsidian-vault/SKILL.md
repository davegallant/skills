---
name: obsidian-vault
description: Search, create, and manage notes in Dave's Obsidian vault (Daily Notes, Pages, Attachments). Use when the user wants to find, create, or organize notes in Obsidian.
---

# Obsidian Vault

## Vault location

`~/Documents/obsidian-vault`

Not a git repository — no commit history or diff-based undo. Treat bulk moves/deletes/renames as hard to reverse; Obsidian's file-recovery plugin is the only safety net.

## Structure

- `Daily Notes/YYYY/MM/YYYY-MM-DD.md` — one file per day, nested by year and month. Enforced by the Daily Notes plugin config (`folder: "Daily Notes"`, `format: "YYYY/MM/YYYY-MM-DD"`); Obsidian creates new daily notes in this layout automatically.
- `Pages/` — flat folder of topic/reference notes (infrastructure systems, incidents, people, vacation handovers, interview notes, etc.). One note per subject, no further subfolders.
- `Attachments/` — flat folder at vault root holding every image/screenshot in the vault.
- `TODO.md` — root-level scratch task/ticket list.

## Linking

- Use Obsidian `[[wikilinks]]` syntax for notes: `[[Note Title]]`.
- Screenshots pasted in Obsidian are embedded as path-less wikilinks, e.g. `![[Pasted image 20260528114742.png]]` — these resolve by filename search across the vault and survive moves.
- Images imported from the prior Logseq vault (filenames like `image_<timestamp>_0.png`) use relative markdown links, e.g. `![image.png](../../../Attachments/image_1742218783821_0.png)`. These break if the note or `Attachments/` moves — the `../` depth depends on folder nesting (3 levels under `Daily Notes/YYYY/MM/`, 1 level under `Pages/`).

## Workflows

### Search for notes

```bash
# Search by filename
find ~/Documents/obsidian-vault -name "*.md" | grep -i "keyword"

# Search by content
grep -rl "keyword" ~/Documents/obsidian-vault --include="*.md"
```

Or use Grep/Glob tools directly on the vault path.

### Create a new page note

1. Add `Pages/<Title>.md` using Title Case for the filename.
2. Add `[[wikilinks]]` to related notes at the bottom.

### Append to today's daily note

Path is `Daily Notes/<YYYY>/<MM>/<YYYY-MM-DD>.md` for today's date. Create the year/month folders if they don't already exist.

### Find related notes / backlinks

```bash
grep -rl "\[\[Note Title\]\]" ~/Documents/obsidian-vault
```

### Check the TODO list

`TODO.md` at the vault root holds scratch tasks/tickets.
