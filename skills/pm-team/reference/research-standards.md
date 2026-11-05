# Research standards

## Claim classification

Every material statement in research and product documents is tagged with one of:

| Tag | Meaning | Required |
|---|---|---|
| `[FACT]` | Verified from a source | Source URL (or file path) + date checked (YYYY-MM-DD). The source must support **this exact claim**, not just the topic. |
| `[INFERENCE]` | Conclusion drawn from facts | List the facts it is drawn from (by reference). |
| `[ASSUMPTION]` | Believed but not verified | Why we believe it + how to verify (verification plan). |
| `[PROPOSAL]` | Our suggested solution or design | Rationale; alternatives considered. |

Example:
```
- [FACT] Fresha offers free booking for salons and charges per payment processed (https://..., checked 2026-11-02).
- [INFERENCE] Competing on price alone is weak, because the market leader is already free to start (from F-3, F-4).
- [ASSUMPTION] Salons in BiH prefer WhatsApp reminders over SMS. Verify: 5 salon owner interviews.
- [PROPOSAL] Offer WhatsApp reminders in MVP; alternative: SMS via Infobip.
```

## Rules

1. **No invented specifics.** Never invent a competitor, price, statistic, user quote, market size or API capability. If you cannot find it, write `[ASSUMPTION]` or "unknown" with a verification plan.
2. **Primary sources first:** official product pages, pricing pages, API docs, regulators, company filings. Secondary (articles, reviews, forums) is fine for user sentiment, labeled as such.
3. **Recency:** record the check date. Prefer sources from the last 24 months for market/pricing claims; flag older ones.
4. **Competitor research ≠ user need.** What competitors build shows what exists, not what users need. User needs require interviews, data or experiments; until then they are `[ASSUMPTION]`s with a validation plan.
5. **When no documentation exists** for a needed solution: describe the best known approach from comparable solutions, tag it `[PROPOSAL]`, list the evidence it is based on, and propose the smallest test that would confirm it.
6. **Quote sparingly.** Summarize in your own words; at most one short quote per source.
7. **Search breadth:** use several queries and phrasings per topic, including the local market/language when the product is local.

## Research files

- `<project>/plan/research/brief.md`: input as received, interpreted problem, assumptions, open questions.
- `<project>/plan/research/market.md`: market, segments, trends, regulation.
- `<project>/plan/research/competitors.md`: table: name, link, target, core features, pricing, strengths, weaknesses, notes; plus "do nothing" / manual alternatives.
- `<project>/plan/research/users.md`: segments, jobs-to-be-done, pains, evidence (public reviews, forums, data), assumptions to validate.
- `<project>/plan/research/solutions.md`: technical and product approaches, APIs, build-vs-buy options.
- `<project>/plan/research/unknowns.md`: each unknown with verification plan.
- `<project>/plan/research/sources.md`: all sources with dates.
