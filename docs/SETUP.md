# Setup Guide

This guide explains how to reproduce the HireFlow AI demo workflow in n8n.

## Requirements

- n8n account or self-hosted n8n instance
- OpenRouter account and API key
- Gmail account with n8n OAuth2 configured
- A public webhook URL (n8n Cloud, Cloudflare Tunnel, or similar)
- An application form that POSTs `name`, `email`, `phone`, and a file field named `resume`

## 1. Import The Workflow

1. Open n8n.
2. Create a new workflow.
3. Import `workflow.json`.
4. Open **LLM - OpenRouter** and attach your own OpenRouter credential.
5. Open both Gmail nodes and attach your own Gmail OAuth2 credential.
6. Save the workflow and copy the production or test webhook URL.

## 2. Configure The Screening Prompt

Open **Resume Screening Agent** and replace the placeholder block:

- `ROLE TITLE`
- `KEY REQUIRED SKILLS`
- `MINIMUM QUALIFICATION`
- `SHORTLIST THRESHOLD`

Keep the JSON output contract. The Code node looks for `total_score` and `decision`.

## 3. Connect The Form

The webhook expects a POST. Recommended fields:

| Field | Type | Notes |
|---|---|---|
| `name` | text | Used in the email greeting |
| `email` | text | Used as the Gmail recipient |
| `phone` | text | Optional for screening, useful if you later store leads |
| `resume` | file | Must match the Extract From File binary property `resume` |

If your form sends a different file field name, change `binaryPropertyName` in **Extract Resume Text**.

## 4. Test Both Paths

Submit one strong resume and one weak resume.

Expected shortlist path:

- Agent returns `decision: SHORTLISTED` and `total_score >= 80`
- **Send Shortlist Email** runs

Expected rejection path:

- Agent returns a lower score or `DISQUALIFIED`
- **Send Rejection Email** runs

## 5. Optional Hosting Notes

The original demo used self-hosted n8n in Docker and a Cloudflare Tunnel so the form could reach the webhook. Those deployment files are not required to understand or import the workflow.

After import, credentials must be created privately inside your n8n instance. The public export contains placeholders only.
