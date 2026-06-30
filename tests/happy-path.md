# Test — Happy path

**Scenario:** A B2B SaaS account pastes a search terms report with an objective. The skill should score every term 1-10 with a one-line reason, produce the five output sections, and hand back an upload-ready negative block.

## Input

**Objective:** "We sell a $1,200/yr HR-compliance SaaS to US companies with 50-500 employees. Not for solo HR consultants or free-template seekers."

**Search terms report:**

| Search term | Campaign | Ad group | Impr | Clicks | Cost | Conv |
|---|---|---|---|---|---|---|
| hr compliance software for mid size company | NB-Search | Software | 220 | 14 | $96 | 2 |
| best hr compliance platform | NB-Search | Platform | 140 | 9 | $71 | 1 |
| hr compliance software pricing | NB-Search | Software | 88 | 6 | $44 | 1 |
| free hr policy template | NB-Search | Software | 410 | 31 | $148 | 0 |
| hr compliance jobs remote | NB-Search | Software | 300 | 22 | $110 | 0 |
| how to do hr compliance myself | NB-Search | Platform | 260 | 18 | $84 | 0 |
| hr compliance consultant salary | NB-Search | Platform | 95 | 7 | $33 | 0 |

## Expected output (shape)

### Scores (with reasoning)
| Term | Score | Reason |
|---|---|---|
| hr compliance software for mid size company | 10 | Exact ICP (mid-size) + product match |
| best hr compliance platform | 8 | Strong intent, no size specifier |
| hr compliance software pricing | 7 | Plausible — price intent, in-category |
| free hr policy template | 2 | "free template" — explicit non-customer |
| how to do hr compliance myself | 2 | DIY intent, not a buyer |
| hr compliance jobs remote | 1 | Job-seeker, wrong audience |
| hr compliance consultant salary | 1 | Salary/job-seeker intent |

### 1. Summary
- Total terms scored: 7
- **Low-relevance burn (≤3):** $375, 0 conversions — "free hr policy template", "hr compliance jobs remote", "how to do hr compliance myself", "hr compliance consultant salary"
- **High-relevance protected (≥8):** $167 — "hr compliance software for mid size company", "best hr compliance platform"
- Projected CPA reduction if the ≤3 terms are negated: **~12-15%** (≈57% of the slice is waste; capped against the ~20% benchmark)

### 2. Negative keyword block
```
[Negative — Phrase match]
"free template"
"jobs"
"how to"
"salary"
```

### 3. Protect + promote (≥8)
| Term | Spend | Conv | CPA | Recommendation |
|---|---|---|---|---|
| hr compliance software for mid size company | $96 | 2 | $48 | Promote to exact-match keyword |
| best hr compliance platform | $71 | 1 | $71 | Protect; don't let a broad negative catch it |

### 4. Watch list (4-5)
- None in this slice. ("hr compliance software pricing" scored 7 — kept and monitored, not negated, not promoted.)

### 5. Open questions
- None. Objective was specific enough to score confidently.

## Pass criteria
- All 7 terms scored 1-10, each with a one-line reason.
- The 4 wrong-intent terms scored ≤3 and appear in the negative block; nothing borderline is negated.
- "When in doubt, score lower" applied (salary/jobs land at 1, not 4).
- The skill does **not** recommend pausing the matched keywords (flags the *term*, not the keyword).
- A dollar figure for low-relevance burn is computed, not hand-waved.
