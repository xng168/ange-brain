# Investing Pillar Launched

- **Built the Investing knowledge pillar** with four sections: Education (fundamentals, ratios, risk management), Markets (ASX, TWSE, HKEX + US reference), Watchlist (ready for user inputs), and Journal (decision tracking)
- **Implemented daily 8am Telegram briefing** pulling live market data (prices + news) from Yahoo Finance via `yfinance`; tested end-to-end including scheduled task execution across all four markets
- **Configured watchlist auto-detection**: briefing picks up any ticker note created in `Investing/Watchlist/` (e.g. `BHP.AX.md`) and includes it in daily runs
- **Validated data source coverage**: free Yahoo Finance works reliably across ASX, TWSE, HKEX, and US markets (Taiwan data often hard to get free; this works)
- **Set scope: research & education only** — no brokerage integration or trade execution; on-demand lookups available anytime
- **Next:** user adds stock tickers to the watchlist folder to start receiving daily briefings
