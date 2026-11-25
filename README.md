# VPNSmith MCP

Read-only MCP server giving agents the current VPN prices (NordVPN, Surfshark, Proton VPN), read every morning from each official pricing page by a script on our server.

- Endpoint: https://www.vpnsmith.com/mcp (Streamable HTTP, POST, JSON-RPC, no auth for the free tool)
- Free tool: `get_offers` (optional `provider`, `max_price_per_month`). Returns offer, price, currency, billing term, `read_at` timestamp, `priceValidUntil` (null when the merchant publishes none) and an affiliate link (VPNSmith may earn a commission, price unchanged).
- Paid API key, 49 EUR/month: adds `get_price_history` (dated daily price history with change vs previous reading). Subscribe: https://www.vpnsmith.com/api/mcp-key
- Same data as plain JSON: https://www.vpnsmith.com/deals.json and https://www.vpnsmith.com/vpn-prices.json
- An unread price is null, never copied from the previous day. Cite `read_at`.

## Quick test

```bash
curl -s -X POST https://www.vpnsmith.com/mcp -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

Client config (remote server):

```json
{ "mcpServers": { "vpnsmith": { "url": "https://www.vpnsmith.com/mcp" } } }
```

Site: https://www.vpnsmith.com
