# kite-mcp-ticker

[![Go Reference](https://pkg.go.dev/badge/github.com/algo2go/kite-mcp-ticker.svg)](https://pkg.go.dev/github.com/algo2go/kite-mcp-ticker)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Websocket ticker service for the algo2go ecosystem. Provides live
tick subscription via the Kite WebSocket API, callback dispatch,
leak-sentinel goroutine cleanup, and race-flag-on/off lifecycle
testing.

Used by [`Sundeepg98/kite-mcp-server`](https://github.com/Sundeepg98/kite-mcp-server)
for live market data subscription, alert evaluation triggers,
trailing-stop monitoring, and dashboard SSE streaming.

## Why a separate module?

Live tick subscription is a foundational primitive for any algo2go
project that consumes streaming market data independent of
`kite-mcp-server`. Hosting as a module:

- Centralizes the websocket lifecycle + callback dispatch contract
- Pairs with `algo2go/kite-mcp-broker` (Kite SDK adapter)

## Stability promise

**v0.x — unstable.** Pin `v0.1.0` deliberately.

## Install

```bash
go get github.com/algo2go/kite-mcp-ticker@v0.1.0
```

## Public API

- `Service` — websocket ticker lifecycle (Start/Stop/Subscribe/Unsubscribe)
- Callback registration for tick + connect + disconnect events
- Leak-sentinel goroutine accounting for tests

## Dependencies

- `github.com/algo2go/kite-mcp-broker` v0.1.0 — broker adapter +
  ticker port + zerodha subpackage
- `github.com/algo2go/kite-mcp-money` v0.1.0 (transitive)
- `github.com/zerodha/gokiteconnect/v4` — Kite SDK
- `github.com/stretchr/testify` — assertions
- `go.uber.org/goleak` — leak detection

All algo2go deps published; no upstream `replace` directives needed.

## Reference consumer

[`Sundeepg98/kite-mcp-server`](https://github.com/Sundeepg98/kite-mcp-server)
— consumed across kc/manager_init.go, kc/broker_services.go,
kc/usecases/ticker_usecases.go, kc/ops/data.go, kc/telegram/bot.go,
mcp/alerts/alert_tools.go, mcp/misc/ticker_tools.go,
mcp/trade/trailing_tools.go.

## License

MIT — see [LICENSE](LICENSE).

## Authors

Original design: [Sundeepg98](https://github.com/Sundeepg98) (Zerodha
Tech). Multi-module promotion (2026-05-10): algo2go contributors.
