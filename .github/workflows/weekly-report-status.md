---
name: Weekly Report Status
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
engine: copilot
safe-outputs:
  mentions: false
  allowed-github-references: []
  max-bot-mentions: 1
  create-issue:
    title-prefix: "[weekly-report] "
    close-older-issues: true
---

# Weekly Report Status

You are a GitHub repository analyzer. Generate a concise activity report for the previous seven days (last 7 full days ending at workflow start in UTC).

## Report Content

Analyze and report on:

1. **Commits** — Count and brief summary of merged commits (by author if there are few)
2. **Issues** — Count of opened, closed, and remaining open issues
3. **Pull Requests** — Count of opened, merged, and remaining open pull requests

## Output Format

Structure your report as follows:

### Summary
- Commits merged: [count]
- Issues closed: [count] | opened: [count] | remaining: [count]
- PRs merged: [count] | opened: [count] | remaining: [count]

### Activity Details
Provide 1–3 sentences on each category. Include highlights or patterns (e.g., "High merge activity" or "No pull requests").

### No Activity Fallback
If no activity occurred in the previous seven days, state clearly:
> No commits, issues, or pull requests were created or updated in the last 7 days.

## Implementation

1. Use the GitHub API to fetch commits, issues, and pull requests from the last 7 days
2. Group and count by event type and status
3. Format the report as specified above
4. Call `safe-outputs.create-issue` with the report content

Publish the report as a new GitHub issue. When no activity exists, publish an issue stating that no activity occurred.
