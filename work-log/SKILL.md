---
name: work-log
description: >
  Document what was worked on in GitHub — as a commit, PR description, issue
  comment, or changelog entry — and optionally capture repeatable workflows
  as new skills in the claude-skills library. Use this skill when the user
  says "log what we did", "document this", "add this to GitHub", "write up
  what I worked on", or when a session ends and the work hasn't been committed
  yet. Also use it when the user has just built something repeatable and should
  capture it as a skill.
---

# Work Logger

Documents work in GitHub and captures repeatable workflows as skills.

## Two modes

This skill does two things — often both in the same session:

1. **GitHub documentation** — commit messages, PR descriptions, issue comments, changelogs
2. **Skill capture** — turning a repeatable workflow into a new skill for the library

---

## Mode 1: GitHub documentation

### What to document

Read the conversation to understand what was worked on:
- Files created or modified
- Problems solved and how
- Decisions made and why
- What's next or still open

### Commit message format

```
<type>(<scope>): <short summary>

<body — what changed and why, not how>

<footer — links, closes #issue, co-authors>
```

Types: `feat`, `fix`, `docs`, `refactor`, `chore`, `report`, `data`

Example:
```
report(q2): add revenue breakdown by region

Added regional split to Q2 report after request from leadership.
Data sourced from Salesforce export (2025-07-02).

Closes #42
```

### PR descriptions

If the user wants a PR description instead, write:
- **What** changed (1–2 sentences)
- **Why** it was needed
- **How to review** (what to look at, what to test)
- Checklist of anything still to do

### Process

1. Summarise the work from the conversation
2. Ask the user: commit, PR description, issue comment, or changelog?
3. Draft the documentation
4. If committing: `git add` the relevant files and `git commit`
5. If pushing: confirm with the user before `git push`

---

## Mode 2: Skill capture

If the work in this session involved a repeatable multi-step workflow,
offer to capture it as a skill in `palmeheskd/claude-skills`.

### When to suggest this

- The user ran the same sequence of steps they'd do again next week
- A workflow required looking up a non-obvious command or API
- The task took 5+ minutes but would take 30 seconds if it were a skill

### How to create the skill

Follow the `skill-creator` skill format:

1. Name the skill (kebab-case, action-oriented)
2. Write `SKILL.md` with frontmatter + instructions
3. Add it to `/tmp/claude-skills/<skill-name>/`
4. Commit and push to `palmeheskd/claude-skills`
5. Update README.md table

Tell the user: "I've added `/<skill-name>` to the library — it'll be available
in future sessions."

---

## Notes

- Don't over-document. A good commit message is 3–7 lines. If it needs more,
  the work should probably be split into separate commits.
- For skills: only capture workflows that are genuinely repeatable and
  would save real time. Don't create a skill for a one-off task.
