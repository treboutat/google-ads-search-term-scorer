# Negative Keyword Starter Library

A reference for `search-term-scorer`. These are the patterns that score 1-3 (negate candidates) in almost any account, plus industry-specific packs. They are *starting points* — always score against the actual objective before negating, and prefer phrase match for category-level blocks, exact match for surgical ones.

## Universal negatives (almost every B2B/lead-gen account)

| Category | Example terms | Default match type |
|---|---|---|
| Job-seeking | careers, jobs, hiring, salary, "interview questions", "job description", glassdoor, indeed | Phrase |
| Support / account | login, "sign in", "log in", support, "customer service", "phone number", "contact number", "track order" | Phrase |
| Free / DIY | free, "for free", DIY, template, "open source", crack, nulled, torrent, tutorial, "how to", "do it yourself" | Phrase |
| Education / research | course, "what is", definition, meaning, examples, pdf, "study", "thesis", wiki | Phrase |
| Cheap / bargain hunters | cheap, cheapest, discount, coupon, "promo code" (unless you compete on price) | Phrase |
| Nonsense / spam | profanity, obvious bot strings, single random characters | Exact |

## Industry packs

### B2B SaaS
Add: "free trial" abusers if you're sales-led, "alternative to" (route to a competitor campaign, don't negate blindly), "open source", "self hosted", "for students", "for nonprofits" (if out of ICP), "api documentation", "pricing" only if you don't want price-shoppers (usually keep).

### Healthcare / regulated
Add: "home remedy", "natural cure", "free clinic", "medicaid" (if you're cash-pay), "jobs"/"travel nurse" (job-seeking is heavy here), symptom-only research queries with no service intent. Watch compliance: never negate terms that block legitimate care-seekers from a service you offer.

### Local services
Add: "diy", "rental", "used", "parts", "repair near me" (if you only sell new/install), neighboring cities/states you don't serve, "how much does it cost" (usually keep — price intent), "salary".

### E-commerce
Add: "used", "refurbished" (if you sell new), "replica", "knock off", "wholesale" (if D2C), "free shipping" hunters (usually keep), competitor brand SKUs in non-competitor campaigns, "review"/"reviews" (keep — comparison intent).

## Match-type rule of thumb

- **Phrase match negative** for a *category* you never want ("free template", "jobs") — catches variants.
- **Exact match negative** for a *specific query* you don't want, where the broader phrase is fine ([salary] but you still want "salary benchmarking software").
- **Account/MCC-level** for universally bad terms across every campaign ("careers", "jobs").
- **Campaign-level** for offer-specific blocks that would be wrong in another campaign.

## Cautions

- Don't negate a term that has 1+ conversion just because volume is low — that's real intent.
- Don't negate a high-cost / zero-conv term first seen <14 days ago — too soon (conversion lag).
- Don't block "alternative to [competitor]" — that's a competitor-campaign opportunity, not waste.
