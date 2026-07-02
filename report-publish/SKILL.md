---
name: report-publish
description: >
  Publish an HTML report to Cloudflare Pages at kdweb.co.uk using Wrangler.
  Use this skill when the user says "publish the report", "deploy this",
  "push to Cloudflare", "make this live", or "share the report URL". Also
  use it when the user has just finished verifying and formatting a report
  and asks what to do next — publishing is the natural final step.
---

# Report Publisher

Deploys HTML reports to Cloudflare Pages at kdweb.co.uk using `wrangler pages deploy`.

## Prerequisites

- `wrangler` must be authenticated (`wrangler whoami` should return an account)
- The Cloudflare Pages project name for kdweb.co.uk must be known (see below)

## Process

### 1. Confirm what's being published

Identify the HTML file or directory to deploy. If it's a single file,
it may need to be in a directory — `wrangler pages deploy` works on directories.

If the user hasn't specified, ask: "Which file should I publish?"

### 2. Find the Pages project name

Run `wrangler pages project list` to see available projects. Match to
kdweb.co.uk — it's likely named `kdweb` or similar. Note it for future use.

### 3. Prepare the deployment directory

If deploying a single HTML file:
```bash
mkdir -p /tmp/publish-staging
cp <report-file> /tmp/publish-staging/index.html
```

If the report has associated assets (CSS, images, charts), copy them all
into the staging directory maintaining their relative paths.

### 4. Deploy

```bash
wrangler pages deploy /tmp/publish-staging \
  --project-name <project-name> \
  --branch main
```

### 5. Confirm and share the URL

After successful deployment, show the user:
- The live URL (kdweb.co.uk or the Cloudflare Pages URL)
- Deployment timestamp
- A one-line summary of what was published

Example:
```
✅ Published: Q2 2025 Revenue Report
🔗 https://kdweb.co.uk/reports/q2-2025
⏱  Deployed at 14:32 UTC
```

## Error handling

- **Auth error**: Run `wrangler login` and ask the user to authenticate
- **Project not found**: List projects with `wrangler pages project list`
  and ask the user to confirm the correct project name
- **Build errors**: Check that all asset paths in the HTML are relative,
  not absolute local paths (e.g. `./charts/q2.png` not `/Users/...`)

## Notes

- Always run `/report-verify` and `/report-format` before publishing unless
  the user explicitly says they've already checked
- Clean up `/tmp/publish-staging` after deployment
