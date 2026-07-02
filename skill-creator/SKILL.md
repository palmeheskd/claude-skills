---
name: skill-creator
description: >
  Create, structure, and write new skills for the claude-skills GitHub library.
  Use this skill whenever the user wants to add a new skill to the library,
  create a SKILL.md, design a skill workflow, or figure out how to package
  a repeatable task as a skill. Also use it when the user describes a workflow
  they do repeatedly and wants Claude to handle it automatically in future sessions.
---

# Skill Creator

A skill for adding new skills to the `palmeheskd/claude-skills` library.

## What a skill is

A skill is a directory in this repo with a `SKILL.md` file. It gives Claude
focused, domain-specific instructions for a particular task — invoked via
`/skill-name` in Claude Code.

```
skill-name/
├── SKILL.md          # required — instructions + frontmatter
└── references/       # optional — docs, schemas, examples
└── scripts/          # optional — helper scripts the skill can run
└── assets/           # optional — templates, icons, static files
```

## Process

### 1. Understand what the skill should do

Ask:
- What task should this skill handle?
- When should it trigger? (what phrases, file types, contexts)
- What's the expected output?
- Are there edge cases or variants to handle?

### 2. Write the SKILL.md

Every SKILL.md needs:

**Frontmatter** (required):
```yaml
---
name: skill-name          # kebab-case, matches directory name
description: >            # primary trigger mechanism — be specific and
  ...                     # include BOTH what it does AND when to use it.
                          # Lean toward being "pushy" — Claude undertriggers
                          # skills, so err on the side of listing more contexts.
---
```

**Body** — markdown instructions for Claude. Include:
- What to do step by step
- Why each step matters (don't just list MUSTs — explain the reasoning)
- Output format if it matters
- Examples where helpful

**Style rules:**
- Imperative voice ("Read the file", not "You should read the file")
- Explain the *why* behind instructions — Claude is smart, not a shell script
- Keep SKILL.md under 500 lines; move large references to `references/`
- No filler — every line should earn its place

### 3. Create the directory and file

Write the skill into the local clone of the library:

```
~/.claude/skills/claude-skills/<skill-name>/SKILL.md
```

### 4. Submit for review — do NOT push to main

The library is gatekeeper-controlled. Only @palmeheskd can merge to main.
Submit the skill as a pull request:

```bash
cd ~/.claude/skills/claude-skills
git checkout -b add/<skill-name>
git add <skill-name>/
git commit -m "add <skill-name> skill"
git push origin add/<skill-name>
gh pr create \
  --title "add: <skill-name>" \
  --body "**What it does:** ...\n**When it triggers:** ...\n**Tested with:** ..."
```

### 5. Confirm with the user

Tell the user:
- What the skill does and when it triggers
- The PR link to share with @palmeheskd for review
- That it will be available to the whole team once merged

Do not push directly to main — the branch is protected.

---

## Description writing tips

The `description` field is what Claude reads to decide whether to invoke the skill.
Good descriptions are specific and mention concrete trigger contexts:

**Weak:** "Helps with Excel files."

**Strong:** "Create, read, transform, and analyze Excel (.xlsx) files. Use when
the user mentions spreadsheets, needs to add/edit columns, calculate totals,
reformat data, or export Excel as CSV. Also use when the user pastes column
names or describes a data table and wants something done with it."

Include near-miss contexts explicitly if there's risk of confusion with another skill.

---

## Skill body patterns

**Defining output format:**
```markdown
## Output format
Always produce a summary with this structure:
### [Title]
**Result:** ...
**Files changed:** ...
```

**Examples:**
```markdown
## Example
Input: "add a profit margin column, revenue is C, costs is D"
Output: reads the file, adds column E = (C-D)/C formatted as %, saves in place
```

**Referencing bundled files:**
```markdown
See `references/api-schema.md` for the full field list before making API calls.
```
