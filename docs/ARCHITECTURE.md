# DealScreen AI Architecture

## Overview

DealScreen AI is designed as a human-in-the-loop industrial real estate screening workflow. Documents and user inputs enter through a deal intake layer, are processed by automated extraction and analysis components, and are returned as structured data for analyst review.

## Processing Flow

```text
1. Deal Intake
   - Offering Memorandum
   - Property information
   - Investment criteria
   - Analyst comments

2. Workflow Orchestration
   - Webhook receives the request
   - File/text content is normalized
   - Processing steps are coordinated in n8n

3. Document Review
   - Property attributes
   - Occupancy and tenant information
   - Lease information
   - Financial information

4. Market Analysis
   - Rent context
   - Vacancy
   - Supply / demand
   - Comparable information
   - Local market indicators

5. Financial Analysis
   - Income and expense inputs
   - Market-vs-in-place comparisons
   - Return inputs when available
   - Financing assumptions when available

6. Risk Analysis
   - Market risk
   - Tenant risk
   - Vacancy risk
   - Lease rollover risk
   - Physical / functional risk
   - Financing risk
   - Environmental / regulatory risk

7. Validation
   - Missing fields
   - Conflicting values
   - Unsupported assumptions
   - Non-calculable metrics

8. Structured Output
   - property
   - financials
   - market
   - risk_flags

9. Human Review
   - Analyst validates sources
   - Analyst accepts, edits, or rejects conclusions
```

## Design Principles

### Do not invent data
If a value is not present or cannot be calculated from available inputs, it should be clearly marked as unavailable or not calculable.

### Preserve source context
Extracted values should remain traceable to their source whenever possible.

### Separate facts from analysis
Property facts, financial inputs, market observations, and AI-generated risk conclusions should be stored separately.

### Human in the loop
DealScreen AI is a screening assistant. Final underwriting and investment decisions remain with the investment professional.

## Example API Response

```json
{
  "property": {
    "address": "8640 Slauson Avenue, Pico Rivera, CA 90660",
    "building_sf": 65014,
    "occupancy_pct": 0,
    "dock_high_doors": 10
  },
  "financials": {
    "noi": null,
    "noi_status": "not_available"
  },
  "market": {
    "status": "requires_market_data"
  },
  "risk_flags": [
    {
      "category": "occupancy",
      "severity": "high",
      "message": "Property is currently vacant."
    }
  ]
}
```

## Planned Extensions

- Source citations for every extracted field
- Market data connectors
- Comparable property analysis
- Scenario and sensitivity modeling
- Debt sizing
- Investment scoring
- Excel export
- Investment committee memo generation
