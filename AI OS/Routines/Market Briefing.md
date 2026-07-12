# Market Briefing

A daily market update delivered automatically, plus an on-demand option.

## Automatic (daily, 8am)
A Windows Scheduled Task (`AngeBrain-MarketBriefing`) runs `_sources/market_briefing.py` every morning at 8am and sends a Telegram message with:
- Prices + % change for anything in [[Investing/Watchlist]] (or major indices if the watchlist is empty)
- The latest 2-3 relevant headlines

## On-demand
Ask in Claude Code any time: *"give me a market update"* or *"what's happening with [stock]"* — no need to wait for the 8am run.

## Adding a stock to the watchlist
Create a note in `Investing/Watchlist/` named exactly after its Yahoo Finance ticker, e.g.:
- `AAPL.md` (US)
- `BHP.AX.md` (ASX — note the `.AX` suffix)
- `0700.HK.md` (HKEX — note the `.HK` suffix)
- `2330.TW.md` (TWSE — note the `.TW` suffix)

Once any file exists there, the daily briefing automatically starts including it.

## Data source
Free Yahoo Finance data via the `yfinance` Python library — no API key, no cost. Covers all four markets (confirmed working for US, ASX, HKEX, TWSE). Data may lag slightly behind real-time and isn't professional/trading-terminal grade — treat it as directional, not execution-grade pricing.
