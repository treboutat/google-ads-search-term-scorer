# Exclusion Checks

Reference for `search-term-scorer`. Use it for every proposed negative: how matching actually works, where to put the exclusion, and which common "universal negatives" need checking against the offer first.

Checked against Google documentation in September 2026. Re-verify before relying on a platform detail.

## How negative matching works

| Negative | Match | Blocks | Doesn't block |
|---|---|---|---|
| `remote jobs` | [Broad](https://support.google.com/google-ads/answer/7302703?hl=en) | jobs for remote accountants | remote accountant |
| `remote jobs` | [Phrase](https://support.google.com/google-ads/answer/7302992/negative-phrase-match-definition) | entry level remote jobs | jobs for remote accountants |
| `remote jobs` | [Exact](https://support.google.com/google-ads/answer/7302926?hl=en) | remote jobs | entry level remote jobs |

These rows explain matching only. They aren't a recommended employment list.

- Broad requires every negative term, in any order. Phrase requires the phrase in order. Exact excludes the complete query with no extra words.
- Negatives don't cover synonyms or singular/plural forms. None of the rows above blocks "remote job". Google's guidance says casing and misspellings are handled automatically; that isn't general semantic expansion. [Matching guidance](https://support.google.com/google-ads/answer/2453972?hl=en)
- A one-word phrase negative is no narrower than the same one-word broad negative. `"free"` still blocks "free trial crm software".
- A list's category name doesn't participate in matching. Only its actual negatives do.
- Google documents a limit when the negative term appears after the sixteenth word of a long query.
- "Doesn't block" means the negative doesn't prevent eligibility. It doesn't promise an ad will serve.

## Where to put it

- **Account level:** only for intent the business wants excluded across every affected campaign. It applies to eligible Search and Shopping inventory in supported campaign types, including future campaigns. [Account-level negatives](https://support.google.com/google-ads/answer/11396330?hl=en)
- **Shared list attached to named campaigns:** for campaigns that share the same exclusions. Creating a list doesn't apply it. Editing a list changes every campaign using it, including ones outside the task. [Shared lists](https://support.google.com/google-ads/answer/2453983?hl=en)
- **Campaign or ad group:** for local exclusions. If a manager-account list is involved, identify its owner and every affected account and campaign before editing it. A manager-account list is a governance choice, not a spend-tier requirement.
- Don't make own-brand, competitor or offer-specific exclusions account-wide just because several campaigns need them.
- **Performance Max:** negative keywords cover Search and Shopping inventory, not every channel. [PMax negative scope](https://support.google.com/google-ads/answer/15726455?hl=en)
- **Demand Gen:** current setup documentation says negative keywords and brand exclusions aren't eligible. Don't promise a Search list controls Demand Gen delivery. [Demand Gen limitations](https://support.google.com/google-ads/answer/17122651?hl=en)
- **Brand separation:** an exact negative `[brandname]` blocks the bare brand query, not "brandname pricing". For broader brand exclusion, look at brand lists or an explicitly scoped negative set, and test the variants you mean to cover. New Search brand exclusions can require AI Max; inspect its matching, text and URL settings before choosing that route. [Brand settings](https://support.google.com/google-ads/answer/13721847?hl=en)
- If the plan routes demand to another campaign, confirm that campaign is active, eligible and set up to capture it. An exclusion in one campaign doesn't make another one win the search.

## Words that need checking before they become negatives

These are prompts for investigation, not a list to paste.

| Candidate | What has to be true before excluding |
|---|---|
| Employment (jobs, careers, salary, hiring) | The search seeks a job or salary information this campaign doesn't serve. Hiring, recruiting and payroll-compliance products may need these words. |
| Education or DIY (how to, tutorial, course, what is, template, examples) | The learning or do-it-yourself intent is outside the campaign's goal. Tutorials, templates and documentation often sit inside a buying journey. |
| Support or troubleshooting (login, support, not working, error) | The search is outside the offer. Support software, repair services and replacement products acquire customers through problem searches. Brand campaigns may need login and support traffic routed correctly. |
| Free, discounts, piracy (free, cheap, coupon, crack, torrent) | Separate an unwanted free substitute or pirated product from a real trial, free plan, consultation, coupon or free-shipping offer. |
| Wrong product or audience | The query asks for something the business doesn't sell or a use case it can't serve. Confirm the actual limitation. |
| Fraud, privacy, compliance (fraud, spam, gdpr, tcpa, hack) | These can be the product category itself: fraud-prevention, compliance and security software sell on exactly these words. Never infer that a concerning word means a bad customer. |
| Healthcare, legal, local services (condition, cost, insurance, place names) | Verify the actual service and eligibility first. A search that looks like research can come from someone seeking the service. |
| Competitor names | Record the strategy first: exclude, buy in a separate campaign, or allow here. |

## Before it goes into the account

- Test each negative against both the target keywords and realistic buyer searches, including valuable ones absent from the keyword plan. A keyword-overlap check alone isn't enough.
- Apply the combined effect of existing and proposed exclusions at every inherited level. A protected-query list is a review tool; it doesn't override an active negative.
- Deduplicate by text, match type and scope. Don't delete an existing duplicate just to tidy up; it may serve a different attachment.
- Use a clean import file: explicit match type and destination, no notes or scores in the keyword text. Google Ads Editor can default an unspecified negative to broad. [Editor import formats](https://support.google.com/google-ads/editor/answer/47635?hl=en-GB)
- Record how to remove the term or detach the list. Removing a negative restores eligibility; it can't recover opportunities already missed.
