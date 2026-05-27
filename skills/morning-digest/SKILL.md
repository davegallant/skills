---
name: morning-digest
description: Use when the user asks for a morning digest, daily briefing, or wants a summary of unread emails, Slack notifications, and upcoming calendar events
---

# Morning Digest

Compile a morning briefing covering unread emails, Slack activity directed at you, and upcoming calendar events.

## Workflow

Run these three data-gathering steps in parallel, then present a unified digest.

### 1. Unread Emails

Use `mcp__claude_ai_Gmail__search_threads` with query `is:unread` to fetch unread threads.

Summarize the unread inbox: group by sender or theme, highlight anything urgent or time-sensitive.

### 2. Slack Mentions and DMs

Use `slack_search_public_and_private` to find recent messages (last 24 hours) directed at you:

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

Use `mcp__claude_ai_Google_Calendar__list_events` to fetch:
- Today's events (set `time_min` to start of today, `time_max` to end of today)
- Rest of the week (set `time_max` to end of the week)

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
