# Search Term Scorer

Search-term review for Google Ads. Paste a search terms report and describe your offer; get back every term assessed for relevance, economics and confidence (with a one-line reason each), narrowly scoped exclusion proposals that each show a search they block and a buyer search they must not block, a clean import block, the terms worth protecting, and a watch list with review conditions.

The 1-10 relevance score sorts the review. It doesn't decide exclusions on its own, and the skill doesn't promise a CPA drop.

## Who it's for
Anyone running Google Ads Search or PMax who wants to cut clearly unwanted searches quickly without blocking buyers who just haven't converted yet.

## Install

**As a Claude Code skill:**
```bash
mkdir -p ~/.claude/skills/search-term-scorer
cp SKILL.md ~/.claude/skills/search-term-scorer/SKILL.md
cp -r references ~/.claude/skills/search-term-scorer/
```
Then trigger it in Claude by pasting a search terms report or saying "score my search terms."

**As a plain SOP:** read `SKILL.md` end to end. It's a complete procedure even if you never run it through Claude.

## What you provide
1. A search terms report (CSV or pasted table), including zero-click and zero-conversion rows: search term, campaign, ad group, match type, impressions, clicks, cost, conversions.
2. Your offer in 2-3 sentences: who it's for, what it sells, who is *not* a customer, and any free trial, free plan or templates you offer.
3. For economic calls: what the conversion column counts, what you can afford per conversion, and how long conversions take to arrive.
4. Your existing negatives and where they're attached, so proposals account for what's already blocked.

## Files
- `SKILL.md`: the skill / SOP
- `references/exclusion-checks.md`: how negative matching and scope actually work, and which common "universal negatives" need checking first
- `tests/`: worked example and edge cases (no offer, immature data, relevant but unprofitable)

## What changed in September 2026
Relevance, economics and confidence are now assessed separately, and the 1-10 score no longer triggers exclusions (the old "≤3 = negate" and "when in doubt, score lower" rules are gone). Uncertain but plausible searches go to a watch list instead. The CPA-reduction projection is removed; spend on proposed exclusions is reported as historical spend. The 14-day waiting rule is replaced by the account's own conversion lag, and every proposed negative now shows a blocked and a protected example.

---
From [TNT Growth](https://tntgrowth.com/skills?utm_source=github&utm_campaign=treboutat). Use it, fork it, adapt it to your account.
