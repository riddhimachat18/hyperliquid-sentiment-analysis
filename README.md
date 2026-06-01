# Hyperliquid Trader Performance × Bitcoin Market Sentiment

An exploratory data analysis of 32 on-chain traders on Hyperliquid, examining how Bitcoin's Fear & Greed Index correlates with trader behaviour, PnL, and risk-adjusted performance across 2024.

> 📓 [View rendered notebook on nbviewer](https://nbviewer.org/github/riddhimachat18/hyperliquid-sentiment-analysis/blob/main/hyperliquid_analysis.ipynb)

---

## Project Structure

```
├── hyperliquid_analysis.ipynb   # Main analysis notebook (run top-to-bottom)
├── Summary.md                   # 1-page executive summary of findings
├── fear_greed_index.csv         # Bitcoin Fear & Greed Index (daily, 2018–2025)
└── historical_data.csv          # Hyperliquid trade history (32 accounts, 2024)
```

---

## Datasets

| File | Rows | Key Columns |
|---|---|---|
| `fear_greed_index.csv` | 2,644 | `date`, `value` (0–100), `classification` |
| `historical_data.csv` | 211,224 | `Account`, `Closed PnL`, `Size USD`, `Direction`, `Timestamp IST` |

**Coverage:** Jan 2024 – Dec 2024 &nbsp;|&nbsp; **Traders:** 32 unique wallets &nbsp;|&nbsp; **Merge rate:** 100%

---

## Setup

```bash
pip install pandas numpy matplotlib scikit-learn jupyter
```

Then open and run the notebook:

```bash
jupyter notebook hyperliquid_analysis.ipynb
```

The notebook is self-contained — all data loading, cleaning, and analysis is sequential. Restart kernel and run all cells top-to-bottom before reviewing outputs.

---

## Analysis Sections

| # | Section | Method |
|---|---|---|
| 0 | Setup & configuration | Constants, style, imports |
| 1 | Data loading & cleaning | Date parsing, column standardisation, sentiment merge |
| 2 | Sentiment landscape | Distribution pie + rolling F&G score over time |
| 3 | PnL by sentiment regime | Avg PnL, win rate, Sharpe-like ratio per regime |
| 4 | Lag analysis | Pearson correlation: same-day vs lag-1 F&G vs daily PnL |
| 5 | Strategy backtest | Cumulative PnL curves: "trade only in regime X" simulation |
| 6 | Trader clustering | KMeans (k=3) on trade count, win rate, avg size, Sharpe |
| 7 | Cluster × sentiment heatmap | Avg trade PnL per archetype per regime |
| 8 | Non-obvious finding | Position sizing vs PnL capture efficiency by sentiment |
| 9 | Limitations & next steps | Assumptions, data gaps, follow-on ideas |

---

## Key Findings (tl;dr)

- **Fear, not Greed, generates the most cumulative PnL** across 2024 — driven by volume of days and consistent positive daily returns
- **Precision Traders** (high win rate, low volume) outperform on risk-adjusted returns in *every* sentiment regime
- **Traders size up in Fear** but exit too quickly — leaving significant PnL on the table by not holding through recovery
- The **1-day lag** in sentiment correlation suggests a systematic, rules-based signal is buildable with more granular data

---

## Design Choices

- **Winsorisation at 1st/99th percentile** for visualisations; raw totals use unclipped values
- **Closed trades only** (non-zero PnL rows) for performance analysis — open positions and adjustments excluded
- **KMeans k=3** chosen after visual inspection of k=2..5; k=3 gives the most interpretable cluster separation
- Consistent colour palette throughout: Red = Extreme Fear → Blue = Extreme Greed

---

## What's Not Covered (Next Steps)

1. **Leverage-adjusted returns** — actual risk per trade is unknown without leverage data
2. **Intraday sentiment granularity** — daily F&G applied to sub-hour trades loses timing precision
3. **Copy-trade / correlated wallet detection** — 32 wallets on one platform warrants a correlation check
4. **Coin-level breakdown** — sentiment sensitivity likely varies significantly across BTC vs altcoin pairs
5. **Survival/drawdown analysis** — how long do losing streaks last per sentiment, and which clusters recover fastest?

---

## Notes

This was built as a submission for an AI Intern data analysis assignment. The goal was depth over breadth — fewer analyses, more clearly reasoned. The non-obvious finding in Section 8 (fear sizing vs capture efficiency) was not in the brief and emerged from exploratory inspection of the `Direction` column.
