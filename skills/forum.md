---
name: Forum
description: Use when building trading bots, market data integrations, or order management systems for perpetual futures on attention indices. Reach for this skill when you need to authenticate API requests, place/cancel orders, stream real-time market data via WebSocket, or query account and position information.
metadata:
    mintlify-proj: forum
    version: "1.0"
---

# Forum API Skill

## Product Summary

Forum is a perpetual futures exchange offering contracts on attention indices. The API provides REST endpoints for order management, account queries, and market data, plus a WebSocket feed for real-time streaming. Base URLs: REST `https://api.forum.market/v1`, WebSocket `wss://api.forum.market/ws/v1`. All requests use JSON. Authentication uses HMAC-SHA256 signatures with three headers: `FORUM-ACCESS-KEY`, `FORUM-ACCESS-TIMESTAMP`, and `FORUM-ACCESS-SIGN`. API keys are created in the web app (app.forum.market) with `read` or `trade` permissions. See the [API Reference](https://docs.forum.market/api-reference/introduction) for complete endpoint documentation.

## When to Use

Reach for this skill when:
- Building automated trading systems or bots that place, cancel, or monitor orders
- Streaming real-time market data (order books, tickers, trades, funding rates) into dashboards or algorithms
- Querying account balances, positions, fills, or order history programmatically
- Integrating Forum's perpetual futures into a larger trading platform
- Implementing market-making or algorithmic trading strategies
- Monitoring margin levels and liquidation risk across a portfolio

Do not use this skill for: UI/UX work, account creation (use the web app), or non-trading operations.

## Quick Reference

### API Endpoints by Category

| Category | Key Endpoints | Auth Required |
|----------|---------------|---------------|
| **Market Data** | `GET /v1/markets`, `GET /v1/markets/{ticker}`, `GET /v1/order-book/{ticker}`, `GET /v1/trades/{ticker}` | No |
| **Orders** | `POST /v1/orders`, `DELETE /v1/orders/{id}`, `GET /v1/orders`, `POST /v1/orders/batch`, `DELETE /v1/orders/batch` | Yes (trade) |
| **Account** | `GET /v1/account`, `GET /v1/fills`, `GET /v1/positions` | Yes (read) |
| **Index Data** | `GET /v1/indices/{ticker}`, `GET /v1/indices/{ticker}/history` | No |
| **Candles** | `GET /v1/candles/{ticker}` (1m, 5m, 1d intervals) | No |

### Order Placement Parameters

```json
{
  "ticker": "OPENAI",           // Required: market ticker
  "side": "buy",                // Required: "buy" or "sell"
  "qty": 1,                     // Required: number of contracts
  "price": 10000,               // Required for limit orders
  "orderType": "limit",         // "limit" or "market"
  "timeInForce": "goodTillCancel",  // "goodTillCancel", "immediateOrCancel", "fillOrKill"
  "clientOrderId": "my-order-1", // Optional: your own order ID
  "reduceOnly": false           // Optional: only reduce position
}
```

### API Key Permissions

| Permission | Allows |
|-----------|--------|
| `read` | View balances, positions, orders, market data |
| `trade` | Place and cancel orders (includes read access) |

### WebSocket Channels

**Public (no auth needed):**
- `bookUpdates` — order book snapshots + incremental updates
- `tickerUpdates` — last price, bid/ask, volume
- `trades` — executed trades
- `indexUpdates` — attention index changes
- `fundingEvents` — funding rate events
- `candleUpdates1m`, `candleUpdates5m`, `candleUpdates1d` — OHLCV data
- `heartbeat` — 1-second heartbeat per ticker

**Private (auth required):**
- `userOrders` — order lifecycle updates
- `userFills` — trade executions
- `userPositions` — position changes
- `userAccount` — margin and PnL updates

### Rate Limits

| Tier | Limit | Window | Scope |
|------|-------|--------|-------|
| Public endpoints | 120 req/min | 60s | Per IP |
| Private read | 300 req/min | 60s | Per user |
| Order operations | 500 ops/min | 60s | Per user |
| WebSocket inbound | 10 msg/sec | 1s | Per connection |

Responses include `X-RateLimit-Remaining` and `X-RateLimit-Reset` headers. On 429, use the `Retry-After` header.

## Decision Guidance

### When to Use REST vs WebSocket

| Use Case | REST | WebSocket |
|----------|------|-----------|
| One-time market data fetch | ✓ | — |
| Streaming real-time prices | — | ✓ |
| Placing a single order | ✓ | — |
| Monitoring order fills in real-time | — | ✓ |
| Querying account balance | ✓ | — |
| Tracking margin changes live | — | ✓ |
| Batch operations (10+ orders) | ✓ | — |

### When to Use Order Types

| Scenario | Type | Time-in-Force |
|----------|------|---------------|
| Execute immediately at market | `market` | N/A |
| Resting limit order, cancel manually | `limit` | `goodTillCancel` |
| Limit order, cancel if not filled in 1 second | `limit` | `fillOrKill` |
| Limit order, cancel if not filled immediately | `limit` | `immediateOrCancel` |
| Close position only, no new exposure | Any | N/A (use `reduceOnly: true`) |

## Workflow

### 1. Set Up Authentication

1. Log in to app.forum.market
2. Navigate to Settings > API Keys
3. Click Create API Key
4. Choose permission level: `read` for queries only, `trade` for order placement
5. Save the key ID (`fk_...`) and secret (`sk_...`) securely — the secret is shown only once
6. Store credentials in environment variables, never in code

### 2. Build a Signature Function

Create a reusable function that takes method, path, and body, then returns the three required headers:

```python
def sign_request(method: str, path: str, body: str = "") -> dict:
    timestamp = str(int(time.time()))
    prehash = timestamp + method + path + body
    signature = base64.b64encode(
        hmac.new(api_secret.encode(), prehash.encode(), hashlib.sha256).digest()
    ).decode()
    return {
        "FORUM-ACCESS-KEY": api_key,
        "FORUM-ACCESS-TIMESTAMP": timestamp,
        "FORUM-ACCESS-SIGN": signature,
    }
```

### 3. Fetch Market Data (No Auth)

```python
# List all markets
resp = requests.get("https://api.forum.market/v1/markets")
markets = resp.json()

# Get specific market
resp = requests.get("https://api.forum.market/v1/markets/OPENAI")
market = resp.json()
print(f"Last price: {market['lastPrice']}")
```

### 4. Make Authenticated Requests

```python
# Get account info
headers = sign_request("GET", "/v1/account")
resp = requests.get("https://api.forum.market/v1/account", headers=headers)
account = resp.json()
print(f"Balance: {account['balance']}")
```

### 5. Place an Order

```python
order = {
    "ticker": "OPENAI",
    "side": "buy",
    "qty": 1,
    "price": 10000,
    "orderType": "limit",
    "timeInForce": "goodTillCancel",
}
body = json.dumps(order)
headers = {
    **sign_request("POST", "/v1/orders", body),
    "Content-Type": "application/json",
}
resp = requests.post("https://api.forum.market/v1/orders", data=body, headers=headers)
result = resp.json()
print(f"Order ID: {result['orderId']}")
```

### 6. Cancel an Order

```python
order_id = "your_order_id"
headers = sign_request("DELETE", f"/v1/orders/{order_id}")
resp = requests.delete(f"https://api.forum.market/v1/orders/{order_id}", headers=headers)
print(f"Cancelled: {resp.status_code}")
```

### 7. Stream Real-Time Data via WebSocket

```python
import asyncio, json, websockets

async def stream_market_data():
    async with websockets.connect("wss://api.forum.market/ws/v1") as ws:
        # Subscribe to public channels
        await ws.send(json.dumps({
            "id": 1,
            "cmd": "subscribe",
            "params": {
                "channels": ["tickerUpdates", "bookUpdates"],
                "tickers": ["OPENAI"],
            },
        }))
        
        async for message in ws:
            data = json.loads(message)
            if data.get("type") == "tickerUpdate":
                print(f"Price: {data['data']['lastPrice']}")

asyncio.run(stream_market_data())
```

### 8. Verify Work Before Submitting

- Check that all required order fields are present and valid
- Verify API key has correct permission level (`trade` for orders, `read` for queries)
- Confirm timestamp is within 30 seconds of server time
- Test with small order quantities first
- Monitor rate limit headers to avoid hitting limits
- Verify WebSocket subscriptions are active before relying on data

## Common Gotchas

- **Timestamp out of sync**: Server rejects requests where timestamp differs by >30 seconds. Call `GET /v1/time` to check server time and measure clock skew.
- **Signature construction**: Concatenate timestamp + method + path + body with no delimiters. For GET/DELETE, body is an empty string. For POST, body must be the raw JSON string, not a Python dict.
- **Query strings in path**: Do not include query parameters in the path when signing. Sign `/v1/orders`, not `/v1/orders?ticker=OPENAI`.
- **Content-Type header**: POST requests must include `Content-Type: application/json` in addition to the three auth headers.
- **API key permissions**: A `read`-only key cannot place orders — returns 403 `INSUFFICIENT_PERMISSIONS`. Create a `trade` key for order operations.
- **Order not found**: Cancelled or filled orders cannot be queried. Check `GET /v1/orders` for open orders only.
- **Insufficient margin**: Orders fail with 409 `INSUFFICIENT_MARGIN` if account balance is too low. Check account balance before placing orders.
- **Reduce-only mode**: If available funds drop below $0, account enters reduce-only mode. Only orders that reduce exposure are allowed.
- **WebSocket subscribe timeout**: Must send a subscribe command within 10 seconds of connecting, or connection closes with code 4001.
- **WebSocket message rate**: Exceeding 10 messages/second per connection closes it with code 4029. Batch subscriptions where possible.
- **Batch operation limits**: Batch create supports up to 10 orders; batch cancel supports up to 20 order IDs. Each item counts toward the 500 ops/min limit.
- **Price band violations**: Limit prices too far from current market price are rejected with 400 `PRICE_BAND_VIOLATION`.
- **Duplicate client order IDs**: If you provide a `clientOrderId`, it must be unique. Reusing one returns 400 `DUPLICATE_CLIENT_ORDER_ID`.

## Verification Checklist

Before submitting code or trading:

- [ ] API key is stored securely (environment variable, not hardcoded)
- [ ] Signature function correctly concatenates timestamp + method + path + body with no delimiters
- [ ] Timestamp is obtained fresh for each request (not cached)
- [ ] POST requests include `Content-Type: application/json` header
- [ ] Order parameters are valid: `side` is "buy" or "sell", `qty` is positive, `price` is positive for limit orders
- [ ] API key has correct permission level for the operation (`trade` for orders, `read` for queries)
- [ ] Rate limit headers are monitored; code backs off on 429 responses
- [ ] WebSocket subscriptions are sent within 10 seconds of connection
- [ ] Error responses are handled: check `error.code` field, not just HTTP status
- [ ] Timestamp validation: call `GET /v1/time` if requests fail with 401 `TIMESTAMP_EXPIRED`
- [ ] Test with small order quantities before scaling up

## Resources

- **Full API Navigation**: [docs.forum.market/llms.txt](https://docs.forum.market/llms.txt) — comprehensive page-by-page reference for all endpoints and channels
- **Quick Start Guide**: [api-reference/quick-start](https://docs.forum.market/api-reference/quick-start) — step-by-step walkthrough of authentication and first order
- **Authentication Reference**: [api-reference/authentication](https://docs.forum.market/api-reference/authentication) — complete HMAC signing specification with code examples
- **WebSocket Connection**: [api-reference/websocket/connection](https://docs.forum.market/api-reference/websocket/connection) — real-time data streaming, channels, and reconnection best practices

---

> For additional documentation and navigation, see: https://docs.forum.market/llms.txt