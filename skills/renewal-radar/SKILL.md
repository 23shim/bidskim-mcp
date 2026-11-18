---
name: renewal-radar
description: Find UK public-sector contracts in the user's market that expire soon, who holds them, and which ones to engage now. Use when the user asks about expiring contracts, contract renewals, incumbents, or wants pipeline beyond published tenders.
---

# Renewal Radar

Build a renewal pipeline for the user's business: contracts likely to re-tender, ranked by how soon the buyer should be engaged.

## Steps

1. **Pin the market.** Call `my_profile` first: it returns what the business does, its regions and the services it follows. Only if that is empty, ask once (one question covering service + region + rough contract size). Don't guess a sector.
2. **Name the service.** Call `search_services` with a word or two for the work and take the slug of the best match (or use a followed service's slug from `my_profile`). A service slug is far more exact than a keyword. If no service fits, fall back to a keyword.
3. **Pull the horizon.** Call `search_renewals` with `services: [slug]`, `expiring_within_months: 12`, and their regions. Add `buyer_types` when they name a kind of buyer (councils = `local_gov`, NHS = `health`). If they gave a competitor, run a second search with `incumbent` set to that name.
4. **Bring in what BidSkim already scored.** Run `search_renewals` with `scored_for_me: true` and `sort: "score"`: contracts BidSkim judged a fit for this business, best first. Rows carry `my_score`; say which rows came from this list.
5. **Split by urgency.** Re-run with `engagement_window_only: true` to isolate contracts where buyer engagement should start now (BidSkim's window is industry-tuned, roughly 3–9 months before expiry). Present two groups: "Engage now" and "Watch".
6. **Enrich the top few.** For the 3–5 most valuable "engage now" rows, call `get_tender` on the row id for the full record: recurrence evidence, certifications, TUPE, contract term, named bidders where the buyer published them. Only pass `include_contacts: true` if the user explicitly wants contact details — contact access is budgeted per day.
7. **Deliver a table**, one row per contract: title (linked with the row's `url`), buyer, incumbent, expiry date, value, and a one-line "why now". Note the value caveat once: values are published contract totals (`value_basis` says which figure), not guaranteed spend.

## Rules

- Expiry (trigger) dates derive from contract end / max-extension dates — say "expected to re-tender", never "will be re-tendered".
- If a search returns nothing, widen months before widening the service; renewals are sparse in narrow niches.
- An unknown service slug is refused, not ignored: go back to `search_services` rather than retrying with a guess.
- Never invent incumbents or dates: everything in the table must come from tool output.
