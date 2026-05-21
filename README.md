# skills

Custom slash commands for AI assistants, used across [Claude Code](https://claude.ai/code) and [Pi](https://pi.dev).

Each skill is a `SKILL.md` file that teaches the assistant how to perform a specific task or interact with a specific tool. Skills are sourced from upstream repositories (primarily [`mitsuhiko/agent-stuff`](https://github.com/mitsuhiko/agent-stuff) and [`googleworkspace/cli`](https://github.com/googleworkspace/cli)) and pinned to specific revisions.

## Skills

| Skill | Description |
|-------|-------------|
| `commit` | Create Conventional Commits-style git commits |
| `github` | Interact with GitHub via the `gh` CLI |
| `grill-me` | Interactive Q&A / knowledge testing |
| `gws-calendar` | Google Calendar API access |
| `gws-calendar-agenda` | View calendar agenda |
| `gws-calendar-insert` | Create calendar events |
| `gws-docs` | Google Docs API access |
| `gws-docs-write` | Write to Google Docs |
| `gws-gmail` | Gmail API — send, read, and manage email |
| `gws-gmail-read` | Read Gmail messages |
| `gws-shared` | Shared auth/config for Google Workspace skills |
| `hunk-review` | Review code hunks |
| `morning-digest` | Daily briefing: unread email, Slack mentions, and calendar |
| `sentry` | Query Sentry for errors and issues |
| `summarize` | Summarize content into markdown |
