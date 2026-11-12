# 07 · Zomato Tier-1 growth strategy — v2

**Original submission:** `Zomato_Tier1_Product_Strategy.pdf` (13 pages, Sep 2026)
**Mentor score:** 3.2 / 5

## What the mentor said

> "The strategy is coherent but the arithmetic isn't reconciled. 42% search-to-cart and 68% cart-to-payment and 72% of traffic at peak cannot all be true of the same funnel without the volume maths working out somewhere — and it doesn't. The tier-1 share of GOV at 55% and the 38% discovery bounce are presented as data when they're estimates. You're one assumption ledger away from a strong document."

Right: thirteen pages of confident percentile claims, none of which were tracked back to a source or to each other.

---

## What changed in v2

1. **Assumption ledger** at the top — every number tagged `[PUBLIC]`, `[DERIVED]`, or `[ASSUMPTION]`.
2. **Funnel arithmetic reconciled** — the stage conversions now produce a consistent monthly order count.
3. **Three initiatives instead of eight**, each with a kill criterion.
4. Removed the "10-page comprehensive deep dive" framing. Length was never the deliverable.

---

## Assumption ledger

| # | Claim | Value | Tag | Basis |
|---|---|---|---|---|
| 1 | Tier-1 share of GOV | 55% | `[ASSUMPTION]` | Widely repeated in earnings commentary; not verified against a filing |
| 2 | Peak share of daily traffic (12:30–14:00, 20:00–22:00) | 72% | `[ASSUMPTION]` | Plausible for food delivery; unsourced |
| 3 | Discovery → cart | 42% | `[ASSUMPTION]` | Industry-typical band, not Zomato's actual number |
| 4 | Cart → payment | 68% | `[ASSUMPTION]` | Same |
| 5 | On-time delivery | 86% | `[ASSUMPTION]` | Same |
| 6 | 38% of sessions bounce in discovery | 38% | `[DERIVED]` | = 100 − 42 − (sessions that never reach discovery), a subtraction dressed as a finding |

Line 6 is the one the mentor caught. "38% bounce in discovery" is not a measurement — it is whatever is left after the 42% figure. Presenting it as a separate finding double-counts, and v2 says so instead of quietly deleting it.

## Funnel arithmetic, reconciled

v1's three stage figures were used to justify three separate initiatives, each with its own "+1000bps" target, without ever being multiplied together. Multiplying them:

```
If 1,000 sessions enter Discovery:
  420 reach cart        (42%)
  286 reach payment     (68% of 420)
  × completion ~95%     (assumed, unstated in v1)
  ≈ 272 orders          (27.2% session-to-order)
```

v1 implied the three improvements would each be additive — 42→52, 68→78, 86→94 — which would produce `0.52 × 0.78 = 40.6%` session-to-order, a **50% relative improvement in orders**. That claim never appeared in the document, because nobody multiplied. When you do, it's obviously too large, which is the tell that the targets were chosen for how they read rather than how they compound.

v2 restates targets multiplicatively and modestly: **+300bps on discovery→cart, +300bps on cart→payment**, giving ~30% session-to-order. Still a strong claim, but one that survives being multiplied.

## The three initiatives that survive

**1. All-in pricing at discovery.** Surface a fee-inclusive price on listing cards for a subset of restaurants. v1 called this "transparent pricing" and buried it under personalisation. It is the highest-confidence lever because bill shock at payment is the most commonly reported friction and is directly measurable as back-navigation from the payment screen.

*Kill if:* back-navigation doesn't fall within 4 weeks, or restaurant partners refuse the display (a real risk — fee-inclusive prices look higher next to competitors).

**2. Peak-aware ETA, not a personalisation engine.** v1's headline initiative was a "contextual hyper-personalisation engine" — an intent ribbon. For a 15-engineer org that is a two-quarter build for an unproven lift. v2 replaces it with a narrower version: during peak windows only, show ETA as a range and rank by *reliability* rather than by rating. Cheap, uses existing prep-time data.

*Kill if:* order-through rate on peak sessions doesn't improve, or rider utilisation falls (ranking by reliability can concentrate orders on a subset of restaurants).

**3. Proactive delay credit — capped.** Keep v1's best idea but bound the cost, which v1 never did. Auto-issue a micro-credit when the ETA slips past a threshold, before the user complains.

*Cost base:* if 14% of orders slip and the credit is ₹25, at 286 surviving orders per 1,000 sessions the credit costs ~₹3.50 per 1,000 sessions. That's affordable. v1 proposed the mechanism with no ceiling; v2 caps total spend at 1.2% of GOV and pauses the programme if the support-ticket reduction doesn't offset it.

## Cut from v1

Infinite-scroll redesign, cross-sell modal reduction, "1-Tap UPI intent" (that's a payments-partner capability, not a product strategy), and the retention cohort section — which was three paragraphs of undifferentiated advice with no numbers attached to any cohort.

## What v1 got right

The three-stage framing (discovery → placement → delivery) is a better structure than the usual "acquisition/activation/retention" for this problem, and the observation that tier-1 users are multi-homing with near-zero switching cost is the strategic fact that makes reliability, not breadth, the lever. Both survive.
