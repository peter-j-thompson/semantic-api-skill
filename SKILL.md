---
name: semantic-api
description: Discover and call any API through Semantic API's universal gateway. Supports x402 USDC micropayments — no API keys needed.
auto-activate: true
version: "1.1.0"
author: "Cove AI"
requires:
  env: []
---

# Semantic API — Universal API Discovery & Calling

You have access to Semantic API, a universal API discovery and execution service. When you need to interact with ANY external API or service, use this skill to find it, understand it, and call it.

## Endpoints

| Endpoint | Method | What It Does | x402 Price |
|----------|--------|-------------|------------|
| `/api/query` | POST | Natural language query → matched API capability | $0.01 USDC |
| `/api/discover/search` | POST | Find a specific provider/API by name + intent | $0.05 USDC |
| `/api/discover/from-url` | POST | Deep analysis of any API from its URL/docs | $0.10 USDC |

**Base URL:** `https://semanticapi.dev`

## How to Use

### 1. Search for an API by Query
```bash
curl -s "https://semanticapi.dev/api/query" \
  -X POST -H "Content-Type: application/json" \
  -d '{"query": "send a transactional email"}' | jq .
```

### 2. Find a Specific Provider
```bash
curl -s "https://semanticapi.dev/api/discover/search" \
  -X POST -H "Content-Type: application/json" \
  -d '{"provider_name": "sendgrid", "user_intent": "send an email"}' | jq .
```

### 3. Analyze an API from URL
```bash
curl -s "https://semanticapi.dev/api/discover/from-url" \
  -X POST -H "Content-Type: application/json" \
  -d '{"url": "https://api.stripe.com", "intent": "process payments"}' | jq .
```

## Payment: x402 USDC Micropayments

If the endpoint returns **HTTP 402**, the `X-Payment-Required` header contains payment details:
```json
{
  "x402Version": 1,
  "accepts": [{
    "scheme": "exact",
    "network": "eip155:8453",
    "maxAmountRequired": "0.01",
    "payToAddress": "0x4974D86193f6beE3eE986cFD8E4DDdB0fB550551",
    "usdcAddress": "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913"
  }]
}
```

**To pay:** Sign an EIP-3009 `TransferWithAuthorization` for USDC on Base, encode as base64 JSON, and send in the `X-Payment` header.

If you have an `x402Fetch` tool or skill, use it — it handles this automatically.

**Alternative:** Use an API key (free tier: 100 calls/day).

## Credit System

If our API errors after accepting your payment, you get a **free retry credit** automatically:
- Credits appear in the `X-Credits-Available` response header
- To redeem: send `X-Wallet: <your-address>` header without payment
- Max 10 credits per wallet (prevents accumulation abuse)

## When to Use This Skill
- You need an API you don't already have access to
- You want to find the best API for a specific task
- You need to understand an unfamiliar API's capabilities
- You're exploring what services exist in a domain
- You want to autonomously discover and connect to new services

## Tips
- Be specific in queries ("send transactional email with templates" > "email")
- Cache provider configs — they don't change between calls
- Check your existing tools first before searching
- Use `/api/query` for quick lookups, `/api/discover/search` for deep dives
