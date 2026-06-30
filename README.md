# Search Term Scorer

AI negative-keyword engine for Google Ads. Paste a search terms report and your objective; get back every term scored 1-10 for relevance (with a one-line reason each), an upload-ready negative keyword block, the high-relevance terms to protect, a watch list, and an estimated CPA-reduction projection.

This is the single highest-frequency optimization in a paid-search account. Manual review finds ~20 negatives a session; scoring every term finds hundreds.

## Who it's for
Anyone running or managing Google Ads search/PMax spend who wants to cut wasted spend systematically instead of eyeballing the search terms tab once a month.

## Install

**As a Claude Code skill:**
```bash
mkdir -p ~/.claude/skills/search-term-scorer
cp SKILL.md ~/.claude/skills/search-term-scorer/SKILL.md
cp -r references ~/.claude/skills/search-term-scorer/
```
Then trigger it in Claude by pasting a search terms report or saying "score my search terms."

**As a plain SOP:** read `SKILL.md` end to end. It's a complete standard operating procedure even if you never run it through Claude.

## What you provide
1. A search terms report (CSV or pasted table) — needs Search term, Campaign, Ad group, Impressions, Clicks, Cost, Conversions.
2. Your offer in 2-3 sentences (who it's for, what it solves, who is *not* a customer).
3. Optional: your existing negatives, so it doesn't suggest duplicates.

## Files
- `SKILL.md` — the skill / SOP
- `references/negative-keyword-starter-library.md` — universal + industry-specific negative patterns
- `tests/` — worked example (happy path) and edge cases

---
From [TNT Growth](https://tntgrowth.com/skills?utm_source=github&utm_campaign=treboutat). Use it, fork it, change the thresholds to fit your account.
