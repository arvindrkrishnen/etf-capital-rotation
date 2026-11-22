# ETF Capital Rotation Analysis Playbook

## Objective

Create a six-week ETF capital-flow analysis showing:

1. which ETF segments lost money
2. which ETF segments gained money
3. which named ETFs explain the movement
4. how much external/new funding is needed to reconcile the receiving flows
5. how the rotation correlates with the macro environment
6. how selected ETFs are positioned and performing
7. a standalone interactive HTML Sankey dashboard

# Phase 1 — Research

## Step 1 — Establish the date window

Identify today's date and the latest ETF.com report.

Use:
- latest five completed ETF flow weeks
- latest current/incomplete week if daily data exists

Never fabricate missing days.

## Step 2 — Retrieve weekly broad asset-class data

For each week capture:

```json
{
  "week": "Nov 9–13",
  "asset_class_flows": {
    "US Equity": 54.2,
    "International Equity": 10.5,
    "US Fixed Income": 0.6,
    "International Fixed Income": 2.0,
    "Commodities": 0.6,
    "Alternatives": 0.7
  },
  "aum": {
    "US Equity": 9.923,
    "International Equity": 2.899
  }
}
```

Use USD billions for flows and USD trillions for AUM.

## Step 3 — Retrieve named ETF creations/redemptions

For each period capture at least:
- top creations
- top redemptions

Example:

```json
{
  "ticker": "SOXL",
  "flow_usd_b": -4.2,
  "sleeve": "Semiconductors / AI"
}
```

# Phase 2 — Rotation Mapping

## Step 4 — Build donor pools

Group negative ETF flows by sleeve.

Example:

```text
Semiconductors / AI

SOXL -4.2
SOXX -1.2
SMH  -0.9

Total = -6.3B
```

## Step 5 — Build receiver pools

Group positive ETF flows by sleeve.

Example:

```text
Broad / Growth Equity

QQQ +13.4
VOO +9.7

Total = +23.1B
```

## Step 6 — Model source → destination links

Use:
- timing
- comparable magnitude
- factor/geographic similarity
- macro context
- observed creation/redemption patterns

Examples:

```text
Semiconductors → Broad Equity
QQQ / Technology → International
High Yield → Investment Grade
Gold → Broad Equity
Cash → International Equity
```

Do not claim direct traceability.

## Step 7 — Add New Cash / External Funding

For each receiving sleeve:

```text
Residual =
Receiver amount
- Sum of modeled donor links
```

If positive:

```text
New Cash / External Funding → Receiver
```

# Phase 3 — ETF Market Value

For U.S. Equity and International Equity:

```text
AUM Change =
Current AUM - Previous AUM

Valuation / Other Effect =
AUM Change - Net ETF Flow
```

Show:
- AUM
- AUM change
- net flow
- valuation / other effect

Do not call ETF AUM total stock-market capitalization.

# Phase 4 — ETF Inspector

For each representative ETF retrieve:
- issuer
- ETF name
- description
- expense ratio
- YTD return
- 3Y beta
- 3Y Sharpe
- top 5 holdings/exposures
- holding weights
- latest price
- weekly price change
- weekly volume change when available

If unavailable, show `—`.

# Phase 5 — Macro Correlation

For each period retrieve:
- CPI / PCE
- payrolls
- unemployment
- retail sales
- Fed decision / minutes
- 2Y Treasury
- 10Y Treasury
- USD
- crude oil
- gold

Construct a theory using cautious wording.

Preferred:
- consistent with
- likely contributed
- suggests
- appears to reflect

Avoid:
- proved
- caused
- definitively

Example:

```text
Sticky inflation
→ higher yields
→ pressure on long-duration growth
→ semiconductor redemptions
→ capital broadens toward value / international / quality
```

# Phase 6 — HTML Generation

Embed all data:

```javascript
const DATA = {
  weeks: [...],
  market: [...],
  profiles: {...}
};
```

Do not fetch data from the browser.

Required UI:

### Week selector
Updates:
- Sankey
- AUM panel
- source/destination nodes

### ETF ticker click
Updates the right-side inspector.

### Ribbon click
Highlights the modeled flow.

# Phase 7 — Interpretation

Return:

### Six-week rotation summary
Example:

```text
Concentrated technology
→ broad U.S. equity
→ international diversification
→ value / active equity
```

### Bond-quality rotation
Example:

```text
High yield / intermediate corporate
→ IG credit / Treasuries
```

### Macro theory
Example:

```text
Sticky inflation and high yields reduced appetite for expensive
duration-sensitive growth while resilient economic growth kept
investors from abandoning equities.
```

# Guardrails

Do not:
- treat ETF flows as a closed system
- imply one ETF redemption literally funded another ETF purchase
- invent full-universe sleeve totals
- estimate missing trading days
- confuse ETF AUM with total stock-market capitalization
- use stale risk metrics without displaying dates
