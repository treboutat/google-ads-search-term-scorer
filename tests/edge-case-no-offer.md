# Test: Edge case, no offer provided

**Scenario:** The user pastes a search terms report but doesn't describe the offer. The skill must not assess or exclude anything blind, and asks for the offer first.

## Input

"Here are my search terms, tell me what to cut:"

| Search term | Clicks | Cost | Conv |
|---|---|---|---|
| widget pro download | 40 | $120 | 0 |
| enterprise widget platform | 12 | $90 | 3 |
| free widget tool | 55 | $130 | 0 |

## Expected behavior

The skill produces no relevance assessments and no exclusions. It asks for the missing context in one message:

> Before I review these, I need:
> 1. What the business sells, who it's for, and who is explicitly **not** a customer.
> 2. Whether you offer a free trial, free plan, download or tool, since that decides whether "free widget tool" and "widget pro download" are buyers.
> 3. What the conversions column counts, what you can afford per conversion, and how long conversions usually take to arrive.
> 4. Your current negatives and where they're attached.
>
> Without the offer, "free widget tool" might be pure waste or your exact freemium entry point. Zero conversions on $130 doesn't settle it either way.

## Pass criteria
- No relevance scores, decisions or negatives are produced before the offer is supplied.
- The skill names *why* it can't assess blind, using a concrete example from the pasted data.
- It asks for non-customers and for any free or download offer, not just who the customers are.
- It doesn't treat zero conversions as proof of waste.
