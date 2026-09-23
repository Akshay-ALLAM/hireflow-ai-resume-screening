# Security Notes

This repository is prepared as a public portfolio project.

## What Is Not Included

- No real API keys
- No OAuth tokens
- No exported n8n credential secrets
- No live webhook URL
- No Cloudflare tunnel hostname
- No real applicant data
- No live Gmail addresses in sample files

## Public Workflow Export

`workflow.json` is a scrubbed public export.

Replaced or removed before publishing:

- OpenRouter credential id and name
- Gmail credential id and name
- webhook path and webhook id
- workflow id, version id, and instance id

After importing, configure your own credentials inside n8n.

## Media

- The demo GIF covers personal form fields from the original screen recording.
- Published screenshots use fictional values such as `Jane Doe` and `jane@example.com`.

## Before Reusing

Before publishing your own version, check:

- n8n credential IDs and names
- webhook URLs and webhook IDs
- OpenRouter model access and keys
- Gmail account used to send candidate email
- Screenshots with private data
- Git history for previously committed secrets

Do not enable the workflow against a public form until you have reviewed email templates and the sending mailbox.
