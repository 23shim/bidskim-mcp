---
name: tender-scan
description: Search live UK tenders that fit what the user's business actually does and rank them by fit and deadline. Use when the user wants current tender opportunities, open procurements, or a scan of what's closing soon in their market.
---

# Tender Scan

Find live UK tenders worth the user's time — not just keyword matches.

## Steps

1. **Understand the capability.** Get a one-sentence description of what they sell, plus region and minimum contract value if they have one.
2. **Search both ways.** Run `search_tenders` (view `active`, their keyword + filters, sort by `deadline`) AND `semantic_search` with the plain-English capability description. Semantic search catches tenders that describe the work differently — retrofit programmes that never say "decarbonisation".
3. **Merge and dedupe by id.** Rank by: closing soonest, then value, then similarity score where present.
4. **Qualify the shortlist.** For the top 3–5, call `get_tender` and check hard gates: mandatory certifications, framework-only routes, TUPE. Flag any gate the user probably fails rather than hiding the tender.
5. **Deliver**: a shortlist table (title, buyer, value, deadline, one-line fit note, any gate flags), then the longer tail as a count with an offer to page through (`page` parameter, 25 rows per page).

## Rules

- Keyword queries need 3+ characters; semantic queries work best as a sentence describing the work.
- Deadlines are ISO dates — always restate them as "closes in N days".
- This skill finds and qualifies opportunities; it does not write bids.
