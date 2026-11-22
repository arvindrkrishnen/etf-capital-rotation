# ChatGPT ETF Capital Rotation Playbook

This repository explains how to recreate the **6-week ETF Capital Rotation Explorer** in ChatGPT.
<img width="952" height="825" alt="image" src="https://github.com/user-attachments/assets/9ae20087-2495-451a-b49b-89112632f81e" />

The final output is a standalone Microsoft Edge-compatible HTML dashboard with:

- week-by-week filtering
- source → destination ETF rotation
- USD outflow and inflow labels
- explicit **New Cash / External Funding**
- U.S. equity ETF AUM and International equity ETF AUM
- weekly AUM increase/decrease
- net ETF fund flows
- approximate valuation / market-price effect
- clickable ETF ticker symbols
- a right-side ETF inspector with:
  - ETF description
  - top holdings / exposures
  - YTD return
  - Sharpe ratio
  - beta / expense ratio when available

## Files in this repository

- `README.md` — how to run the workflow
- `PLAYBOOK.md` — detailed research and modeling methodology
- `MASTER_PROMPT.md` — reusable prompt to paste into ChatGPT
- `DATA_SCHEMA.md` — recommended embedded JSON structure
- `CHECKLIST.md` — QA checklist before publishing

## Quick start

1. Open ChatGPT.
2. Paste the contents of `MASTER_PROMPT.md`.
3. Ask:

```text
Run the ETF Capital Rotation Playbook as of today.
Generate the latest 6-week interactive Sankey HTML.
```

ChatGPT should browse current ETF.com / FactSet data, retrieve ETF profiles and holdings, calculate rotation and residual external funding, and generate a downloadable standalone HTML file.

## Primary data sources

Use this priority order:

### Fund flows
1. ETF.com weekly ETF flows
2. ETF.com daily ETF flows for an incomplete current week
3. ETF.com monthly summaries
4. FactSet data quoted by ETF.com

### ETF metadata
Prefer issuer pages:

- Vanguard
- iShares / BlackRock
- State Street / SPDR
- Invesco
- VanEck
- Capital Group
- ARK

### Risk metrics
Prefer:
- Morningstar
- issuer risk pages

Always label the period, e.g. `3Y Sharpe` or `YTD through Nov. 20, 2026`.

## Six-week window rule

Always use the latest six weekly periods.

For completed weeks, use ETF.com weekly data.

For the current incomplete week:
- aggregate available ETF.com daily flow reports
- add `*` to the period label
- never estimate missing trading days

## Stable ETF sleeves

### U.S. equity
- Broad U.S. Equity
- Nasdaq / Growth
- Semiconductors / AI
- Small Cap
- Mid Cap
- Value / Dividend
- Quality / Active Equity

### International
- Developed ex-U.S.
- Broad Emerging Markets
- Emerging Markets ex-China
- China
- India
- Japan
- Europe
- Brazil / Latin America

### Bonds
- Ultra-Short Treasury
- Intermediate Treasury
- Long Treasury
- Aggregate Bond
- Investment-Grade Corporate
- High Yield
- Municipal

### Commodities
- Gold
- Broad Commodities
- Energy
- Agriculture
- Industrial Metals

### Alternatives
- Managed Futures
- Covered Call
- Hedged Equity
- Buffer / Defined Outcome
- Long/Short

## Donors and receivers

A **donor** is a sleeve with observed ETF redemptions.

Example:

```text
Semiconductors / AI
SOXL -$4.2B
SOXX -$1.2B
SMH  -$0.9B
Total donor amount = $6.3B
```

A **receiver** is a sleeve with observed ETF creations.

Example:

```text
Broad / Growth Equity
QQQ +$13.4B
VOO +$9.7B
Total receiver amount = $23.1B
```

## New Cash / External Funding

ETF flows are not a closed zero-sum system.

If destination creations exceed mapped donor redemptions, create:

```text
New Cash / External Funding
```

Calculate:

```text
External Funding =
Destination Inflows
- Mapped Identifiable Donor Outflows
```

This residual can include:
- new savings
- money-market balances
- cash
- mutual-fund redemptions
- futures/options repositioning
- pension or institutional rebalancing

Never claim this residual is literally cash unless a source proves it.

## Sankey methodology

A ribbon means:

> observed donor outflow and destination inflow occurred in the same period and are economically consistent with a plausible rotation.

It does **not** mean ETF.com traced the actual seller's dollars to the buyer.

Ribbon amount must not exceed:

```text
min(remaining donor outflow, remaining receiver inflow)
```

## Market-value / AUM panel

Use ETF.com asset-class AUM, not total public-equity market capitalization.

Show:
- U.S. Equity ETF AUM
- International Equity ETF AUM

Calculate:

```text
AUM Change = Current AUM - Prior AUM

Valuation / Other Effect =
AUM Change - Net ETF Flow
```

Use this wording:

> “Valuation / Other Effect is a residual approximation and can include market-price changes, distributions, classification changes, and other AUM effects.”

## ETF inspector requirements

Every displayed ticker should be clickable.

Show:
- ticker
- ETF name
- description
- YTD return
- 3Y Sharpe
- beta when available
- expense ratio when available
- top 5 holdings/exposures
- holding weights

For bond ETFs show bond exposures.
For commodity ETFs show commodity exposure.

Never invent unavailable values. Render missing data as `—`.

## Color standard

```text
Semiconductors / AI = #7c3aed
Broad / Growth      = #2563eb
Gold / Commodities  = #d97706
Bonds / Credit      = #b91c1c
Value / Defensive   = #0f766e
Innovation / Crypto = #db2777
New Cash            = #6b7280
Destination         = #16a34a
```

## HTML compatibility

For Microsoft Edge compatibility:

- plain HTML
- plain CSS
- vanilla JavaScript
- no React
- no D3
- no CDN
- no external JavaScript libraries
- embed all data directly into the file
- use SVG for Sankey ribbons
- keep the ETF inspector outside the SVG

## Avoiding text overlap

Do not place long labels in ribbons.

Use:

```text
LEFT LABEL COLUMN
[sleeve]
[OUT $X.XXB]
[TICKER]
[TICKER]

   Sankey ribbons

RIGHT LABEL COLUMN
[sleeve]
[IN $X.XXB]
[TICKER]
[TICKER]
```

Recommended minimum SVG:

```text
viewBox="0 0 1300 900"
```

Use:
- at least 24px between nodes
- minimum visible node height around 18px
- only 1–3 representative tickers when a sleeve contains many ETFs

## Final ChatGPT deliverables

Return:

1. downloadable HTML file
2. concise six-week interpretation
3. donor segments
4. receiving segments
5. new/external cash explanation
6. macro theory
7. source citations

Before finalizing, verify every displayed ETF ticker works in the inspector.
