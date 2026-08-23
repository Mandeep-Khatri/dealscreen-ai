# n8n Workflow

This folder is for the DealScreen AI n8n workflow export.

## Intended Flow

```text
Webhook
  ↓
Receive Deal / Document Input
  ↓
Extract and Normalize Content
  ↓
AI Deal Analysis
  ↓
Validate Structured Output
  ↓
Respond to Webhook
```

## Before Committing a Workflow Export

Remove or replace all sensitive values, including:

- API keys
- credentials
- webhook authentication secrets
- private URLs or tokens
- proprietary document contents

Commit a sanitized workflow export as something like:

`industrial-deal-screening-workflow.json`

## Expected AI Output

```json
{
  "property": {},
  "financials": {},
  "market": {},
  "risk_flags": []
}
```
