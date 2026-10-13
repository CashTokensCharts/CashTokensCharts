# CashTokens Charts — starter prototype

A responsive browser/PWA prototype for exploring CauldronSwap historical candles.

## Run locally

Serve this folder over HTTP rather than opening `CashTokensCharts.html` directly. With Python installed, run:

```sh
python -m http.server 8080
```

Then open `http://localhost:8080/CashTokensCharts.html`.

## Included

- Search by token name, ticker, or 64-character category ID.
- Results display category IDs to distinguish duplicate names/tickers.
- Candlestick chart with zoom, pan, and touch pinch controls.
- 1m, 5m, 15m, 1h, 4h, daily, weekly, and approximate 30-day intervals.
- Date-range controls and no-trade interval handling.
- PWA manifest and basic service worker shell cache.

## Known limitations

1. Cauldron token search and candlestick endpoints are documented as unstable; schema changes must be handled.
2. Browser CORS behavior is not verified. If direct requests fail, a small backend proxy is required.
3. `/token/<id>/first_pool` reports the first Cauldron pool, not the CashToken's on-chain creation date. It is shown only as pool metadata and does not limit the requested historical range. A compact info button explains this distinction in the UI. The earliest returned candle is labelled as the first available candle in the selected range, not as the token's creation or first-ever trade.
4. Date selection cannot begin before May 15, 2023.
5. Candles are BCH-denominated; price units and token decimal normalization need validation before production.
6. Reliable on-chain token-genesis timestamp lookup, persistent historical database, incremental refresh, chunked long-range queries, and reliable price-unit validation remain future work. Volume and several technical indicators are implemented in prototype form but require live API validation.
7. The API omits intervals without trades; no synthetic zero-price candles are generated. The UI explains this through a compact information popover rather than a large warning block.
8. Lightweight Charts is loaded from a CDN. Pin or self-host it for production and review Apache 2.0 license requirements.

## Next milestones

- Verify CORS, rate limits, response size and historical limits from a real browser.
- Establish on-chain token creation timestamps and keep them separate from first pool/first trade dates.
- Add persistent caching and incremental candle refresh.
- Add BCH/USD conversion with explicit source and unit labels.
- Add volume, SMA/EMA, RSI, MACD, Bollinger Bands, saved settings, and multi-token comparison.
- Add tests for schema changes, duplicate timestamps, empty history, and tiny token prices.
