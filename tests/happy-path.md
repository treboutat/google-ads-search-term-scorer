# Test: Happy path

**Scenario:** A B2B SaaS account pastes a search terms report with its offer, conversion definition, acceptable cost and lag. The skill should assess every term for relevance, economics and confidence, propose only narrow intent-based exclusions with blocked and protected examples, and report spend as historical.

## Input

**Offer:** "We sell a $1,200/yr HR-compliance SaaS to US companies with 50-500 employees, with a 14-day free trial. Not for solo HR consultants or people looking for free templates."

**Conversion:** demo request, checked against pipeline. Acceptable cost per demo: $400. Most demos arrive within 7 days of the click.

**Coverage:** last 30 days, NB-Search. Campaign-reported cost for the window: $640.

**Existing negatives:** none on NB-Search; no shared lists attached.

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
| hr compliance manager jobs near me | NB-Search | Software | 12 | 0 | $0 | 0 |

## Expected output (shape)

### 1. Coverage and findings
- 8 rows reviewed; visible-query spend $586 of $640 reported ($54, 8%, not visible).
- No row has spent enough to judge economics against a $400 demo cost, so every proposed exclusion is intent-based.

### 2. Assessed terms (representative)
| Term | Rel. | Economics | Decision | Reason |
|---|---|---|---|---|
| hr compliance software for mid size company | 10 | acceptable, sparse | protect | Product plus target size |
| best hr compliance platform | 9 | acceptable, sparse | protect | Comparison intent |
| hr compliance software pricing | 9 | acceptable, sparse | protect | Price intent is buying intent |
| how to do hr compliance myself | 5 | pending | watch | Could be a self-serve buyer |
| free hr policy template | 2 | n/a (intent) | intent_negative_candidate | Free-template seeker; offer excludes them |
| hr compliance jobs remote | 1 | n/a (intent) | intent_negative_candidate | Employment |
| hr compliance consultant salary | 1 | n/a (intent) | intent_negative_candidate | Salary research |
| hr compliance manager jobs near me | 1 | n/a (intent) | intent_negative_candidate | Employment; zero clicks, exclude anyway |

### 3. Proposed exclusions (NB-Search)
| Negative | Match | Blocks | Must not block |
|---|---|---|---|
| `jobs` | Phrase | hr compliance jobs remote | job description compliance software |
| `consultant salary` | Phrase | hr compliance consultant salary | salary transparency compliance software |
| `free hr policy template` | Phrase | free hr policy template download | free trial hr compliance software |

Rejected with reasons: bare `free`, bare `salary`, `how to`.

### 4. Clean import block
Campaign NB-Search; three rows with explicit match types; no notes or scores in the keyword text.

### 5. Protected demand
The three product searches, with the note that an exact keyword for "mid size company" is worth adding only for a specific routing, copy or page purpose.

### 6. Watch list
"how to do hr compliance myself": review after its clicks pass the 7-day demo lag; exposure the business accepts before an economic call: $400.

### Spend on proposed exclusions
$291 historical spend in this window, about 50% of visible-query spend. Not labeled savings.

## Pass criteria
- Every term has a relevance score, an economics status, a confidence level and a one-line reason.
- No exclusion is justified by the score alone; each proposed negative has a blocked and a protected example.
- `free`, `salary` and `how to` are **not** proposed as bare negatives, because each would block a buyer search.
- The zero-click employment query is proposed for exclusion despite having no cost.
- "how to do hr compliance myself" goes to the watch list, not the negative block.
- No CPA-reduction projection and no "savings" language.
- The skill does **not** recommend pausing the matched keywords.
