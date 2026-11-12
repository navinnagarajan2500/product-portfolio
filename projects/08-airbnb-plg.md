# 08 · Airbnb India product-led growth — v2

**Original submission:** `Airbnb_India_PLG_Strategy.pdf` (Sep 2026)
**Mentor score:** 4.1 / 5 — **noteworthy** (the only project marked noteworthy)

## What the mentor said

> "This is the strongest work in the cohort. The reasoning is genuinely good and the India-specific trust thesis is well argued. What's missing is decisions: nothing gets cut, no experiment can stop, and the revenue model has ingredients but no base underneath the percentages. You've written a strategy with no stops in it."

A 4.1 with a clear ceiling. The gap between this and a 5 is entirely "what would make you abandon this".

---

## What changed in v2

| v1 | v2 |
|---|---|
| Three pillars, all funded | Two pillars, one explicitly deferred with a trigger to reopen |
| Experiments described, none with stop rules | Every experiment has a pre-registered stop rule and a cost cap |
| Revenue model with percentages, no base | Base case stated, then sensitivity on the two variables that matter |
| "Connection density" as the north star | North star kept, but with a proxy metric that can be read weekly |

---

## What v1 got right (kept intact)

The core thesis stands and is the reason this scored well:

> In India, home-sharing carries a trust deficit relative to hotels, and Indian travellers default to trusting *people* over *platforms*. Therefore community features are not a differentiation layer — they are the conversion mechanism.

That reframes Airbnb India's growth problem from "acquire more guests" to "manufacture trust faster than the hotel category can". Everything else follows from it.

Also kept: **three-pillar structure (Stay, Experiences, Logistics) treated as one trip operating system rather than three marketplaces.** That is a genuine strategic insight, not a framework, and it's the reason the growth loops compound instead of competing.

## The cuts

v1 funded all three pillars. v2 funds Stay + Experiences and **defers Logistics entirely** — with a trigger.

- **Logistics (airport transfers, inter-city)** requires a supply-side partnership or a marketplace build, either of which is a 2+ quarter effort with a different sales motion.
- **Deferred until:** Stay shows a repeat-booking rate above 25% in two cities. Below that, there is no trip to attach logistics to.
- Writing that trigger down is the difference between a strategy and a wish list.

Also cut: the vernacular SEO programme as a *growth loop*. It is a marketing channel, it is not product-led, and including it in a PLG strategy required pretending that content acquisition is a loop. v2 keeps it as a supporting channel, outside the loop model, and stops claiming it compounds.

## Experiments with stop rules

v1 described four MVP features with success metrics. Not one had a stopping condition. v2 adds them:

| Experiment | Hypothesis | Stop rule | Cost cap |
|---|---|---|---|
| **Host-verified local guide** (host recommends 3 places, shown to guest in-app) | Guests who receive a guide rebook within 12 months at ≥1.3× the rate of those who don't | Stop if guide open rate <40% after 6 weeks in one city, or rebook lift <1.1× | 6 eng-weeks, 1 city |
| **Trust ladder** (verified ID → verified home → verified reviews, shown as a 3-step completion state) | Completion of all three steps raises first-booking conversion ≥10% | Stop if step-3 completion is <25% — the ladder is too long | 4 eng-weeks |
| **Local host circles** (city-level host groups with shared calendars) | Hosts in a circle accept ≥20% more bookings in shoulder season | Stop if circle formation <15% of invited hosts in 8 weeks | 3 eng-weeks + community ops |
| **Guest photo-to-listing match check** | Reduces "not as described" disputes by ≥30% | Stop if dispute rate doesn't move in 90 days | 3 eng-weeks |

Four experiments, four stop rules, four cost caps. That's the missing half of the document.

## The revenue model, with a base

v1 presented a revenue redesign with commission percentages but no base — so a reader couldn't tell whether "12% → 9% + experience fee" was a downgrade or an upgrade.

**Base case, stated explicitly as an assumption:**

```
Assume a city with:
  1,000 active listings, 40% occupancy, 3.2 nights average stay
  → 1,000 × 365 × 0.40 = 146,000 booked nights/year
  Average nightly rate ₹4,500  [ASSUMPTION — metro Airbnb rate]
  → GMV ≈ ₹65.7 Cr/year per city

Current model: 12% host commission
  → ₹7.9 Cr/year

Proposed: 9% commission + ₹350 per-booking experience fee
  Bookings/year = 146,000 / 3.2 ≈ 45,600
  Commission:  65.7 Cr × 9%          = ₹5.9 Cr
  Experience:  45,600 × ₹350          = ₹1.60 Cr
  → ₹7.5 Cr/year
```

**The proposal is a revenue decrease of ~5% at these assumptions.** That is the finding v1 didn't surface, and it changes the recommendation: the fee model only wins if it increases bookings by ~6%, which is exactly what the trust ladder is supposed to do. So the revenue redesign should be **gated on** the trust ladder result, not launched alongside it.

That's the decision v1 was avoiding by presenting ingredients without a base.

## Sensitivity, on the two variables that matter

| Variable | Low | Base | High | Effect on the fee-model verdict |
|---|---|---|---|---|
| Average nightly rate | ₹3,000 | ₹4,500 | ₹7,000 | At ₹7,000 the fee model is revenue-neutral; below ₹4,000 it loses ~8% |
| Average stay length | 2.2 nights | 3.2 nights | 4.5 nights | Shorter stays favour the per-booking fee; longer stays favour commission |

The per-booking fee is a bet on **short stays** (weekend trip demand). If Indian metro demand skews to longer family stays, the model is wrong. v1 never stated which way it was betting.
