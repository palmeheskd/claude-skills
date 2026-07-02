---
name: transcript-to-tasks
description: >
  Convert any transcript, meeting notes, email thread, Slack discussion, or
  voice memo into structured Asana tasks. Use this skill whenever the user
  pastes a conversation, discussion, meeting summary, or email and wants
  action items captured. Also use it when the user says "turn this into tasks",
  "extract the actions", "log what came out of this meeting", "make tasks from
  this thread", or shares any block of text describing work that needs to happen.
  Proactively offer this when a long discussion ends and no tasks have been logged.
---

# Transcript to Asana Tasks

Reads any unstructured text — meeting notes, email threads, Slack exports,
voice memo transcriptions — and creates properly structured Asana tasks from it.

## What counts as a task

Extract something as a task only if it is:
- **Assigned or assignable** — someone specific is responsible, or it's clear who should be
- **Actionable** — it describes concrete work, not a general observation
- **Not already done** — skip things marked as completed in the transcript

Do not create tasks for vague items like "we should think about X" or "it would
be good to explore Y" unless someone explicitly agreed to own it.

## Process

### 1. Read the full text first

Before extracting anything, read the entire transcript. Understanding the full
context helps distinguish real commitments from passing comments.

### 2. Extract action items

List every task you find with:
- **What**: a clear action-oriented description
- **Who**: the person responsible (use their name from the transcript)
- **When**: any deadline mentioned, even rough ones ("by end of week", "before the call")
- **Context**: one sentence of why this matters, if not obvious

If the transcript is ambiguous — "someone should handle X" — flag it and ask
the user who to assign it to before creating it.

### 3. Show the user your list before creating

Present the extracted tasks clearly and ask for confirmation:

```
I found 4 tasks in this transcript. Does this look right before I create them?

1. Update the Q3 slide deck with revised revenue figures
   → Sarah | By Thursday | From: "Sarah said she'd fix the numbers before the client call"

2. Send the contract draft to legal for review
   → James | No deadline mentioned — should I set one?

3. ...
```

This step matters — transcripts are noisy and you may misread intent. Let the
user correct or remove items before anything goes to Asana.

### 4. Create confirmed tasks in Asana

Once the user approves the list, create all tasks in one go using `create_tasks`.
For each task:
- Look up the assignee's Asana user ID via `get_users`
- Use `get_projects` to identify the right project (ask the user if unclear)
- Set the due date if one was mentioned; leave blank if none

### 5. Confirm

After creating, show a brief summary:

```
✅ Created 4 tasks in [Project Name]
• Update Q3 slide deck → Sarah, Thu 10 Jul
• Send contract to legal → James
• ...
```

## Handling different input formats

**Meeting notes**: Look for action items often prefixed with "AI:", "Action:", "→", or people's names followed by verbs.

**Email threads**: Focus on the most recent messages. Earlier messages are context; commitments are usually in the replies.

**Slack exports**: Timestamps and usernames are your friend. A message starting with a name and a verb ("James will send...") is almost always a task.

**Voice memo transcriptions**: These are messy. Read liberally and flag anything that sounds like a commitment, even if phrased casually.

## Notes

- If the transcript mentions many tasks across different projects, group them by project and confirm the grouping with the user before creating
- Never create duplicate tasks — if a task from this transcript already exists in Asana, skip it (check with `search_tasks` if the user is unsure)
