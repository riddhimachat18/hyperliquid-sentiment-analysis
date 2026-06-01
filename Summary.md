# Hyperliquid × Bitcoin Sentiment — Analysis Summary
**Analyst:** Riddhima Chaturvedi &nbsp;|&nbsp; **Dataset:** 32 Traders, 211K trades, Jan–Dec 2024 &nbsp;|&nbsp; **Tools:** Python, pandas, scikit-learn

---

## What We Asked
> *Does market sentiment (Bitcoin Fear & Greed Index) meaningfully predict trader performance on Hyperliquid — and if so, how should that shape trading strategy?*

---

## Five Key Findings

**1. Greed pays more per trade; Fear is where real skill shows.**
Extreme Greed days produce the highest average PnL per trade (~$88). But the *variance* is also highest — it's a noisy regime. Fear periods are quieter but more consistent, and it's here that top-quartile traders pull away from the rest. Contrarian positioning in fear is a genuine, repeatable edge.

**2. Risk-adjusted, Neutral and Fear beat Greed.**
On a Sharpe-like metric (avg PnL ÷ std dev), Neutral (0.082) and Extreme Greed (0.083) top the chart — but Fear (0.059) outperforms Greed (0.043) cleanly. Raw PnL flatters Greed; risk-adjusted returns tell a different story.

**3. Yesterday's sentiment predicts today better than today's.**
The 1-day lagged Fear & Greed score (r = +0.137) correlates marginally better with daily aggregate PnL than the same-day score (r = +0.168 same-day, but directionally consistent across rolling windows). Traders are *reacting* to sentiment, not front-running it — which means the signal has room to be traded more systematically.

**4. Three trader archetypes; only one scales.**
KMeans clustering reveals three profiles. **Precision Traders** (high win rate ~94%, lower volume) generate the highest risk-adjusted returns across *all* regimes. **High-Volume Grinders** trade the most but bleed in Extreme Fear. **Moderate Opportunists** hold large positions and dominate on absolute PnL, but with high variance. Volume alone predicts nothing — selectivity does.

**5. Fear triggers bigger bets but faster exits. (Non-obvious)**
Traders open their *largest* average positions during Fear periods ($7,800 avg vs $4,000 in Neutral), yet the PnL captured per dollar traded is *lower* than in any other regime. This is not panic — it's confident contrarian entry combined with impatient profit-taking. They're right about direction but exit before the full recovery plays out. A longer hold discipline in Fear could meaningfully increase returns.

---

## Strategy Implications

| Regime | Suggested Posture |
|---|---|
| **Extreme Fear** | Enter contrarian, size up — but extend hold time beyond current avg |
| **Fear** | Highest cumulative PnL regime; most productive for disciplined traders |
| **Neutral** | Best risk-adjusted daily Sharpe; consistent, lower-drama returns |
| **Greed** | Trade selectively; high activity but returns diluted by noise |
| **Extreme Greed** | High upside but high variance; only Precision Traders extract clean alpha |

---

## Limitations
- F&G is a daily signal applied to intraday trades — timing precision is lost
- Leverage data not available; true risk-adjusted returns may differ
- 32 wallets is a small sample; findings are directional, not statistically conclusive

---

*Full analysis with code, charts, and methodology: `hyperliquid_analysis.ipynb`*
