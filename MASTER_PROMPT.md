# MASTER PROMPT — ETF Capital Rotation Sankey

Act as an institutional ETF flow strategist.

Recreate the latest **6-week ETF Capital Rotation Explorer**.

## Objective

Analyze the latest six weekly ETF flow periods and generate a standalone interactive HTML dashboard using current ETF.com / FactSet data.

## 1. Time Window

Use:
- latest 5 completed weeks
- latest current/incomplete week if ETF.com daily data exists

Label incomplete periods with `*`.

Never estimate missing trading days.

## 2. Retrieve broad flow data

For every week retrieve:
- U.S. Equity flow and AUM
- International Equity flow and AUM
- U.S. Fixed Income
- International Fixed Income
- Commodities
- Alternatives
- Leveraged
- Inverse
- Currency / crypto

## 3. Retrieve named ETF creations/redemptions

For each week retrieve the most important ETF creations and redemptions.

Classify into:

- Broad U.S. Equity
- Nasdaq / Growth
- Semiconductors / AI
- Small Cap
- Value / Dividend
- Quality / Active
- Developed ex-U.S.
- Emerging Markets
- EM ex-China
- Ultra-Short Treasury
- Intermediate Treasury
- Long Treasury
- IG Corporate
- High Yield
- Municipal
- Gold
- Broad Commodities
- Energy
- Agriculture
- Alternatives

## 4. Build donor and receiver pools

Donor = ETF/sleeve with redemptions.

Receiver = ETF/sleeve with creations.

Group named ETFs by sleeve.

## 5. Model source → destination links

Use:
- timing
- comparable magnitude
- macro context
- factor rotation
- geographic rotation

Do not claim the transfer is directly traced.

Ribbon dollars are modeled.

## 6. New Cash / External Funding

For each receiving sleeve calculate:

`Residual = receiving inflows - mapped donor flows`

If positive, create:

`New Cash / External Funding → destination`

Explain that it can represent:
- cash
- new savings
- money-market assets
- mutual-fund redemptions
- futures/options repositioning
- pensions / institutional rebalancing

## 7. Market-value panel

Show:

### U.S. equity ETF market value
Use ETF.com U.S. Equity AUM.

### International equity ETF market value
Use ETF.com International Equity AUM.

Calculate:

`AUM Change = current AUM - previous AUM`

`Valuation / Other Effect = AUM Change - Net ETF Flow`

Clearly label the latter as an approximation.

Do not call these total U.S. or global equity market capitalization.

## 8. ETF Inspector

Every ticker displayed in the Sankey must be clickable.

Right-side panel must show:
- ticker
- ETF name
- description
- YTD return
- 3Y Sharpe
- beta when available
- expense ratio when available
- top 5 holdings/exposures
- holding weights

Use issuer pages first.
Use Morningstar for Sharpe/beta where needed.

For bond ETFs show bond exposures.
For commodity ETFs show commodity exposure.

Never invent missing values.

## 9. Macro theory

For each week correlate with:
- CPI/PCE
- payrolls
- unemployment
- retail sales
- Fed decisions/minutes
- Treasury yields
- USD
- gold
- crude oil

Use cautious causal language:
- consistent with
- suggests
- likely contributed
- appears to reflect

## 10. HTML requirements

Generate one standalone `.html`.

Requirements:
- Edge compatible
- no React
- no D3
- no CDN
- no external JS
- all data embedded
- SVG Sankey
- vanilla JavaScript

Layout:

### Top
Week dropdown

### Market panel
U.S. Equity ETF AUM
International Equity ETF AUM

For both:
- AUM
- AUM change
- net flow
- valuation/other effect

### Main body
Left: Sankey
Right: ETF inspector

### Source node
- sleeve
- OUT $ amount
- clickable ETF tickers

### Destination node
- sleeve
- IN $ amount
- clickable ETF tickers

### Ribbon
- modeled USD amount when space permits

## 11. Colors

- Semiconductors / AI = #7c3aed
- Broad / Growth = #2563eb
- Gold / Commodities = #d97706
- Bonds / Credit donor = #b91c1c
- Value / Defensive = #0f766e
- Innovation / Crypto = #db2777
- New Cash = #6b7280
- Destination = #16a34a

## 12. Prevent text overlap

Never put long labels in the center of the Sankey.

Use:

Left label column
→ source nodes
→ ribbons
→ destination nodes
→ right label column

Minimum:

`viewBox="0 0 1300 900"`

Use at least 24px between nodes.

If a sleeve has many ETFs, show only 1–3 representative tickers.

## Final deliverables

Return:
1. downloadable HTML
2. six-week interpretation
3. donor segments
4. receiving segments
5. external/new-cash explanation
6. macro theory
7. source citations

Before finalizing:
- verify every displayed ticker opens the ETF inspector
- verify the week selector works
- verify there is no label overlap
