# Claude Skills Library

A company-wide library of Claude Code skills for the team at kdweb.

## Usage

Add this repo as a skills source in your Claude Code settings (`~/.claude/settings.json`):

```json
{
  "skills": {
    "sources": ["github:palmeheskd/claude-skills"]
    }
}
```

Then use skills with `/skill-name` in any Claude Code session.

## Skills

| Skill | What it does |
|-------|--------------|
| [skill-creator](skill-creator/) | Create and add new skills to this library |
| [asana-task](asana-task/) | Create Asana tasks instantly using the team's fixed template |
| [report-verify](report-verify/) | Verify all numbers in an HTML report against source data (catches hallucinations) |
| [report-format](report-format/) | Check a report against the team's GitHub template for structure and formatting |
| [report-publish](report-publish/) | Publish HTML reports to Cloudflare Pages at kdweb.co.uk |
| [work-log](work-log/) | Document work in GitHub and capture repeatable workflows as skills |
| [slack-announce](slack-announce/) | Announce updates and reports to the right internal Slack channels |
