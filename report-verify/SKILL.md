---
name: report-verify
description: >
  Verify all numbers, statistics, and data points in an HTML report against
  the original data sources to catch hallucinations and errors. Use this skill
  whenever the user asks to "verify the report", "check the numbers", "fact-check
  this", or "make sure the data is right". Also use it automatically after
  generating any HTML report that contains statistics, percentages, totals, or
  figures — always offer to verify before the user publishes.
---

# Report Verifier

Re-reads original data sources and cross-checks every number in an HTML report.
This exists because Claude can hallucinate figures when generating reports —
this skill catches those errors before they reach anyone else.

## Process

### 1. Identify the report and data sources

Ask the user (if not already clear):
- Which HTML file is the report?
- Where is the source data? (CSV, spreadsheet, database query output, etc.)

If source files aren't provided, ask for them — you cannot verify without them.

### 2. Extract all claims from the report

Read the HTML report and list every specific data claim:
- Numbers and statistics (totals, averages, percentages, growth rates)
- Date ranges referenced
- Named entities with attached figures (e.g. "Product A: £42,000")
- Rankings or comparisons ("up 12% from last month")

Build an internal checklist of each claim.

### 3. Re-read the source data independently

Read the source data files from scratch — do not rely on what was used to
generate the report. Calculate the same figures yourself:
- For totals: sum the relevant column
- For percentages: calculate numerator ÷ denominator × 100
- For comparisons: pull both periods and compute the delta

This is the core of the skill — you're acting as an independent auditor,
not re-confirming your own prior work.

### 4. Compare and report

For each claim in the report, state whether it matches the source data.

**Format:**

```
## Verification results

✅ Revenue total (£128,450) — matches source (sum of column C: £128,450)
✅ Growth rate (14%) — confirmed (128,450 / 112,675 - 1 = 14.0%)
❌ Top product (Widget X: £32,000) — source shows £29,800. Widget Y (£31,200) is actually top.
⚠️  Date range "Jan–Mar 2025" — source data runs Jan 6–Mar 28, not full months
```

Use ✅ for confirmed, ❌ for wrong, ⚠️ for approximate or needs clarification.

### 5. Fix errors

For any ❌ findings, offer to correct the HTML report directly. Fix only the
specific numbers — do not rewrite or reformat anything else.

## Important

- If source data is ambiguous (multiple possible interpretations of a figure),
  flag it as ⚠️ and explain the ambiguity — do not guess which interpretation
  was intended
- After fixing errors, re-run verification on the corrected report to confirm
  all ✅ before the user publishes
