<p align="center">
  <img src="logo-512.png" alt="BidSkim" width="120" height="120">
</p>

<h1 align="center">BidSkim MCP Server &mdash; UK Tenders, Contract Renewals &amp; Procurement Intelligence</h1>

<p align="center">
  UK procurement intelligence for AI assistants — live tenders, contract renewals with incumbents, service markets, frameworks, and buyer/supplier profiles.
</p>

<p align="center">
  <a href="https://smithery.ai/servers/bidskim/bidskim"><img src="https://smithery.ai/badge/bidskim/bidskim" alt="smithery badge"></a>
</p>

<p align="center">
  <a href="https://bidskim.com/mcp">Docs</a> ·
  <a href="https://bidskim.com">bidskim.com</a> ·
  <a href="https://registry.modelcontextprotocol.io">Official MCP registry: <code>com.bidskim/mcp</code></a>
</p>

---

BidSkim's official [Model Context Protocol](https://modelcontextprotocol.io) server. It is a **hosted remote server** — there is nothing to install or run locally. This repository holds the public documentation and brand assets for directory listings; the server itself is closed-source.

```
Endpoint:   https://mcp.bidskim.com/mcp
Transport:  Streamable HTTP (stateless, MCP spec 2026-07-28, with fallback for 2025-era clients)
Auth:       OAuth 2.1 (RFC 9728 discovery) or API keys minted in BidSkim Settings
Access:     read-only, included with the BidSkim Predict plan
```

## What it does

Fourteen read-only tools over UK public procurement data — Find a Tender, Contracts Finder, Public Contracts Scotland and Sell2Wales, entity-resolved and deduplicated to one record per opportunity. Every row comes back with a link to its BidSkim page.

**Tenders and renewals**

| Tool | What it answers |
| --- | --- |
| `search_tenders` | Live and historical tenders by service, buyer type, keyword, CPV, region, value and deadline |
| `semantic_search` | "Find tenders like this": meaning-based search over live tenders |
| `get_tender` | Full detail for one notice: services it is tagged to, the framework it sits under, certifications, named bidders where published |
| `similar_contracts` | For an open tender: who won the same job before, for how much, and who else bid |
| `search_renewals` | Contracts expiring soon: expiry dates, incumbent suppliers, and BidSkim's fit score for your business |

**Service markets**

| Tool | What it answers |
| --- | --- |
| `search_services` | Which of about 1,700 services a kind of work belongs to ("stairlifts", "school catering"), with its size over the last 12 months |
| `get_service_market` | The market for one service: who buys it, who wins it, totals, the split by buyer type and region, open tenders, contracts ending in the next 12 months |

**Buyers, suppliers and frameworks**

| Tool | What it answers |
| --- | --- |
| `search_organisations` | Buyers and suppliers by name, or ranked by who buys or wins a service |
| `get_buyer` | A buyer's award history, spend patterns and top suppliers |
| `get_supplier` | A supplier's wins, buyers served and market footprint |
| `search_frameworks` | About 17,000 framework agreements and DPSs: by service, by supplier, by who runs them, by end date |
| `get_framework` | One agreement: who runs it, its term, the suppliers on it and the contracts called off under it |

**Your account**

| Tool | What it answers |
| --- | --- |
| `my_profile` | The company profile BidSkim matches against and the services you follow, so the assistant knows what you do |
| `my_pipeline` | Your scored matches, saved tenders and tracked suppliers |

Typical prompts:

- *"Which contracts in my space expire in the next six months, and who holds them?"*
- *"Who wins stairlift work from councils in the North West?"*
- *"Who won contracts like this open tender, and who else bid?"*
- *"Which frameworks cover grounds maintenance, and which end in the next year?"*
- *"What has Manchester City Council awarded recently, and to whom?"*

## Connect

Full per-client walkthroughs: **[bidskim.com/mcp](https://bidskim.com/mcp)**

**Claude Code**

```bash
claude mcp add -t http bidskim https://mcp.bidskim.com/mcp
```

Or install this repository as a **Claude Code plugin** — it connects the server and adds three procurement workflow skills (`renewal-radar`, `tender-scan`, `buyer-brief`):

```bash
claude plugin install bidskim@<marketplace>
```

**Claude (web/desktop)** — Customize → Connectors → + Add → Add custom connector → `https://mcp.bidskim.com/mcp`

**ChatGPT** — Plugins → + → Add custom MCP server → `https://mcp.bidskim.com/mcp`

**Cursor / VS Code / Windsurf / Cline** — add a remote MCP server with URL `https://mcp.bidskim.com/mcp`; the OAuth sign-in opens in your browser. Signed-in BidSkim users connect with one approval click.

## Access

MCP access is included with the [BidSkim Predict plan](https://bidskim.com/pricing). All tools are read-only: your assistant can search and read, never change anything. Rate limits and daily budgets apply.

## Support

Questions or issues: [bidskim.com](https://bidskim.com) → support, or open an issue here.
