---
name: tender-scan
description: Search live UK tenders that fit what the user's business actually does and rank them by fit and deadline. Use when the user wants current tender opportunities, open procurements, or a scan of what's closing soon in their market.
---

# Tender Scan

Find live UK tenders worth the user's time — not just keyword matches.

## Steps

1. **Understand the capability.** Call `my_profile` first: it returns what the business does, its regions, certifications and the services it follows. Only if that is empty, get a one-sentence description of what they sell, plus region and minimum contract value if they have one.
2. **Search three ways.** Call `search_services` for the work and pass the best slug as `services` to `search_tenders` (view `active`, sort by `deadline`, plus `buyer_types` if they named a kind of buyer). Run `search_tenders` again with their keyword if no service fits. AND run `semantic_search` with the plain-English capability description: it catches tenders that describe the work differently — retrofit programmes that never say "decarbonisation".
3. **Merge and dedupe by id.** Rank by: closing soonest, then value, then similarity score where present.
4. **Qualify the shortlist.** For the top 3–5, call `get_tender` and check hard gates: mandatory certifications, framework-only routes, TUPE. Flag any gate the user probably fails rather than hiding the tender.
5. **Size up the competition.** For the 2–3 strongest, call `similar_contracts` with the tender id: who won the same job before, for how much, and who else bid where the buyer published it. An empty bidder list never means nobody else bid.
6. **Deliver**: a shortlist table (title linked with the row's `url`, buyer, value, deadline, one-line fit note, any gate flags, previous winner where found), then the longer tail as a count with an offer to page through (`page` parameter, 25 rows per page).

## Rules

- Keyword queries need 3+ characters; semantic queries work best as a sentence describing the work.
- An unknown service slug is refused, not ignored: go back to `search_services` rather than retrying with a guess.
- Deadlines are ISO dates — always restate them as "closes in N days".
- This skill finds and qualifies opportunities; it does not write bids.
