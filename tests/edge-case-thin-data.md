# Test: Edge case, immature data (conversion lag)

**Scenario:** A relevant term has meaningful spend and zero conversions, but its clicks are younger than the account's normal conversion lag. The skill must keep it eligible on the watch list with a review condition tied to that lag, while still excluding clear mismatches immediately regardless of their age.

## Input

**Offer:** "Managed Google Ads for home-services businesses (HVAC, plumbing, roofing), $3-5K/mo retainer, US only."

**Conversion:** booked sales call. Acceptable cost per booked call: $250. Most booked calls arrive within 21 days of the click. The business will accept up to $500 of exposure on an unproven relevant query before an economic review.

**Search terms report:**

| Search term | Clicks age | Impr | Clicks | Cost | Conv |
|---|---|---|---|---|---|
| google ads management for hvac | 25-60 days | 410 | 30 | $210 | 4 |
| ppc agency for plumbers | 0-6 days | 190 | 16 | $180 | 0 |
| hvac marketing jobs | 30-45 days | 160 | 12 | $70 | 0 |
| plumber jobs near me | 2 days | 3 | 0 | $0 | 0 |

## Expected behavior

- "google ads management for hvac" → **protect.** Relevant, mature, $52.50 per booked call against a $250 limit.
- "ppc agency for plumbers" → **watch, not excluded.** Relevant intent (relevance stays high). Its clicks are younger than the 21-day lag and it has spent less than one acceptable booked call, so economics are `pending`. Review condition: once its clicks are older than 21 days, or earlier if it reaches the $500 exposure limit. The review is an economic assessment, not an automatic exclusion.
- "hvac marketing jobs" → **intent exclusion.** Employment search. Its age has nothing to do with the decision.
- "plumber jobs near me" → **intent exclusion** even at 3 impressions and zero clicks. Report $0 historical cost; don't claim savings.
- Propose narrow negatives for the two employment searches, each with a blocked and a protected example (e.g. phrase `marketing jobs`, blocks "hvac marketing jobs", must not block "hvac marketing agency"; phrase `plumber jobs near me`, must not block "google ads for plumbers near me").
- **Reject bare `jobs`.** For home-services owners "jobs" means booked work, so it would block buyer searches like "how to get more hvac jobs".

## Pass criteria
- The recent relevant term is **not** in the negative block and its relevance score isn't lowered for missing data.
- Its review condition is tied to the account's 21-day lag and the business's exposure limit, not a universal 14-day rule or a "negate at $X if still zero" trigger.
- Both employment searches are proposed for exclusion regardless of click count or age.
- No bare `jobs` negative, because it collides with this offer's buyer language.
- No "zero conversions = waste" framing.
