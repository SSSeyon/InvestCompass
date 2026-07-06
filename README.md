# Invest Compass

Personal portfolio tracker + market-signal assistant. Single-file PWA (like Tracker / MomentumScout) — no build step, no backend, all data in localStorage.

## Markets & data sources (all free)
| Market | Source | Key needed? |
|---|---|---|
| NGX (Nigeria) | Official NGX feed (`doclib.ngxgroup.com`) — full daily price list, CORS-open | No |
| US & global | [Twelve Data](https://twelvedata.com/pricing) quotes + daily history | Free key (~800 req/day, 8/min) |
| FX (USD/NGN etc.) | open.er-api.com | No |

## Setup
1. Serve the folder over HTTP (any static server; `.claude/serve.ps1` runs one on `http://localhost:8644`).
2. Open Settings → paste a free Twelve Data API key (only needed for US/global symbols).
3. Turn off **Demo mode**.
4. Add your holdings (Portfolio tab) and tickers you're considering (Watchlist tab).
5. Set your target allocation (%) in Settings — this drives the rebalancing recommendations.

## How recommendations work (transparent, mechanical rules)
- **Rebalance** — actual vs target allocation drift > 5pt, with an amount to shift.
- **Concentration** — any single position > 25% of portfolio.
- **Cash** — cash > target + 15pt (inflation drag / DCA suggestion).
- **Signals** — per ticker, a score from: 50/200-day moving-average trend (±25), price vs 50-day (±10), RSI overbought/oversold (±15), 3-month momentum (±15), 52-week high/low proximity (±5). Score ≥ +30 = Bullish, ≤ −30 = Bearish. Every signal lists its reasons.
- **NGX breadth** — advancers vs decliners context on broad rally/selloff days.

### NGX history note
The NGX feed only provides the current day's prices, so the app records each day's closes in localStorage. Technical signals for NGX names activate automatically once ~30 trading days have been collected (US/global names get 260 days of history immediately from Twelve Data). Export a backup (Settings → Export JSON) to preserve collected history.

## Not financial advice
Signals are mechanical rules on historical prices. They know nothing about earnings, news, or your circumstances. Always verify before investing.
