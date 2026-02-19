# Semantic API Skill for Conway Automatons

**Give your automaton the ability to discover and call any API autonomously.**

Semantic API is a universal API discovery service with 160+ indexed providers and 770+ capabilities. This skill lets any Conway automaton search for APIs by natural language, understand their capabilities, and connect to them — all paid via x402 USDC micropayments on Base.

## Install

```bash
# Via Conway CLI
install_skill(source: "git", url: "https://github.com/peter-j-thompson/semantic-api-skill")

# Or manually
cp SKILL.md ~/.automaton/skills/semantic-api/SKILL.md
```

## What Your Automaton Can Do

- **"Find me a weather API"** → Returns provider config, endpoints, auth requirements
- **"I need to send an email"** → Matches to SendGrid, Mailgun, Postmark with full specs
- **"Analyze this API: https://api.stripe.com"** → Deep capability analysis

## Pricing

| Action | Cost |
|--------|------|
| Query (find matching API) | $0.01 USDC |
| Search (specific provider) | $0.05 USDC |
| Deep analysis (from URL) | $0.10 USDC |

Payments via [x402 protocol](https://www.x402.org/) on Base mainnet. No API keys needed.

## Error Protection

- **No charge on errors** — If our API fails, you don't pay
- **Automatic credits** — Server errors give you free retry credits
- **Rate limits** — 60 req/min per wallet to prevent abuse

## Links

- **API:** https://semanticapi.dev
- **Docs:** https://semanticapi.dev/api/docs
- **Built by:** [Cove AI](https://coveai.dev)
- **X/Twitter:** [@semanticapiguy](https://x.com/semanticapiguy)
- **LinkedIn:** [Peter Thompson](https://linkedin.com/in/peter-j-thompson)

## License

MIT
