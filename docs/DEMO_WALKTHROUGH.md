# Demo Walkthrough

This walkthrough explains how to present DealScreen AI in a short hackathon or portfolio demo.

## 1. Start With the Problem

Industrial Offering Memorandums contain property, financial, and market information across many pages. A first-pass analyst still needs to determine what is factual, what is missing, what is market context, and what creates material investment risk.

DealScreen AI automates that first screening pass.

## 2. Upload / Analyze an OM

The user starts a new analysis from the Lovable frontend. The document is sent to the n8n workflow through the deal-screening webhook.

## 3. Extract the Document

n8n extracts text from the uploaded PDF and passes the source content to the industrial underwriting AI agent.

## 4. Review Property Fundamentals

For the prototype property, the system extracts physical characteristics such as:

- 65,014 SF building size
- 0% occupancy
- 18 ft clear height
- 10 dock-high doors
- 1 ground-level door
- 89 parking spaces
- 1,200 amps of power
- 1960 year built
- 2024 renovation year

These values are presented as subject-property facts rather than mixed with market statistics.

## 5. Show Financial Discipline

The Financial Underwriting section clearly identifies when core financial fields are unavailable.

Instead of estimating missing figures, the workflow leaves them unavailable. This prevents a market rent, comparable price/SF, or other external statistic from being silently substituted for a subject-property financial value.

## 6. Show Market Intelligence

The prototype separates broader Central Los Angeles market statistics from Pico Rivera submarket statistics.

This is important because market vacancy, market rent, and availability are context for underwriting - they are not the same as subject-property occupancy or subject rent.

## 7. Show the Five Risk Checks

DealScreen AI explicitly evaluates:

1. Rent PSF vs Market
2. Cap Rate
3. Clear Height
4. Vacancy
5. Price/SF vs Comparable Market Data

When a category cannot be evaluated, the system returns `not_evaluable` and identifies the missing information.

## 8. Explain the Validation Layer

After the AI completes its analysis, a deterministic JavaScript node independently validates key parts of the output.

This is the core technical differentiator:

> The project does not rely solely on an LLM. The AI extracts and reasons over the Offering Memorandum, while deterministic workflow logic validates critical outputs before they reach the investment dashboard.

The deterministic layer checks required risk categories, financial completeness, vacancy calculations, price/SF and cap-rate calculability, risk consistency, and recommendation validity.

## 9. End With the Recommendation

For the prototype case, the result is `INSUFFICIENT_DATA` because the OM lacks enough verified financial information for reliable valuation.

That result demonstrates the intended behavior of the system: it is willing to stop and ask for more information rather than manufacture a confident answer.

## 60-Second Demo Script

> DealScreen AI is an AI-assisted industrial real estate screening platform. An analyst uploads an Offering Memorandum, and our n8n workflow extracts the PDF, sends the document to a specialized underwriting agent, forces the response into a structured schema, and then runs deterministic JavaScript validation before returning anything to the dashboard. The system extracts property fundamentals, separates market and submarket data, evaluates five required risk categories, detects missing information, and produces an investment recommendation. The key design choice is that the model is not allowed to invent missing financial values. In this example the property has strong physical attributes, but the OM does not include enough verified pricing and income information, so the engine returns INSUFFICIENT_DATA rather than pretending it can complete the underwriting.

## Links

- Live demo: https://industrial-dealscreen.lovable.app
- n8n architecture: [`N8N_WORKFLOW_ARCHITECTURE.md`](./N8N_WORKFLOW_ARCHITECTURE.md)
- Decision engine: [`DECISION_ENGINE.md`](./DECISION_ENGINE.md)
- Public workflow: [`../n8n/industrial-deal-screening-workflow.json`](../n8n/industrial-deal-screening-workflow.json)
