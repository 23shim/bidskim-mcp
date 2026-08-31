---
name: renewal-radar
description: Find UK public-sector contracts in the user's market that expire soon, who holds them, and which ones to engage now. Use when the user asks about expiring contracts, contract renewals, incumbents, or wants pipeline beyond published tenders.
---

# Renewal Radar

Build a renewal pipeline for the user's business: contracts likely to re-tender, ranked by how soon the buyer should be engaged.

## Steps

1. **Pin the market.** If the user hasn't said what they sell or where, ask once (one question covering service + region + rough contract size). Don't guess a sector.
2. **Pull the horizon.** Call `search_renewals` with a keyword for their service, `expiring_within_months: 12`, and their regions. If they gave a competitor, run a second search with `incumbent` set to that name.
3. **Split by urgency.** Re-run with `engagement_window_only: true` to isolate contracts where buyer engagement should start now (BidSkim's window is industry-tuned, roughly 3–9 months before expiry). Present two groups: "Engage now" and "Watch".
4. **Enrich the top few.** For the 3–5 most valuable "engage now" rows, call `get_tender` on the row id for the full record: recurrence evidence, certifications, TUPE, contract term. Only pass `include_contacts: true` if the user explicitly wants contact details — contact access is budgeted per day.
5. **Deliver a table**, one row per contract: title, buyer, incumbent, expiry date, value, and a one-line "why now". Note the value caveat once: values are published contract totals (`value_basis` says which figure), not guaranteed spend.

## Rules

- Expiry (trigger) dates derive from contract end / max-extension dates — say "expected to re-tender", never "will be re-tendered".
- If a search returns nothing, widen months before widening keywords; renewals are sparse in narrow niches.
- Never invent incumbents or dates: everything in the table must come from tool output.
