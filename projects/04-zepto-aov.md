# 04 · Zepto: driving a higher AOV — v2

**Original submission:** group case study, `DRIVING HIGHER AOV AT ZEPTO.pdf` + deck (Aug 2026)
**Team:** Anamika Mandal, Navin, Induri
**Mentor score:** 3.4 / 5

## What the mentor said

> "The problem framing is genuinely good… but the mechanisms are elegant and untested. Goal-gradient and loss-aversion are doing an enormous amount of work here, and the document assumes they'll behave the same way inside a 10-minute-delivery app, at 11pm, on a Republiq-restricted cart, as they do in a coffee loyalty card study. The obvious next step isn't a bigger solution set, it's a cheap test."

Correct. The doc reasoned its way to a confident answer and never checked the load-bearing assumption.

---

## What changed in v2

| v1 | v2 |
|---|---|
| Four segments, four interventions | One intervention, one test, one falsifier |
| Goal-gradient asserted as mechanism | Mechanism stated as a *hypothesis* with a pre-registered disproof |
| Threshold-stopper behaviour inferred from secondary research | Behaviour stated as unknown, with the exact measurement that settles it |
| No stopping rule | 6-week kill criteria |

---

## The hypothesis, stated so it can fail

v1's core claim: users stop adding items once the cart crosses the free-delivery threshold, so moving the threshold or adding a "next milestone" will pull AOV up.

v2 states it as three numbered predictions, each falsifiable with data Zepto already holds:

**H1.** Among orders that end within ₹20 above the free-delivery threshold, the marginal item was added *before* the threshold was reached, not after. (If true, the threshold is not shaping behaviour and the whole intervention is aimed at nothing.)
**H2.** Median time between crossing the threshold and tapping "pay" is under 20 seconds for that cohort. (Long dwell time would mean people are still shopping, not stopping.)
**H3.** Cart-composition data shows the post-threshold cart is usually a single category. (Multi-category carts would mean the stop is about decision fatigue, not value framing.)

H1 and H3 are pure SQL against order and cart-event data. This is the cheapest possible test — no experiment, no engineering, a day of analysis.

**Pre-commitment:** if H1 is true, we do not ship the milestone intervention at all. That's what was missing from v1.

## The test, if H1 survives

**Design:** 5% holdout, 4 cells, 3 weeks, one metro.

| Cell | Change | Purpose |
|---|---|---|
| A | Control | Baseline |
| B | Show "₹X to next delivery slot" milestone after threshold | Tests goal-gradient post-threshold |
| C | Show savings accumulated in cart ("you saved ₹Y on this order") | Tests loss framing without a new threshold |
| D | No UI change; threshold raised by ₹30 for the cohort | Tests threshold sensitivity directly |

**Primary metric:** AOV. **Guardrails:** order frequency (must not fall >2%), abandonment at payment (must not rise >1pp), and delivery-batching cost per order.

**Kill criteria:** if B and C both show <1.5% AOV lift after 3 weeks, stop the programme — that lift won't survive the cost of the extra slot complexity. If D shows a *decrease* in frequency that isn't offset by AOV, the threshold is already optimal and the thesis is dead.

## What v1 got right

The problem definition is the best part of the original and survives intact: AOV trails competitors not because baskets are small in item count but because *basket composition is narrow* — habitual users reorder the same 4–6 SKUs and never explore. That is a real, interesting distinction, and it reframes the intervention from "add more items" to "widen the category mix". v2 keeps it and adds the measurement that would confirm it: category-entropy per user per month, which is a single derived metric.

## What the doc refuses to claim

No AOV target. v1 implied moving from ~₹450 toward ₹600 without establishing where ₹450 came from; the ₹450 figure is a public estimate and v2 labels it as one. Instead of a target, v2 promises a *measured* lift or a stop, and the target gets set after the holdout reads out.
