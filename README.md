# Koot — by Datakoot

One call that does the work of many lookups. Koot briefs your AI agent on a software stack, a public company, a domain or a US place, and answers in one line, with the details underneath.

```
https://koot.datakoot.com/mcp
```

No API key for the free briefs (5 a day). Built on the nine [Datakoot](https://datakoot.com) official-data servers.

## Tools

| Tool | What it does | Sources |
|---|---|---|
| `brief_stack` | "Is my project safe?" Checks every package for known vulnerabilities, ranks them by real-world exploitation (CISA KEV, FIRST EPSS), flags abandoned packages and npm malware placeholders, and returns a fix-first list | OSV.dev, CISA KEV, FIRST EPSS, npm / PyPI / crates.io |
| `brief_company` | A US public company in one call: SEC profile, recent filings (8-K material events flagged), insider trades and reported financials | SEC EDGAR |
| `brief_domain` | A domain in one call: registration and DNS, email security (SPF/DKIM/DMARC), tech stack, subdomains from certificate logs | RDAP, DNS, Certificate Transparency |
| `brief_place` | A US place in one call: current conditions, forecast, active alerts for the state, nearby earthquakes, elevation | NWS, USGS, US Census |
| `koot_watch` | **Pro.** Tell Koot once what to watch (packages, a pasted package.json, and/or company tickers). Optional daily alerts to Slack or Discord | |
| `koot_whats_new` | **Pro.** "Anything new?" Reports only what changed: newly exploited or likely-exploited issues in your packages, and new SEC filings from your companies | |
| `koot_watches` | **Pro.** Lists what Koot is watching | |
| `koot_unwatch` | **Pro.** Stop watching some or all items, or turn alerts off | |

## Quick start

```
claude mcp add --transport http koot https://koot.datakoot.com/mcp
```

Or point any MCP client at `https://koot.datakoot.com/mcp`.

## Try it in 10 seconds — no key, no signup

```bash
curl -s https://koot.datakoot.com/mcp \
  -H 'content-type: application/json' \
  -H 'accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"brief_stack","arguments":{"packages":["lodash@4.17.15","express@4.17.1"]}}}'
```

The `koot` field answers in one line, for example: *"⚠️ No confirmed exploitation, but 2 issue(s) have a high exploit probability (EPSS ≥ 10%). Fix first: npm:lodash@4.17.15."*

Or just ask your agent:

- "Is my package.json safe to ship?"
- "Brief me on Tesla's recent SEC filings."
- "What's the weather risk in Pine Grove, PA today?"

## Pricing

- **Free:** 5 briefs a day, no key, no signup.
- **Pay per brief:** $0.01 in USDC on Base through [x402](https://datakoot.com/guides/pay-per-call-mcp-with-x402), with no account, at `https://x402.datakoot.com/mcp`.
- **Pro ($15/mo):** unlimited briefs, plus Koot Watch. Send your key as `Authorization: Bearer <key>` (or `X-Datakoot-Key: <key>`). [Pricing](https://datakoot.com/pricing).

## Data & attribution

Data comes from official public sources: NIST NVD and CISA KEV (US public domain), FIRST EPSS, OSV.dev (CC-BY 4.0), SEC EDGAR, the National Weather Service, USGS and the US Census Bureau. No API keys. No signup. No data resale.

Part of [Datakoot](https://datakoot.com): official-source data for AI agents, one keyless call.
