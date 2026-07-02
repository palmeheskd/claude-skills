---
name: asana-task
description: >
  Create Asana tasks instantly using the team's fixed task template. Use this
  skill whenever the user says "create a task", "add to Asana", "log this in
  Asana", "make a task for", or describes work that should be tracked. Also
  use it when the user finishes describing a piece of work and hasn't logged
  it anywhere yet — proactively suggest creating an Asana task.
---

# Asana Task Creator

Creates properly structured Asana tasks using the team's fixed template,
via the Asana MCP tools.

## Task template

Every task must include these fields — do not skip any:

| Field | Source |
|-------|--------|
| **Name** | Clear, action-oriented title (verb + object, e.g. "Update Q3 revenue report") |
| **Description** | What needs to be done and why. Include relevant context, links, or data |
| **Assignee** | Who owns this — ask if not obvious from context |
| **Due date** | When it's needed — ask if not mentioned |
| **Project** | Which Asana project it belongs to — see below |

## Process

### 1. Extract task details from context

Read the conversation and pull out what you can. For anything missing,
ask in a single message — don't ask field by field.

Example: "I'll create the Asana task. Just to confirm: should this be assigned to you, and when does it need to be done by?"

### 2. Identify the right project

Use `get_projects` to list available projects. Match the task type to the
most relevant project. If ambiguous, ask the user to pick.

### 3. Create the task

Use `create_tasks` with all required fields. Set the assignee using their
Asana user ID (look up via `get_users` if needed).

### 4. Confirm

After creating, show the user:
- Task name
- Asana link (the `permalink_url` from the response)
- Assignee and due date

Keep it brief — one line each.

## Notes

- If the user mentions multiple tasks at once, create them all in the same turn
- For recurring task types (e.g. weekly reports), note the pattern so future
  invocations can pre-fill fields automatically
- Do not create duplicate tasks — if the user seems to be describing something
  already in Asana, check first with `search_tasks`
