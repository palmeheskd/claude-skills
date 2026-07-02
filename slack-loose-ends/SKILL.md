---
name: slack-loose-ends
description: >
  Scan Slack for unresolved mentions, unanswered questions, and threads waiting
  for a response. Use this skill when the user says "check Slack for loose ends",
  "what's waiting for me on Slack", "any unresolved mentions", "what have I been
  tagged in", "Slack follow-ups", "what do I still need to reply to", or just
  "check Slack". Also use it proactively at the start of a working session when
  the user asks what needs their attention.
---

# Slack Loose Ends

Scans Slack for messages where the user was mentioned and identifies which ones
still need a response or action — the ones that have fallen through the cracks.

## What counts as a loose end

A loose end is a mention where something is still waiting:
- A direct question to the user that hasn't been answered
- A thread the user was tagged in where they haven't replied
- A decision or approval that was requested and not given
- A task assigned via Slack that hasn't been acknowledged

A mention is **not** a loose end if:
- The user has already replied in that thread
- The matter was resolved by someone else after the mention
- It was a general FYI with no action required (e.g. "cc @user just so you know")

## Process

### 1. Search for recent mentions

Use `slack_search_public_and_private` to find messages where the user was mentioned. Search for their @-handle. Start with the last 7 days unless the user specifies a different window.

```
query: "@[username]"
```

### 2. For each mention, check if it's resolved

Read the thread using `slack_read_thread` to see what happened after the mention:
- Did the user reply? → resolved, skip it
- Did someone else answer the question? → resolved, skip it
- Is the thread still waiting? → loose end, keep it

Don't just flag every mention — the goal is to surface only the ones that genuinely need attention.

### 3. Present the loose ends clearly

Group by urgency if there are many. For each loose end show:
- **Where**: channel and thread link if available
- **Who**: who mentioned them and when
- **What's needed**: one sentence on what action or reply is expected
- **Age**: how long it's been sitting

**Example output:**

```
Found 3 loose ends from the past 7 days.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔴  #client-acme · 3 days ago
    Sarah asked if you'd reviewed the contract draft before she sends it.
    Thread has no reply from you yet.

🟡  #design · 2 days ago  
    Tom tagged you asking which logo version to use for the pitch deck.
    Still unresolved — Tom replied asking again yesterday.

🟢  #general · 5 hours ago
    James mentioned you when sharing the new brief. No question asked
    but he hasn't had a response — may just need an acknowledgement.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Use 🔴 for mentions with a direct question or pending decision that's been waiting more than 48 hours, 🟡 for recent or less urgent ones, 🟢 for FYIs that might just need a quick acknowledgement.

### 4. Offer to act

After showing the list, ask: "Want me to draft a reply for any of these?"

If the user says yes, read the full thread context and draft a reply that fits the conversation — matching their usual tone, not a generic response.

## If there are no loose ends

Say so simply: "Nothing unresolved from the past 7 days — you're up to date."
Don't pad it.

## Notes

- Focus on private channels and DMs too, not just public channels — mentions in DMs are often the most time-sensitive
- If the search returns a very large number of mentions (20+), ask the user if they want to narrow to a specific channel or time window before reading every thread
- Don't flag mentions from automated bots or app notifications
