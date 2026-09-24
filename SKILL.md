---
name: search-term-scorer
description: Review a Google Ads search terms report against the actual offer and customer economics. Use when a user pastes a search terms report, says "score my search terms", "find negative keywords", "clean up my search terms", "what's wasting my spend", or uploads a search terms CSV. Assesses relevance, economics and confidence separately (a 1-10 relevance score sorts the review but never decides an exclusion by itself), then returns narrowly scoped exclusion proposals with a blocked and a protected example for each, a clean import block, protected demand, a watch list with review conditions, and historical spend labeled as historical.
---

# Search Term Scorer (search-term review for Google Ads)

Review the searches you paid to reach and the ones that could spend next. Exclude clear mismatches, protect valuable demand, and deal with searches whose economics don't work.

You don't need to pay for a click to recognize a query the business can't serve. You do need evidence before treating a relevant buyer as an unprofitable one. This skill prepares the decisions; a human approves every exclusion before it goes in.

## Inputs

Required:

1. **Search terms report.** Every row in scope, including zero-click and zero-conversion rows. Columns: search term, campaign, ad group, match type (and matching source where available), impressions, clicks, cost, conversions. Note the date range, currency and which conversion action the conversions column counts.
2. **The offer**, in 2-3 sentences: what it sells, who it's for, service geography, brand and competitor strategy, and who is explicitly not a customer. Mention any free trial, free plan, consultation or template you offer; they decide whether "free" searches are buyers.

Needed for economic decisions:

3. **The conversion definition and its acceptable cost** (target CPA, acceptable cost per qualified lead, or CAC limit), and whether that conversion has been checked against actual customers.
4. **Conversion lag:** how long after a click the conversion usually arrives.

Needed before anything is "ready to apply":

5. **Current negatives:** account-level exclusions, shared lists and the campaigns they're attached to, and campaign and ad-group negatives. Without them you can draft, but you can't call an exclusion ready.

If the offer is missing, ask for it before assessing anything. If economics or lag are missing, do the relevance review and say that economic decisions are on hold.

## Step 1: Record coverage

- Record the window, account timezone, currency, filters and when the report was pulled. For a first review the last 30 days is a practical start; extend it when volume is low or outcomes arrive slowly. On repeat runs, review new activity and refresh an overlapping window plus open watch-list items. Don't add overlapping snapshots together as new spend.
- Compare visible-query spend with the campaign's reported total for the same dates and filters. Google doesn't show every query, so label the difference as hidden or unexplained spend. Search-term insight categories aren't observed searches.
- **PMax:** its search-term reporting path and fields differ from Search. Make sure those rows are included if PMax is in scope. Search negatives don't control every PMax channel.
- **AI Max:** include its aggregate "Other search terms" when checking coverage. Filtering to the AI Max match-type label alone understates the total.
- When the same query appears in several campaigns, keep each campaign's context.

## Step 2: Assess relevance, economics and confidence separately

For each query in its campaign:

| Assessment | Question |
|---|---|
| Relevance | Does the search fit the offer and this campaign's intended customer or buying journey? |
| Economics | What do mature outcomes show against the acceptable cost and customer value? |
| Confidence | How strong is the evidence, and what's still unknown? |

**The 1-10 relevance score** sorts the review. It never decides an exclusion or a keyword addition by itself. Don't lower it because information is missing; missing information lowers confidence instead. It isn't Quality Score or a probability of becoming a customer.

| Score | Reading |
|---|---|
| 9-10 | Clear fit with the offer and intended customer |
| 6-8 | In category, fit plausible |
| 4-5 | Genuinely ambiguous intent |
| 2-3 | Points away from the offer or customer |
| 1 | Nothing to do with the offer |

**Economics** is `acceptable`, `unacceptable`, `pending` or `unavailable`:

- Judge the age of the clicks and outcomes, not when the term first showed up. Recent cost is fully reported while conversions arrive later. Use the account's own conversion lag, and refresh older rows for late conversions.
- Use query-level customer outcomes only where attribution supports the link. Don't assign an aggregate customer rate to individual queries as if it were observed, and don't compare different conversion goals as if they're the same outcome.
- Match outcomes to the click cohort that produced them. Customers closed this month may come from last month's clicks.
- A query that has spent a fraction of one acceptable conversion's cost has no economic verdict yet. It's `pending`.

**Confidence** is `high`, `medium`, `low` or `unknown`.

Write a one-line reason for every row. The reason is what lets the reader trust or overrule the call.

## Step 3: Choose the action from the evidence

| Evidence | Action |
|---|---|
| Clear mismatch with the offer or campaign objective | Propose a narrow exclusion now, even at one impression and zero clicks. |
| Plausible buyer intent with sparse or immature evidence | Keep it eligible and watch it, with a review condition and the exposure the business will accept while it waits. |
| Relevant demand with acceptable mature economics | Protect it from accidental exclusion; note any specific improvement or expansion opportunity. |
| Relevant demand with persistently unacceptable mature economics | Find the right control: bid or target, page, offer, conversion signal, or a narrow economic exclusion. |
| Looks like wrong intent but has recorded conversions | Check the conversion definition, attribution and downstream outcomes before deciding which evidence is misleading. |

None of these decides anything on its own:

- A click count. There's no automatic exclusion at 100 clicks.
- One conversion. It doesn't protect a query forever.
- High impressions with no clicks. That isn't proof of wrong intent.
- A waiting period. There's no universal 14-day rule: clearly irrelevant intent doesn't need a paid test, and economic calls need the account's own conversion cycle. After AI Max is enabled, Google recommends at least two weeks before routine optimization changes. Note that context; a confirmed offer mismatch can still be excluded.
- Words like `free`, `jobs`, `login`, `template`, `tool` or `how to`. They aren't universal negatives. A free trial, a support product, a template-led buying journey or a hiring product makes them buyer searches.

**Economic exclusions** are for relevant queries that don't pay. First check whether a workable bid, a better page or a better conversion signal could fix the economics. You don't have to run every possible test. If mature evidence stays unacceptable, propose a narrowly scoped negative and label the reason economic; don't relabel the query irrelevant. Record the reason, query, scope, date applied, reviewer, and a reassessment in about a month, or sooner if a stronger conversion signal, more reliable data and better observed performance justify another look. The review date isn't an automatic expiry. Before any retest, check that account, shared-list or campaign negatives won't still block the query in the test.

Group related queries to diagnose a pattern, but a weak family average doesn't prove every query in it should go. If the same problem shows up across many queries, the fix may be measurement or structure rather than a longer negative list.

## Step 4: Build the exclusions and the protected list

`references/exclusion-checks.md` has the matching and scope rules. In short:

- **Exact** excludes the query with no extra words. **Phrase** requires the phrase in order. **Broad** requires every term, in any order. Negatives don't cover synonyms or singular/plural forms; Google handles casing and misspellings.
- A one-word phrase negative such as `"free"` blocks as much as the same one-word broad negative.
- Use the narrowest exclusion that gets the intended coverage. Don't turn one bad query into a broad word or phrase exclusion without evidence for the wider decision.
- For every proposed negative, show **a search it blocks** and **a nearby buyer search it must not block**. Check the combined effect with existing account, shared-list, campaign and ad-group negatives.
- Scope deliberately. Use account level only for intent the business wants excluded everywhere. A shared list affects every campaign it's attached to. Campaign or ad-group level handles local exclusions. Brand and competitor routing need an explicit strategy and an eligible destination campaign.

Keep opportunities separate from the apply list. A high relevance score doesn't mean the query needs its own exact keyword. Recommend an addition only for a specific purpose (routing, ad relevance, landing-page fit) after checking existing coverage, and remember an exact keyword doesn't guarantee exclusive routing. A report row marked "Exact" doesn't prove the triggering keyword is exact match.

## Output format

Deliver in this order and lead with the decisions.

### 1. Coverage and findings
Rows reviewed, window, visible vs reported spend (and the hidden share), mature vs pending outcomes, and the decisions that matter.

### 2. Assessed terms
| Search term | Campaign | Cost | Conv | Relevance (1-10) | Economics | Confidence | Decision | Reason |
|---|---|---|---|---|---|---|---|---|

Decision is `protect`, `watch`, `intent_negative_candidate` or `economic_negative_candidate`.

### 3. Proposed exclusions
| Negative | Match | Scope | Basis (intent or economic) | Evidence | Confidence | Blocks | Must not block |
|---|---|---|---|---|---|---|---|

### 4. Clean import block
Only the candidate text, with the match type and destination set explicitly. No notes, scores or labels in keyword text. Adding a negative from the Search terms report in Google Ads defaults to negative exact; a Google Ads Editor import can default to broad when the type is omitted.

### 5. Protected demand and opportunities
Valuable queries, conflicts with existing negatives, and any specific keyword or page opportunity with its purpose.

### 6. Watch list and open questions
For each item: the unresolved question, current exposure, the review condition, the exposure the business will accept while waiting, and who reviews it. Include economic exclusions due for reassessment.

### Spend on proposed exclusions
State it as **historical spend in this window**, and name the denominator if you show a percentage. It isn't realized savings, and the skill doesn't project a CPA reduction: the next dollar may go to different queries, and total spend and conversion volume can change too. A zero-click query has no paid cost to report. An accurate review can propose zero exclusions.

## Example run (hypothetical)

**Offer:** "$1,200/yr HR-compliance SaaS for US companies with 50-500 employees, with a 14-day free trial. Not for solo HR consultants or people looking for free templates." Conversion = demo request, checked against pipeline. Acceptable cost per demo: $400. Most demos arrive within 7 days of the click. Window: last 30 days, NB-Search only. Visible-query spend is $586 of $640 reported, so $54 (8%) isn't visible.

| Search term | Cost | Conv | Rel. | Economics | Decision | Reason |
|---|---|---|---|---|---|---|
| hr compliance software for mid size company | $96 | 2 | 10 | acceptable, sparse | protect | Product plus target company size |
| best hr compliance platform | $71 | 1 | 9 | acceptable, sparse | protect | Product, comparison intent |
| hr compliance software pricing | $44 | 1 | 9 | acceptable, sparse | protect | Product; price intent is buying intent |
| how to do hr compliance myself | $84 | 0 | 5 | pending | watch | "Myself" may mean without a consultant, which is who buys self-serve software |
| free hr policy template | $148 | 0 | 2 | n/a (intent) | intent_negative_candidate | Free-template seeker; the offer excludes them |
| hr compliance jobs remote | $110 | 0 | 1 | n/a (intent) | intent_negative_candidate | Employment search |
| hr compliance consultant salary | $33 | 0 | 1 | n/a (intent) | intent_negative_candidate | Salary research |
| hr compliance manager jobs near me | $0 (12 impr) | 0 | 1 | n/a (intent) | intent_negative_candidate | Employment search; exclude before it spends |

**Proposed exclusions (NB-Search campaign only):**

| Negative | Match | Blocks | Must not block | Confidence |
|---|---|---|---|---|
| `jobs` | Phrase | hr compliance jobs remote | job description compliance software | High |
| `consultant salary` | Phrase | hr compliance consultant salary | salary transparency compliance software | High |
| `free hr policy template` | Phrase | free hr policy template download | free trial hr compliance software | Medium: confirm there's no free-template lead magnet |

`free hr policy template` doesn't cover the plural "templates"; add that separately only if it shows up.

**Rejected:** bare `free` (blocks the free-trial search), bare `salary` (blocks pay-transparency compliance searches), `how to` (blocks "how to choose hr compliance software").

**Watch:** "how to do hr compliance myself" stays eligible. Review it once its clicks are past the 7-day demo lag. The business accepts up to $400 of exposure (one demo's acceptable cost) before an economic assessment.

**Spend on proposed exclusions:** $291 of historical spend in this window, about 50% of visible-query spend ($586). Not a savings figure.

**Opportunity:** "hr compliance software for mid size company" fits well. An exact keyword is worth adding only if mid-size-specific ad copy or a mid-size page would serve it better than the current route.

## Hard rules

- **Assess against the offer.** No offer, no assessments. Ask.
- **Relevance, economics and confidence stay separate.** A score sorts; it doesn't decide.
- **Missing information lowers confidence, not relevance.** Uncertain but plausible demand goes on the watch list.
- **Use the narrowest exclusion that works**, with a blocked and a protected example for each.
- **Flag the query, not the keyword.** This skill doesn't recommend pausing keywords. Repeated problems route to structure, bidding, page or measurement work.
- **No savings claims or CPA projections.** Historical spend is historical.
- **A human approves each exclusion or clearly defined group**, naming the terms, match types and scope. New rows or broader exclusions don't inherit an earlier approval.

## Cadence

Weekly is a practical starting cadence for an active account. Review faster when spend pace, new launches or targeting changes justify it, and slower for a stable account with little new query data. Cadence is an operating choice, not a Google requirement or a quota of negatives per run. When checking results, look at current query rows and settings: a search-insight label can reflect older activity, including terms already excluded.

## Related skills

- **[`negative-library-starter`](https://github.com/treboutat/google-ads-negative-keyword-library):** the pre-launch complement. Build starter exclusions from the business before search-term data exists, then use this skill once real queries arrive.
- **[`ads-audit`](https://github.com/treboutat/google-ads-account-audit):** checks 20-24 set the targeting context this review runs in.

## Tone

Operational. The reader ships exclusions from this output, so accuracy beats narrative. If a term is unclear, say what's unclear and put it on the watch list. Never exclude on a guess.
