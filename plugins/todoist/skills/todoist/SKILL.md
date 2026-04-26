---
name: todoist
description: Interact with Todoist via the MCP server to query, create, update, and complete tasks
---

## Overview

Todoist is connected via an MCP server. The MCP tools are available directly — no CLI needed. Configure the Todoist MCP in `.claude/settings.local.json`:

```json
{
  "mcpServers": {
    "todoist": {
      "type": "url",
      "url": "https://ai.todoist.net/mcp"
    }
  }
}
```

## Available MCP Tools

The Todoist MCP server exposes tools for task and project management. Common tools include:

- **Get tasks** — Retrieve tasks with optional filters (today, overdue, by project, by priority)
- **Create task** — Add a new task with content, due date, priority, project, and labels
- **Update task** — Modify an existing task's content, due date/time, priority, or project
- **Complete task** — Mark a task as done
- **Get projects** — List all projects

## Key Patterns

### Querying today's tasks

Fetch tasks due today and any overdue items. Look for filter parameters like `filter` (uses Todoist filter syntax) or date-based parameters.

Useful Todoist filter strings:

- `today` — tasks due today
- `overdue` — past-due tasks
- `today | overdue` — both
- `p1` — priority 1 (urgent)
- `p1 | p2` — high priority
- `no date` — unscheduled tasks
- `#ProjectName` — tasks in a specific project
- Combine with `&` (AND) and `|` (OR): `(today | overdue) & p1`

### Setting due dates

Update a task's due string using Todoist natural language:

- `today` — due today (no specific time)
- `today at 10:00` — due today at 10:00 AM
- `tomorrow` — due tomorrow
- `next week` — due next Monday
- `Feb 16` — specific date
- `every Monday` — recurring

### Rescheduling patterns

Common during grooming and reviews:

- Move overdue to today: set due string to `today`
- Defer to tomorrow: `tomorrow`
- Defer to next week: `next Monday`
- Remove due date: clear the due string (someday/unscheduled)

## Operating Constraints

- **Read operations** (get tasks, get projects, list labels): Execute freely, no approval needed
- **Write operations** (create, update, complete, delete tasks): Always require explicit user approval before executing
- **Batch updates**: When updating multiple tasks (e.g., scheduling), present the full list of changes first and get a single approval for the batch
- Keep task queries focused — don't dump the entire backlog. Filter to what's relevant for the current context.
