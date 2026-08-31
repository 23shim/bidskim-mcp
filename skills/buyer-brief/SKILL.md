---
name: buyer-brief
description: Research a UK public-sector buyer before bidding - their awards, spend patterns, top suppliers, and upcoming renewals. Use when the user names a council, NHS trust, or other public body and wants to understand it, or asks "what has X bought/awarded".
---

# Buyer Brief

Produce a pre-bid brief on one UK public-sector buyer.

## Steps

1. **Resolve the buyer.** Call `search_organisations` with `kind: "buyer"` and the name. If several candidates match, show them and ask which — councils and trusts have similar names.
2. **Pull the profile.** Call `get_buyer` with the chosen id: headline stats, top suppliers by value, upcoming renewals, and BidSkim's researched positioning notes where available. Only pass `include_contacts: true` on explicit request (budgeted per day).
3. **Map the incumbents.** For the 2–3 suppliers dominating the buyer's spend in the user's category, call `get_supplier` to see their footprint — where else they win, and where their contracts expire.
4. **Check live demand.** Run `search_tenders` filtered to this buyer's name as the query to catch anything open right now.
5. **Deliver the brief** in four short sections: Who they are (stats), Who wins with them (suppliers + values), What's coming up (renewals with dates and incumbents), Openings (live tenders + the single best next action).

## Rules

- Attribute every number to the data ("awarded value across N deduplicated contracts"), and note that totals exclude framework ceiling values.
- Positioning notes exist for many buyers, not all — when absent, say so rather than padding.
- Keep the brief under a page unless asked for depth.
