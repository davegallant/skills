---
name: my-prs
description: "Use when the user runs /my-prs, or asks for their open pull requests, their review queue, or which PRs are awaiting their review."
---

# My PRs

Cross-repo GitHub PR status via `gh search prs`. `gh pr list` and `gh pr status`
are repo-scoped — don't use them here, even when inside a git repo.

The answer is these three sections, in this order.

## 1. Needs my review

```bash
gh search prs "user-review-requested:@me" --archived=false --state=open --limit 1000 \
  --json repository,number,title,author,updatedAt \
  --jq 'sort_by(.updatedAt)|reverse|.[]|"\(.repository.nameWithOwner)#\(.number) (@\(.author.login)) \(.title)"'
```

List every result. This is the actionable queue, so it leads.

## 2. My open PRs

```bash
gh search prs --author=@me --archived=false --state=open --limit 1000 \
  --json repository,number,title,isDraft,updatedAt \
  --jq 'sort_by(.updatedAt)|reverse|.[]|"\(.repository.nameWithOwner)#\(.number)\(if .isDraft then " [draft]" else "" end) \(.title)"'
```

List every result, most recently updated first, drafts marked `[draft]`.

## 3. Team review queue

```bash
gh search prs --review-requested=@me --archived=false --draft=false --state=open --limit 1000 \
  --json repository,number,title,updatedAt \
  --jq 'sort_by(.updatedAt)|reverse|.[]|"\(.repository.nameWithOwner)#\(.number) \(.title)"'
```

Report the total count, then the 10 most recent. It runs to dozens of PRs — show
the rest only when asked for them.

## Query gotchas

- `--review-requested` is **team-inclusive**: every PR routed to any team you
  belong to. `user-review-requested:` is direct-asks-only and has no flag — pass
  it as a **single** positional query string with everything else as flags.
  Splitting qualifiers across two positional args quotes them into one broken
  token and the search fails.
- `--limit` defaults to 30 and truncates silently.
- `--archived=false` drops PRs sitting in archived repos. They still count as
  open and are never actionable.
- A PR leaves both review-requested queues once you submit a review on it.
