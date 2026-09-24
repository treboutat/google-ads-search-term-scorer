# Test: Edge case, relevant but unprofitable

**Scenario:** A clearly relevant query has failed on mature economics. The skill must keep its relevance intact, propose a narrow exclusion labeled as economic, set a reassessment, and avoid blocking related queries that work.

## Input

**Offer:** "Payroll software for US small businesses, including restaurants and retail."

**Conversion:** accepted lead, validated against closed customers. Acceptable cost per accepted lead: $75. Accepted leads arrive within 10 days of the click. Tracking was checked and is healthy.

**Campaign:** NB - Payroll - Core, tCPA at the $75 target. The landing page is the general payroll page; the business has decided not to build a restaurant page this quarter.

**Search terms report (clicks 45-120 days old):**

| Search term | Clicks | Cost | Accepted leads |
|---|---|---|---|
| payroll software for restaurants | 190 | $1,500 | 0 |
| restaurant payroll services | 40 | $120 | 2 |

## Expected behavior

- "payroll software for restaurants": relevance stays high (the offer serves restaurants). Economics `unacceptable`: $1,500 of mature spend, zero accepted leads, against $75. Bidding is already at target and the page option is ruled out for now, so no further test is justified today.
- Propose a campaign-level **exact** negative `[payroll software for restaurants]` in NB - Payroll - Core, basis **economic**, not "irrelevant".
- Blocks: "payroll software for restaurants". Must not block: "restaurant payroll services" (working at $60 per accepted lead).
- Record reason, scope, reviewer and a reassessment in about one month, or sooner if a stronger conversion signal, more reliable data and better observed performance justify it. The date isn't an automatic removal.
- Optional: a monitored retest later, with a spend limit and outcome-based stop and success rules. Check that the new negative (or any account or shared-list negative) won't still block the query in the test.
- Report $1,500 as historical spend in the window, not savings.

## Pass criteria
- The query isn't relabeled irrelevant and its relevance score isn't lowered.
- The exclusion is exact and campaign-scoped. No phrase `restaurants`, no account-level block.
- The working sibling query is protected.
- A reassessment condition is recorded.
- No CPA projection.
