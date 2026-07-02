---
name: report-format
description: >
  Check whether a report follows the team's standard reporting structure and
  template from GitHub. Use this skill when the user asks to "check the format",
  "does this follow our template", "is this report correct", "review the
  structure", or before publishing any report. Also use it automatically when
  the user shares a draft report and hasn't mentioned format checking — always
  check format before suggesting publication.
---

# Report Format Checker

Compares a report against the team's official reporting template stored in
GitHub and flags any structural or formatting deviations.

## Process

### 1. Fetch the official template from GitHub

The template/structure lives in the team's GitHub repo. Use the GitHub CLI
to fetch it:

```bash
gh repo view --json name   # confirm the right repo is in context
gh api repos/{owner}/{repo}/contents/{path} --jq '.content' | base64 -d
```

If you don't know the repo or path, ask the user: "Where is the reporting
template stored in GitHub?" Note the answer for future uses.

### 2. Read the report being checked

Read the report file the user has provided or created in this session.

### 3. Compare structure

Check for these elements in order:

**Required sections** — does the report contain all sections defined in the
template? Flag any that are missing or out of order.

**Section content rules** — does each section follow the template's
requirements (e.g. executive summary must be 3 bullets, charts must have
titles and axis labels)?

**Formatting rules** — number formatting (currency symbols, decimal places,
thousands separators), date formats, colour usage, font headings (in HTML).

**Branding** — logo presence, correct company name, footer content.

### 4. Report findings

```
## Format check results

✅ All required sections present and in correct order
✅ Executive summary: 3 bullets ✓
❌ Section missing: "Data sources" — required by template, not found
❌ Revenue figures: formatted as "128450" — template requires "£128,450"
⚠️  Chart on page 2 has no title — template recommends but doesn't require
```

List all issues. For ❌ items, explain exactly what the template requires.

### 5. Fix on request

If the user says "fix it" or "correct the format", apply all ❌ corrections
directly to the file. Leave ⚠️ items for the user to decide.

After fixing, re-run the check to confirm all ✅.

## Notes

- If the template has changed since this report style was established, note
  the discrepancy and ask which version to enforce
- Structural issues (wrong sections, wrong order) are more important than
  cosmetic ones (exact spacing, minor colour variations) — prioritise them
