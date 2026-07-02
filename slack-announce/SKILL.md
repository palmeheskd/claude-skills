---
name: slack-announce
description: >
  Announce new things, updates, and reports on the team's internal Slack
  channels. Use this skill when the user says "announce this on Slack",
  "post to Slack", "let the team know", "share this in Slack", or "send
  a Slack message". Also use it after publishing a report or completing
  a major piece of work — proactively offer to announce it to the relevant
  channel.
---

# Slack Announcer

Posts announcements to the right Slack channels using the Slack MCP tools.

## Channel routing

Route announcements based on content type. If you're unsure which channel
to use, ask — don't guess and post to the wrong place.

| Content type | Default channel |
|---|---|
| New reports published | Ask user — likely a reporting or data channel |
| Product updates / features | Ask user — likely a product or engineering channel |
| Company / team news | Ask user — likely #general or #announcements |
| Data / analysis findings | Ask user — likely a data or analytics channel |
| Skill library updates | Ask user — likely a tools or internal channel |

On first use, ask the user to map their content types to channel names.
Note the mapping so future announcements go to the right place automatically.

## Process

### 1. Understand what to announce

Extract from context:
- What is being announced?
- Who is the audience?
- Is there a link or attachment to include?
- Any urgency or tone requirements?

### 2. Pick the channel

Use the routing table above. If the content type isn't covered, ask.
Use `slack_search_channels` to find the channel ID from the name.

### 3. Draft the message

Keep announcements concise and scannable:

```
*[What]* — Short title of what's new

[1–2 sentences of context: why it matters, what changed]

🔗 [Link if applicable]

/cc @[relevant people if needed]
```

Use Slack formatting (`*bold*`, `_italic_`, `• bullets`) where it helps clarity.
Don't use emoji heavily — one to signal the type of announcement is enough.

### 4. Confirm before sending

Always show the user the draft message and which channel it will go to
before sending. Ask: "Shall I post this?"

This is important — Slack messages are visible to the whole team immediately
and can't be unsent cleanly.

### 5. Send

Use `slack_send_message` with the channel ID and formatted message text.

After sending, confirm: "Posted to #[channel-name] ✓"

## Tone

Match the announcement tone to the channel:
- #general / #announcements: professional, clear, brief
- Team/project channels: can be more informal, include detail
- Leadership channels: crisp, outcome-focused, no jargon

## Notes

- For report announcements: include the live URL and a one-line summary of
  the key finding — don't just say "report is ready"
- For skill library updates: mention what problem the skill solves and how
  to invoke it (e.g. "Use `/report-verify` to fact-check any report before publishing")
- If announcing to multiple channels, send each message separately — don't
  cross-post with "also in #channel" references
