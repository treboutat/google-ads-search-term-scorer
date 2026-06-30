# Test — Edge case: thin / recent data (conversion lag)

**Scenario:** A term has meaningful spend and zero conversions, but it was first seen only a few days ago. The skill must **not** negate it — it goes on the watch list because of conversion lag.

## Input

**Offer:** "Managed Google Ads for home-services businesses (HVAC, plumbing, roofing), $3-5K/mo retainer, US only."

**Search terms report:**

| Search term | First seen | Clicks | Cost | Conv |
|---|---|---|---|---|
| google ads management for hvac | 45 days ago | 30 | $210 | 4 |
| ppc agency for plumbers | 6 days ago | 16 | $180 | 0 |
| hvac marketing jobs | 40 days ago | 12 | $70 | 0 |

## Expected behavior

- "hvac marketing jobs" → **negate** (job-seeking, scored 1, mature data).
- "ppc agency for plumbers" → **watch list, do NOT negate.** High cost, zero conv, but first seen 6 days ago. Under the 14-day conversion-lag rule it's too soon to judge. Decision rule: "Re-score after it reaches 14 days live and ~$300 spend; negate then if still zero conv."
- "google ads management for hvac" → keep (winner, $52 CPA).

## Pass criteria
- The recent high-cost/zero-conv term is **not** in the negative block.
- It appears on the watch list with an explicit re-score date/threshold.
- The skill cites the <14-day conversion-lag rule as the reason.
