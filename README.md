# Claude Skills Library

A company-wide library of Claude Code skills for the team at kdweb.

## Usage

Clone the library into your local Claude skills directory:

```bash
gh repo clone palmeheskd/claude-skills ~/.claude/skills/claude-skills
```

Pull updates when new skills are added:

```bash
cd ~/.claude/skills/claude-skills && git pull
```

Skills activate automatically in your next Claude Code session.

## Contributing

Anyone can create a skill and submit it for review. **Only @palmeheskd can merge to main.**

1. Create your skill in `~/.claude/skills/claude-skills/<skill-name>/` — use `/skill-creator` to help
2. Push to a branch and open a PR
3. @palmeheskd reviews and merges

Do not push directly to `main` — the branch is protected.

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
| [transcript-to-tasks](transcript-to-tasks/) | Convert any transcript, email, or discussion into Asana tasks |
