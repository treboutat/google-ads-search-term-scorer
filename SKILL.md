---
name: search-term-scorer
description: Score Google Ads search terms 1-10 by relevance to the account's objective and surface negative-keyword candidates at scale. Use when a user pastes a search terms report, says "score my search terms", "find negative keywords", "clean up my search terms", "what's wasting my spend", or uploads a CSV from Google Ads. Outputs a relevance-scored list with one-line reasoning, an upload-ready negative keyword block, the high-relevance terms to protect, and an estimated CPA-reduction projection.
---

# Search Term Scorer (AI Negative Keyword Engine)

Manual search-term review surfaces maybe 20 negative candidates in a session. Scoring every term with AI surfaces hundreds in the same time. This is the highest-frequency optimization in a paid-search account and one of the most reliable levers on CAC: run consistently in higher-spend accounts, it typically takes CPA down by around 20%.

This is the self-contained version of TNT Growth's relevance-scoring methodology. You score every term 1-10 against the account's stated objective, flag the low-relevance ones for negation, and hand back an upload-ready negative keyword list plus the high-relevance terms worth protecting.

## How to use

The user provides a search terms report and the account's objective (what the business is trying to drive). You score every term 1-10 on **relevance to that objective**, write a one-line reason per term, and produce an upload-ready negative keyword list.

## Inputs

Required:

1. **Search terms report** — CSV or pasted table from the Google Ads Search Terms tab. Minimum columns: Search term, Campaign, Ad group, Impressions, Clicks, Cost, Conversions.
2. **The objective** — what the account is actually trying to drive, in 2-3 sentences. Who it's for, what it sells, payer/geo/service constraints if relevant, and explicit non-customers. *Every score depends on this.*
3. **Existing negatives** (optional but valuable) — so you don't recommend duplicates.

If the user pastes terms without the objective, ask for it first. Scoring without objective context is guesswork.

## The scoring rubric (1-10)

Anchor every score against the objective. When in doubt between two scores, **pick the lower one** — a false-positive negative is recoverable; a false negative keeps burning money.

| Score | Meaning | Action |
|-------|---------|--------|
| 10 | Perfect match — high intent, in-segment, payer/geo/service aligned | Keep + promote to its own exact-match keyword |
| 8-9 | Strong match — high intent and segment fit, missing one specifier | Keep / protect |
| 6-7 | Plausible — in-category but ambiguous on intent or segment | Keep, monitor CPA |
| 4-5 | Weak — in-category but a signal points the wrong way | Watch list; negate only if cost/conv is clearly poor |
| 2-3 | Poor — wrong segment, wrong audience, mostly noise | **Negate candidate** |
| 1 | Irrelevant — nothing to do with the offering | **Negate candidate** |

### Terms that score 1-3 (negate candidates)

- **Job-seeking:** "careers", "jobs", "hiring", "salary", "interview questions"
- **Support/login:** "login", "sign in", "support", "contact", "phone number" (unless brand-protect campaign)
- **Free/DIY:** "free", "DIY", "tool", "template", "open source", "tutorial", "how to do X yourself"
- **Wrong audience:** student/educator/researcher terms when selling to enterprise; B2C terms when selling B2B
- **Adjacent-industry mistakes:** terms that sound similar but mean a different industry's offering
- **Geographic mismatch:** locations the business doesn't serve
- **Competitor brand terms** appearing in non-competitor campaigns
- **Profanity / nonsense / spam queries**

The full category list with industry-specific packs (B2B SaaS, healthcare, local services, e-commerce) and match-type guidance lives in `references/negative-keyword-starter-library.md`. Load it before scoring an account in an industry you're unfamiliar with.

### Scoring 4-5 (weak) — scrutinize before negating

- Long-tail terms with low impressions but 1+ conversion → **keep** (real intent, just rare)
- Single-word broad terms with lots of impressions, no clicks, no conv → **negate** (Google misreading intent)
- Terms with high impressions and high CPC but no conv after 100+ clicks → **negate**

## Output format

Always produce these five sections, in order.

### 1. Summary

- Total terms scored: X
- **Low-relevance burn** — spend on terms scoring ≤3: $X (Y% of total)
- **High-relevance protected** — spend on terms scoring ≥8: $X (Y% of total)
- Wasted spend in last 30 days (cost on ≤3 terms with zero conversions): $X
- Projected CPA reduction if the ≤3 terms are negated: ~Y% (use TNT's ~20% benchmark as a ceiling, scaled by the share of wasted spend you're removing)

### 2. Negative keyword block (ready to paste into Google Ads)

A clean list, one term per line, grouped by recommended match type:

```
[Negative — Phrase match]
"free template"
"jobs"
"careers"

[Negative — Exact match]
[salary]
[login]
```

Use phrase match for category-level negatives (catches variants), exact match for specific queries you don't want to over-block.

### 3. Protect + promote (scored ≥8)

Table: Search term | Campaign | Spend | Conv | CPA | Recommendation (e.g. "Promote to exact-match keyword in Ad Group X", "Protect — do not let a broad negative catch this").

### 4. Watch list (scored 4-5)

Table: Search term | Campaign | Spend | Conv | Why it's borderline | Decision rule (e.g. "Re-score in 4 weeks if no conv after $200 cost").

### 5. Open questions

Anything you couldn't score because the objective was ambiguous or the data was missing.

> Whatever format you output, include a **one-line reason per scored term** (why that score). The reason is what lets the user trust — or overrule — the score.

## Example run

**Objective given:** "$1,200/yr HR-compliance SaaS for US companies with 50-500 employees. Not for solo HR consultants or free-template seekers."

**Search terms (excerpt):**

| Search term | Clicks | Cost | Conv |
|---|---|---|---|
| hr compliance software for mid size company | 14 | $96 | 2 |
| free hr policy template | 31 | $148 | 0 |
| hr compliance jobs remote | 22 | $110 | 0 |
| best hr compliance platform | 9 | $71 | 1 |
| how to do hr compliance myself | 18 | $84 | 0 |

**Scored (abbreviated):**

| Term | Score | Reason |
|---|---|---|
| hr compliance software for mid size company | 10 | Exact ICP + product match |
| best hr compliance platform | 8 | Strong intent, no size specifier |
| free hr policy template | 2 | "free template" — explicit non-customer |
| how to do hr compliance myself | 2 | DIY intent, not a buyer |
| hr compliance jobs remote | 1 | Job-seeker, wrong audience |

- **Summary:** 5 scored. Low-relevance burn (≤3): $342, 0 conv. High-relevance protected (≥8): 2 terms.
- **Negatives:** `[Phrase] "free template"`, `"jobs"`, `"how to"` / `"myself"`.
- **Protect + promote:** "hr compliance software for mid size company" → exact-match. Projected CPA reduction if ≤3 negated: ~10-12% (≈58% of spend is waste, capped against the ~20% benchmark).

## Hard rules

- **Always score against the objective.** If the user hasn't given one, ask. Do not score blind.
- **When in doubt, score lower.** False-positive negatives are recoverable; false negatives keep burning money.
- **Flag the term, never the keyword.** A term scored 1-3 means the *query* should be negated. The keyword that matched it is often fine; don't recommend pausing keywords from this report.
- **Match types matter.** Phrase-match negatives ("free template") catch variants. Exact-match negatives ([salary]) are surgical. Recommend the right one per term.
- **Conversion-lag awareness.** Don't negate a term that has spend but no conv if it was first seen <14 days ago. Put it on the watch list with a re-score date.
- **Recurrence.** Tell the user to run this 2-3x per week in high-spend accounts. Once a month is too slow; lookalike-training pollution accumulates.
- **Account-level vs campaign-level.** Recommend MCC-level master negative lists for universally bad terms ("careers", "jobs"). Campaign-level for offer-specific terms.

## Cadence guidance to give the user

- $0-50K/mo spend → run **weekly**
- $50-250K/mo spend → run **2x/week**
- $250K+/mo spend → run **3x/week** + automate with the API + AI in the account itself

In high-spend accounts, the first sweep typically surfaces hundreds of negative candidates. Steady-state is closer to 100 per run.

## Related skills

- **`/negative-library-starter`** — The complement: when an account is brand-new and has no search-term data yet, build a categorized starter negative library from the business first, then come back to this skill once data accrues.
- **`/ads-audit`** — Section D (keywords) sets the account context this skill operates in; run it first on a new account.
- **`/lead-quality-pattern-analysis`** — Search-term scoring is one step of the broader lead-quality system; when CVR is up but quality is down, run both.

## Tone

Operational. No editorializing. The user is shipping negatives based on this output, so accuracy matters more than narrative. If you're unsure about a term, score it in the 4-5 band and put it on the watch list. Never negate on a guess.
