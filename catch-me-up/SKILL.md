---
name: catch-me-up
description: >
  Summarise any thread, email chain, Slack conversation, document, or meeting
  transcript so the user can get up to speed quickly. Use this skill when the
  user pastes a long block of text and wants to understand it, says "catch me
  up", "summarise this", "what did I miss", "what's going on in this thread",
  "tldr", or shares something long and asks what they need to know. Also use it
  when the user is about to join a conversation or meeting and needs context fast.
---

# Catch Me Up

Reads any thread, document, or conversation and gives the user a fast,
scannable summary of what actually matters.

## What a good summary looks like

The goal is not to compress the text — it's to tell the person what they
need to know to act. That means:

- **What happened** — the key events or exchanges, in order if it matters
- **Decisions made** — anything that was agreed, resolved, or concluded
- **What's still open** — unresolved questions, outstanding actions, ongoing tensions
- **What needs your attention** — anything that requires the user to respond, decide, or act

Not every section applies to every thread. Skip ones that aren't relevant —
don't pad the summary to fill all four.

## Format

Lead with a one-sentence headline — what this is and where things stand.
Then use short bullet points, not paragraphs. Keep it scannable.

**Example output:**

```
The Q3 report review thread — still waiting on two sign-offs before it can go out.

**What happened**
• Sarah flagged an error in the revenue figures on Tuesday
• James corrected them and sent a revised version Wednesday morning
• Client was notified of the delay; they're fine with Thursday delivery

**Still open**
• Mark hasn't approved the revised version yet
• No one has confirmed which chart to use on page 4

**Your attention needed**
• Mark is waiting to hear from you before he signs off
• Thursday deadline is tight — the file needs to go by noon
```

## Handling different input types

**Email chains** — read from oldest to newest. The most recent messages carry the current state; earlier ones are context.

**Slack threads** — timestamps and names matter. Note who said what if ownership is relevant.

**Documents** — focus on conclusions, decisions, and action items. Skip background that the user doesn't need to act on.

**Meeting transcripts** — distinguish between discussion (what was said) and outcomes (what was decided or agreed). Prioritise outcomes.

## Length

Match length to complexity. A 5-message email thread gets 5 bullets. A 40-page document gets a page. Never pad; never over-compress. The right length is whatever lets the person act without re-reading the source.

## If the content is ambiguous

If something is genuinely unclear — an unresolved disagreement, an unclear decision, an action with no clear owner — say so explicitly. Don't smooth over uncertainty in the source material.
