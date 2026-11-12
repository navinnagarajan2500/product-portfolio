# 05 · Zomato checkout — UX evaluation & redesign — v2

**Original submission:** `UX_Evaluation_Redesign_Complete_Report_NAVIN.pdf` (Sep 2026)
**Mentor score:** 2.4 / 5
**Brief:** Evaluate a real interface against heuristics, then redesign it.

## What the mentor said

> "This reads like an inventory of frameworks rather than an evaluation of an interface. Hick's Law, Fitts' Law, Jakob's Law, Nielsen's ten, the noun-clarification framework, JTBD — all present, and none of them are doing the thing the brief actually asks: looking at the screen and telling me what is wrong with it… The $108M figure is a chain of four unsourced assumptions. Delete it."

The worst mistake in the portfolio, and the most instructive: I never once described what was on the screen.

---

## What changed in v2

**Deleted:** the $108M revenue chain, the "Nielsen heuristics mapped to issues" table, Fitts'/Hick's/Jakob's name-drops, the noun-clarification diagram, the severity matrix, the 60%→75% completion target.

**Added:** eight screen descriptions, each with what is on it, what the user has to do, and where it breaks.

---

## The evaluation, rewritten as observation

v1 issue 5 said "6-step checkout — Flexibility & Efficiency heuristic — structural system friction". That is a category label, not a finding. Here is the actual sequence, walked on Zomato Android, v18.x, September 2026, one order of biryani from a Koramangala restaurant:

**Screen 1 — Cart.** Line items, quantity steppers, coupon field, bill summary collapsed behind a tap, "Proceed" pinned at the bottom. *Observation:* the bill summary is collapsed by default, so the first number a user sees is the item subtotal, not the payable amount. The gap between those two is the bill shock v1 asserted without evidence.

**Screen 2 — Address.** Saved addresses as cards, "Add new address" as the last card, map pin adjustment behind a small "change" link. *Observation:* the address cards show no landmark or delivery instruction, so a user reordering to a flat cannot verify which floor instruction is attached without opening each card.

**Screen 3 — Delivery time.** "Now" preselected, schedule requires a tap and a wheel picker. *Observation:* the wheel picker is the only place in the flow where a mis-tap costs more than one tap to correct, and it's on the path for the minority use case while occupying a full screen for everyone.

**Screen 4 — Coupon/payment combined.** Coupon row at the top, payment methods below, "Place order" pinned. *Observation:* this is where the "6 steps" feeling comes from — it is two decisions on one screen with no visual separation, and the coupon row sits above payment, so the user hits the offer before seeing the total they're about to pay.

**Screen 5 — Processing.** Full-screen interstitial with no progress state and no cancel. *Observation:* if payment stalls (UPI intent timeout is the common failure), the screen gives no recovery path — no "check status", no "try another method". This is the one genuine CRITICAL, and it was in v1 only as a heuristic reference.

**Screen 6 — Confirmation.** Order ID, ETA, a live map, restaurant contact.

That's the whole flow. Five decision surfaces and one dead-end state — not "6 steps vs 3 steps", which was a framing choice v1 made to fit a heuristic.

## The three findings that survive

1. **Collapsed bill summary before the payment screen.** Users commit to a cart without seeing fees and taxes until screen 4. Fix: show payable total on screen 1, with the fee breakdown one tap away. This is testable — show total-up-front to 50% of users and measure back-navigation and abandonment at screen 4.
2. **No recovery state during payment processing.** A stalled UPI intent leaves a full-screen block with no exit. Fix: after 12 seconds, reveal "checking status" plus a cancel path. This is a bug-fix, not a UX improvement, and should not be A/B tested — just shipped.
3. **Delivery instructions invisible on saved-address cards.** Causes failed handoffs and rider calls. Fix: surface the instruction text on the card.

Three findings, three fixes, one of them shipping without an experiment. That is more useful than five findings mapped to five heuristics.

## What I'd measure

- **Screen 1 → 4 back-navigation rate** as the proxy for bill shock. If total-up-front reduces it, the fix works.
- **Payment-screen dwell above 30s** as the proxy for a stalled or confused payment attempt.
- **Rider-initiated calls per 100 orders** for the address fix.

No revenue projection. The relationship between checkout completion and annual revenue involves commission rate, contribution margin, and cannibalisation, and v1 multiplied four assumptions in a row to get a number that looked authoritative and was not. Deleting it made the document stronger, not weaker — a reader can now check every claim by opening the app.

## The one thing worth keeping from v1

The JTBD framing was right, and it survives as a single sentence rather than a section: the user's job is not "complete payment", it is *"turn hunger into satisfaction while remaining certain the order is correct"*. That is why the collapsed bill summary matters — it attacks certainty, not speed.
