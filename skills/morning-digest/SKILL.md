---
name: morning-digest
description: Use when the user asks for a morning digest, daily briefing, or wants a summary of unread emails, Slack notifications, and upcoming calendar events
---

# Morning Digest

Compile a morning briefing covering unread emails, Slack activity directed at you, and upcoming calendar events.

## Workflow

Run these three data-gathering steps in parallel, then present a unified digest.

### 1. Unread Emails

```bash
gws gmail +triage
```

Summarize the unread inbox: group by sender or theme, highlight anything urgent or time-sensitive.

### 2. Slack Mentions and DMs

Use `slack_search_public` to find recent messages directed at you:

```
query: "to:me"
sort: timestamp
sort_dir: desc
limit: 20
after: <yesterday's Unix timestamp>
```

Also check for recent direct messages by searching:

```
query: "in:<@YOUR_USER_ID>"
sort: timestamp
sort_dir: desc
limit: 10
after: <yesterday's Unix timestamp>
```

Group results by channel/sender. Highlight questions awaiting your response, action items, and FYIs.

### 3. Calendar

```bash
# Today's schedule
gws calendar +agenda --today

# Rest of the week
gws calendar +agenda --days 5
```

### Presenting the Digest

Combine everything into a single briefing:

```
## Morning Digest — <today's date>

### Email
- <count> unread messages
- <grouped summary with urgent items first>

### Slack
- <mentions and DMs grouped by channel/person>
- <items needing response highlighted>

### Calendar
**Today:**
- <today's events with times>

**This week:**
- <notable upcoming events>
```

Keep each section concise — 3-5 bullets max. Flag items that need action vs. FYI.
