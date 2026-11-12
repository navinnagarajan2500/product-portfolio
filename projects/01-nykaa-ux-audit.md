# 01 · Nykaa skincare UX funnel audit — v2

**Original submission:** `nykaa_report.pdf` + `nykaa_presentation.pdf` (Sep 2026)
**Mentor score:** 3.5 / 5
**Brief:** Audit a B2C purchase funnel, apply root-cause and problem-statement frameworks, propose a differentiation lever, test it.

## What the mentor said

> "Your entire audit rests on numbers I can't check… I'd go straight for 'walk me through 5 of those 400 reviews' or 'how did you verify Tira's winning lever is Personalization and not something else.'"

That is the whole problem in one sentence. The analysis was directionally right; the evidence behind it was a claim, not a record.

---

## What changed in v2

| v1 | v2 |
|---|---|
| "400+ reviews analysed" with category totals | A documented sample: platforms, dates pulled, inclusion rule, and 24 verbatim reviews tagged in full |
| "Tira's winning lever is Personalization" | The lever is derived from three observable product behaviours, each with a screenshot-level description and a date |
| Five friction points asserted from one journey | Each friction point carries a frequency count in the sample and one representative quote |
| Competitive claims unlinked | Every competitive claim has a checkable source line (app store listing, help-centre page, or dated observation) |

---

## Evidence appendix (the part v1 was missing)

**Sampling method.** Reviews pulled over 6 days in September 2026: Google Play (Nykaa Beauty, 150 most recent that mention skin or product mismatch), App Store India (80), r/IndianSkincareAddicts threads (60), Trustpilot India (110). Inclusion rule: the review has to describe an experience with *discovery, filtering, ingredient information, review credibility, or checkout*. Ratings-only and delivery complaints excluded. 400 candidates → **312 in scope → 24 retained for verbatim quotation** (six per friction category, chosen as the first six that matched, not the most damning).

That last clause matters. Picking the six angriest reviews would reproduce the same failure in a new form.

**Tagged sample, friction 02 — filters returning the wrong skin type (11 of 24 retained quotes):**

| # | Source | Date | Verbatim (trimmed) | Tag |
|---|---|---|---|---|
| 1 | Play Store | 2026-08-19 | "Selected dry skin, still showing me creams for oily. What's the point" | filter |
| 2 | Play Store | 2026-08-27 | "filter doesn't work, bought wrong product twice" | filter / mismatch |
| 3 | Reddit | 2026-09-02 | "Nykaa's skin type filter is a suggestion, not a constraint" | filter |
| 4 | Trustpilot | 2026-07-30 | "…ordered a moisturiser for normal skin after filtering for dry" | filter / mismatch |
| 5 | App Store | 2026-08-11 | "no way to filter by ingredient or exclude fragrance" | filter / ingredient |
| 6 | Reddit | 2026-08-23 | "I've stopped trusting the filter and just read every ingredient list" | workaround |

Retained but not shown here: six more in the same category (full table in the original appendix file). The honest summary is **11 of 24 in-scope reviews describe filter failure**, not "400 users are angry about filters".

**What this sample cannot tell you.** Reviews are self-selected and skew toward the aggrieved. It supports "this failure is common enough to investigate", not "X% of users experience it". A 400-review sample of complaint channels is not a funnel measurement, and v2 stops pretending it is.

## Competitive claim, made checkable

v1 asserted Tira wins on personalization. The defensible version is narrower and verifiable:

- **Observation 1 (Tira app, Sep 2026):** the skincare landing surface asks for skin type, concern, and sensitivity *before* showing a grid — a 3-step quiz, skippable.
- **Observation 2 (Tira PDP):** ingredient list is rendered as text in the page, with key actives surfaced above the fold.
- **Observation 3 (Nykaa PDP):** ingredient detail sits inside a product image on several SKUs, so it is not searchable or screen-readable.

So the claim is not "Tira's differentiation lever is personalization". It is: **Tira makes skin attributes a structured input; Nykaa makes them a browse filter.** That is a product-behaviour difference you can point at, and it is falsifiable — if Tira's quiz turns out to be non-binding in the actual filter results, the claim collapses.

## The recommendation, unchanged but now costed

Keep the v1 recommendation: make skin-barrier compatibility a hard attribute, not a tag. v2 adds the decision v1 lacked.

- **Ship:** a hard filter on 3 attributes (skin type, barrier-safe flag, fragrance-free) across the top 200 skincare SKUs, plus a structured ingredient field for the same set.
- **Kill if:** within 8 weeks, cart-add rate from filtered sessions is not at least 3 percentage points above unfiltered sessions, or the structured field is populated on under 70% of the 200 SKUs. Both conditions are measurable in existing analytics; no new instrumentation needed beyond a session flag.
- **Cost of being wrong:** ~6 engineering weeks plus a merchandising sprint for classification. Reversible — the filter can be hidden without deleting data.

## What I'd do next

Six moderated sessions, three of them with men buying for dry skin, asked to find a barrier-safe moisturiser while narrating. The prediction to test: they attempt the filter, discover it doesn't constrain, then abandon filtering and read ingredient images. If two of six don't do that, the root cause is wrong.
