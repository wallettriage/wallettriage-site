# WalletTriage — website

Source of [wallettriage.com](https://wallettriage.com), the public site for
**WalletTriage**: a real-time wallet risk engine for AI agents.

## What is WalletTriage?

WalletTriage answers one question before an agent acts on-chain:
**"is this address dangerous right now?"** It cross-references active ERC20
approvals with a live threat feed of contracts under attack and returns a
`risk_score` (0–100), a `risk_level` and actionable findings.

Built for the agent economy:

- **Paid per query via [x402](https://x402.org)** — USDC on Base, settled at
  request time. No signup, no API key, no subscription.
- **MCP server** — agents call `check_address_risk` as a native tool and pay
  autonomously with a session key. `get_pricing` is free.
- **Stateless & watch-only** — nothing about you or your query is persisted,
  and the service can never hold or move funds.
- **Honest by design** — risk signals are probabilistic. It never says "safe";
  a low score always comes with the evidence that was checked.

## API

- Spec: [`openapi.yaml`](./openapi.yaml) (OpenAPI 3.1), also served at
  `https://api.wallettriage.com/openapi.yaml`
- Free status/pricing endpoint: `GET https://api.wallettriage.com/health`
- Paid risk check: `GET https://api.wallettriage.com/scan?address=0x…&chain=eth`
  (returns HTTP 402 with x402 payment requirements; any x402 client handles
  payment and retry automatically)

## About this site

A single static file (`index.html`) — no framework, no build step, no
tracking. The "paste an address" demo replays pre-recorded API responses so
humans can inspect the exact schema agents receive.

Local preview:

```bash
python -m http.server 8080   # or any static server
# open http://localhost:8080
```

Deployed via GitHub Pages (`CNAME` → wallettriage.com).
