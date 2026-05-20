# Security Policy

## Reporting a vulnerability

If you find a security issue in this repository — including, but not limited to, accidentally committed credentials, hardcoded secrets, or any sensitive data that shouldn't be public — please **do not open a public issue**.

Instead, email **olawaleemmanuel100@gmail.com** with the details. I'll respond within 48 hours and patch immediately.

---

## What this repository does NOT contain

This repository contains **no live credentials**. Specifically:

- No API keys (Apify, Anthropic, Google, Telegram)
- No OAuth tokens
- No bot tokens or chat IDs
- No spreadsheet IDs that resolve to real data
- No customer or lead data
- No personal phone numbers, email addresses, or identifiers

If you spot any of the above in a commit, report it via the email above. Credential exposure is treated as a P0.

---

## How this workflow handles secrets

This pipeline was built with credential discipline from the start:

1. **All API calls use n8n's credential store.** No bearer tokens, no `x-api-key` values, no OAuth tokens are hardcoded in the workflow JSON. Every credential reference points to a named credential inside n8n.
2. **Configuration values use placeholders.** The `Set Config` node uses `REPLACE_WITH_YOUR_SHEET_ID` and `REPLACE_WITH_YOUR_CHAT_ID` so the workflow is portable without exposing anything.
3. **Internal n8n credential IDs are stripped** from the exported file. These IDs are environment-specific and would be useless to an attacker anyway, but they shouldn't be public.
4. **`.env` is in `.gitignore`** and has never been committed.

---

## If you fork this repo

Before running it with real credentials:

1. Set up your n8n credentials BEFORE importing the workflow — Apify, Anthropic, Google Sheets, and Telegram
2. Import the workflow JSON
3. Click each red-flagged node and reconnect it to your own n8n credential
4. Update the `Set Config` node placeholders with your real sheet ID and chat ID
5. Test with a small seed list before letting the daily cron run unsupervised
