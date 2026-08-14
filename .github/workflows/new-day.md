---
name: New Day
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine: copilot
tools:
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

Update the Daily Updates section of index.html with today's date (UTC).

## Workflow Task

1. **Determine today's date in UTC format** — e.g., "14th of August"
2. **Check for existing date** — Search index.html for the current date. If it already exists in the Daily Updates navigation, call `noop("Date already exists")` and make no changes.
3. **Add navigation button** — Insert a new list item in the `.daily-updates-list` with:
   - A button with `class="daily-update-trigger"`
   - `type="button"`, `aria-haspopup="dialog"`
   - `aria-controls` pointing to a new dialog ID (e.g., "august-14-dialog")
   - A span containing the formatted date (e.g., "14th of August")
   - A span with `aria-hidden="true"` containing `&#8594;`
4. **Add matching dialog** — Insert a new `<dialog>` element:
   - `id` matching the `aria-controls` reference (e.g., "august-14-dialog")
   - `class="daily-update-dialog"`
   - `aria-labelledby` and `aria-describedby` pointing to header and content IDs
   - Standard header with close button
   - An h2 with a relevant question (e.g., a question about Agentic Workflows)
   - A paragraph with an answer
5. **Follow existing patterns** — Match the HTML structure, ID naming conventions, and styling of the existing August 1st entry. Do NOT modify styles.css.
6. **Preserve all existing updates** — Do not remove or modify existing daily update entries.
7. **Create a pull request** — Use `safe-outputs.create-pull-request` to propose the changes to index.html.

## Implementation Notes

- Use tools.edit to read and modify index.html
- The date format should follow the existing pattern (ordinal number + month name)
- Dialog IDs should follow the pattern: `[month-name]-[day]-dialog` in lowercase
- Only modify index.html; do not touch other files
- If the current UTC date is already present in the file, skip all modifications
