# DealScreen AI

**AI-powered industrial real estate deal screening and underwriting assistant.**

DealScreen AI helps investment teams review industrial real estate opportunities faster by turning offering memorandums and market inputs into structured property data, financial insights, market context, validation checks, and risk flags.

## Problem

Industrial real estate underwriting is often manual and fragmented. Analysts must review long offering memorandums, extract property and financial information, compare market data, identify missing assumptions, and assess risk before a deal can move forward.

## Solution

DealScreen AI creates an automated first-pass screening workflow that:

1. Ingests deal documents and property information.
2. Extracts key property, tenant, lease, and financial data.
3. Organizes market indicators and comparable information.
4. Evaluates investment and operating risks.
5. Validates extracted information and flags missing data.
6. Returns structured output for a human analyst to review.

## Core Workflow

```text
Deal Intake
   ↓
AI Document Review
   ↓
Market Research
   ↓
Financial Analysis
   ↓
Risk Analysis
   ↓
Validation
   ↓
Structured Deal Summary
   ↓
Human Analyst Review
```

## Key Features

- Offering Memorandum review and structured extraction
- Property and building data extraction
- Financial information screening
- Market vacancy, rent, supply, and absorption analysis
- Risk flag generation
- Missing-data and assumption validation
- Structured JSON output for downstream applications
- Human-in-the-loop review
- n8n workflow automation

## Example Property

The prototype workflow has been tested with an industrial property at **8640 Slauson Avenue, Pico Rivera, California**.

Example extracted fields include:

- Building size: 65,014 SF
- Occupancy: 0%
- Clear height: 18 ft
- Dock-high doors: 10
- Ground-level doors: 1
- Parking: 89 spaces
- Power: 1,200 amps
- Year built: 1960
- Renovated: 2024

The system is designed to mark missing financial inputs as unavailable rather than inventing values.

## Structured Output

The AI workflow is designed around four primary result groups:

```json
{
  "property": {},
  "financials": {},
  "market": {},
  "risk_flags": []
}
```

### Reliability Rules

DealScreen AI follows several important validation rules:

- Never guess missing values.
- Preserve original units when possible.
- Mark calculations as `not_calculable` when required inputs are missing.
- Explain why a value cannot be calculated.
- Surface validation warnings and unusual assumptions.
- Keep AI output reviewable by a human analyst.

## Architecture

```text
User / Analyst
     │
     ▼
Deal Intake / Upload
     │
     ▼
n8n Webhook
     │
     ▼
Document Extraction
     │
     ▼
AI Analysis Layer
 ┌──────┼────────┬────────┐
 ▼      ▼        ▼        ▼
Property Financial Market Risk
Analysis  Analysis Analysis Analysis
 └──────┬────────┴────────┘
        ▼
Validation Layer
        │
        ▼
Structured JSON
        │
        ▼
Frontend / Analyst Review
```

## Technology

- **Workflow automation:** n8n
- **AI layer:** Large language model based extraction and analysis
- **Integration:** Webhooks / APIs
- **Data format:** JSON
- **Frontend:** Analyst-facing deal screening interface
- **Architecture:** Modular AI-agent workflow with human review

## Repository Structure

```text
dealscreen-ai/
├── README.md
├── .gitignore
├── .env.example
├── docs/
│   └── ARCHITECTURE.md
├── n8n/
│   └── README.md
└── sample-data/
    └── example-output.json
```

## Security

Do not commit:

- API keys
- `.env` files
- passwords or credentials
- private webhook secrets
- confidential offering memorandums
- proprietary market data

Use `.env.example` to document required configuration without exposing secrets.

## Project Status

This repository contains the prototype architecture and workflow for an AI-powered industrial real estate fellowship / hackathon project. The system is being developed as a decision-support tool, not as a replacement for professional investment judgment.

## Future Improvements

- Automated rent and sales comparable collection
- Sensitivity analysis and scenario modeling
- Debt and financing analysis
- Investment scoring
- Interactive underwriting dashboard
- Source-level citations for every extracted field
- Export to Excel and investment committee memo formats

## Disclaimer

DealScreen AI is a prototype decision-support system. Outputs should be independently verified before being used for investment decisions.
