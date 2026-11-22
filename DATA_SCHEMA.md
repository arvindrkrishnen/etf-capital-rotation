# DATA SCHEMA

Recommended embedded JSON:

```json
{
  "weeks": [
    {
      "label": "Nov 9–13",
      "note": "Huge broad-equity inflows...",
      "sources": [
        {
          "name": "Semiconductors / AI",
          "tickers": ["SMH", "SOXX"],
          "amount": 6.29,
          "color": "#7c3aed"
        }
      ],
      "dest": [
        {
          "name": "Broad / Growth Equity",
          "tickers": ["QQQ", "VOO"],
          "amount": 23.10
        }
      ],
      "map": [
        ["Semiconductors / AI", "Broad / Growth Equity", 5.00],
        ["New Cash / External Funding", "Broad / Growth Equity", 13.10]
      ]
    }
  ],
  "market": [
    {
      "label": "Nov 9–13",
      "us_aum": 9.923,
      "intl_aum": 2.899,
      "us_flow": 54.2,
      "intl_flow": 10.5,
      "us_change": 98.7,
      "intl_change": 18.9,
      "us_val_effect": 44.5,
      "intl_val_effect": 8.4
    }
  ],
  "profiles": {
    "QQQ": {
      "name": "Invesco QQQ Trust",
      "desc": "Tracks the Nasdaq-100...",
      "ytd": "5.41%",
      "sharpe": "1.07",
      "holdings": [
        ["AAPL", "Apple", 8.13],
        ["NVDA", "NVIDIA", 8.02]
      ]
    }
  }
}
```

## Units

- AUM: USD trillions
- flows: USD billions
- ribbon values: USD billions
- holdings: percent
- returns: percent

## Missing numeric values

Use:

```json
null
```

Render in the UI as:

```text
—
```
