# 03 · Uber "Find My Ride" — pickup coordination in Perambalur — v2

**Original submission:** `uber_find_my_ride_report.pdf` + presentation (Aug 2026)
**Mentor score:** 2.5 / 5 — the lowest in the portfolio
**Brief:** Problem discovery and market research for a feature gap, with primary interviews.

## What the mentor said

> "There's a lot of apparatus here — RICE scores, Porter's five forces, wedge and moat and guardrail, 70-20-10, an audit appendix — and very little of it is load-bearing… writing 'Evaluation Target: 5/5 Grade' and a slide addressing mentor feedback into the deliverable makes that explicit. Meanwhile the ₹18 crore figure rests on an 18.5% baseline cancellation rate that appears from nowhere. Strip the frameworks you aren't actually using, keep the Perambalur locations and the gate-timing insight, and let ten honest sentences do the work of thirteen pages."

Every word of that lands. v1 was thirteen pages of proof-of-effort wrapped around one good observation.

---

## What changed in v2

**Deleted entirely:** Porter's five forces, RICE matrix, wedge/moat/guardrail framing, 70-20-10 split, "auditability guarantee" cover page, the mentor-feedback slide, the "Evaluation Target: 5/5" line, the audit appendix.

Each of those was decoration. None of them changed a recommendation. Keeping them made the document longer and the argument weaker, because a reader has to work out which parts are doing something.

**Kept:** the Perambalur field locations, the ten interviews, the gate-timing insight, and the pin-vs-place distinction.

**Rebuilt:** the money.

---

## The insight that survived

In Perambalur's five real pickup clusters — New Bus Stand, Four Roads Junction, the DS Campus gate, Collectorate Complex, and the old bus stand — the pin is not the place. GPS resolves to a building centroid. But the *deeper* finding from the interviews was about **gate timing**, not pin accuracy:

> Riders arrive at the gate they think is obvious. Drivers arrive at the gate that is legal to stop at. In four of five clusters those are different gates, and the difference is only visible at the moment the driver is already committed — mid-traffic, unable to take a call.

Three of ten interviewees described the same sequence: pin looks right, driver calls, both describe landmarks, one of them walks 150m in the wrong direction, and the ride either starts late or gets cancelled by the driver to avoid a fine. That pattern is worth a product.

Everything else in v1 — the market sizing, the competitor benchmarking, the RICE ranking — was scaffolding around these ten sentences.

## The money, rebuilt honestly

**v1:** "1.8M SOM rides/month × ₹200 fare × 5.0% saved rides = ₹18.0 Cr saved monthly GMV," resting on an 18.5% hub cancellation rate with no source.

**v2** starts by admitting the measurement gap and giving a range with a stated base:

```
Base: Uber does not publish Perambalur ride volume. 
Any city-level number is an estimate and is labelled as one.

Estimate construction:
  Perambalur urban population        ~1.5 lakh (Census 2011 projection)
  Ride-hailing trips/person/month     1.2  [ASSUMPTION — from comparable 
                                            Tier-3 town benchmarks, ±50%]
  → ~180,000 rides/month   (range 90k–270k)

Share of rides starting at the five studied clusters: 40% [ASSUMPTION
  from interview self-reports, small n]
  → ~72,000 cluster rides/month

Cancellation at clusters: unknown. Interview-reported, not measured:
  3 of 10 described a cluster cancellation in the last month.
  Use 10% as the planning rate (range 5–20%), explicitly not 18.5%.

Rides recoverable if gate-timing is solved: assume 30% of those cancel-
  lations are timing-related [ASSUMPTION]
  → 72,000 × 10% × 30% = ~2,160 rides/month

Value per recovered ride: ₹200 average fare × 25% take rate = ₹50
  → ~₹1.08 lakh/month contribution, about ₹13 lakh/year

That is the honest number. Not ₹18 crore/month.
```

The v1 figure was off by roughly **three orders of magnitude** because it used a metro-scale SOM against a town of 1.5 lakh people. A reader who checked it would have stopped reading — correctly.

**What this means for the decision:** at ₹13 lakh/year of contribution, this is not a business case. It's a **learning case**. Which is fine, and is the call v2 makes explicitly: run it as a two-cluster pilot with success measured on cancellation rate, not GMV, because the GMV is too small to justify building for. If gate-timing fixes work in Perambalur and in a second town, the mechanism is portable to any Indian tier-3 bus-stand cluster — *that* is the scale story, and it doesn't need a fabricated crore figure to make it.

## The proposal, stripped

1. **Gate Drop** — at booking, rider confirms which gate by photo, chosen from the three gate photos the cluster most often confuses. Driver sees the same photo. Cost: photo upload at cluster level, one-time curation per cluster.
2. **Two-minute call replacement** — a fixed set of four tappable messages ("I'm at the north gate", "I'm at the temple gate", "walking to you", "can't find you") that both sides can send during the 0–7 minute window. Cheap, and directly addresses the language/noise failure the interviews described.

No RICE score. Gate Drop first because it removes the ambiguity at the moment it is created; the messaging layer is the fallback for when the photo still isn't enough.

## Kill criteria

If, over 6 weeks and ≥400 cluster rides, cluster cancellation does not fall by at least 3 percentage points, or the gate-confirmation screen is skipped by more than half of riders, stop. Both are answerable with existing data plus one dashboard field.
