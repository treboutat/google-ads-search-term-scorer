# Test — Edge case: no offer provided

**Scenario:** The user pastes a search terms report but gives no description of the offer. The skill must refuse to score blind and ask for the offer first.

## Input

"Here are my search terms, tell me what to cut:"

| Search term | Clicks | Cost | Conv |
|---|---|---|---|
| widget pro download | 40 | $120 | 0 |
| enterprise widget platform | 12 | $90 | 3 |
| free widget tool | 55 | $130 | 0 |

## Expected behavior

The skill does **not** produce scores. It asks for the offer using the required 3-part prompt:

> Before I score these, I need the offer in 2-3 sentences:
> 1. What does the business sell, and who is it for?
> 2. What problem does it solve, and roughly what does it cost?
> 3. Who is explicitly **not** a customer?
>
> Scoring without offer context is guesswork — "free widget tool" might be pure waste, or it might be your exact freemium top-of-funnel. I can't tell which without the offer.

## Pass criteria
- No 1-10 scores are produced before the objective is supplied.
- The skill explicitly names *why* it can't score blind (uses a concrete example from the pasted data).
- It asks for non-customers, not just customers.
