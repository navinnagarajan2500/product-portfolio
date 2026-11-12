# 09 · QuickBite: from one city to twelve — v2

**Original submission:** `QuickBite_Navin_N_Final.pdf` (Oct 2026)
**Mentor score:** 4.8 / 5 — the highest score in the portfolio

## What the mentor said

> "This is close to professional quality. The workload separation argument — that three workloads grow at very different rates and only one justifies being pulled apart — is the right call and well evidenced. Two fixes: there are empty brackets in the cost section where numbers should be, and a few targets are written as if measured when they're modelled. Fix those and this is a 5."

Only two defects: an unfinished artefact and a precision-honesty problem. Both are cheap to fix and both are symptoms of writing fast at the end.

---

## What changed in v2

1. **Every bracketed placeholder filled**, with the derivation shown rather than just the number.
2. **Modelled vs measured table** — a new section that states, for each load number, whether it came from the current city's telemetry, extrapolation, or planning assumption.
3. One addition the mentor implied: a **failover drill plan**, because the doc commits to 15–30 seconds of no-new-orders per city during failover, and that number was never tested.

---

## The argument that was right (kept verbatim in substance)

> Users grow 400× (5,000 → 2,000,000). Orders grow 480× (to ~8/sec at dinner peak). Rider location writes grow 1,000× (to ~3,200/sec). Tracking connections grow 1,400×.

Because the workloads diverge by more than an order of magnitude, a uniform "split into microservices" answer would be wrong: it would impose 30–40% operational overhead across fifteen engineers to solve a problem that only applies to one workload. **The correct call is to pull out rider location/tracking only**, and keep orders, menus, and payments in a modular monolith with per-city data partitioning.

That is a judgement, not a pattern, and it's why this scored 4.8. v1 got the hard part right.

## The placeholders, filled

v1's cost section had `₹[ ]` and `[ ] engineers` in several rows. v2 fills them with actual workings:

**Per-city infrastructure (monthly, at 500k orders/month per city):**

| Component | Estimate | Derivation |
|---|---|---|
| App/API compute | ₹1.9 L | 8 orders/sec peak × ~40ms CPU per order × 1.4 headroom, on 4 vCPU nodes at ~₹11k/node |
| Postgres (orders, 1 primary + 1 sync replica per city) | ₹2.6 L | 500k orders/month ≈ 180 GB working set; `db.r6g.xlarge` × 2 per city |
| Redis (menus, sessions, cart cache) | ₹0.7 L | 12 GB hot set, single node + replica |
| Object storage + CDN (menu images) | ₹0.5 L | 40k images/city × 180 KB, ~2.5 TB egress |
| Rider location store (time-series, 30-day retention) | ₹1.1 L | 3,200 writes/sec × 30 days ≈ 8.3B points; downsampled to 1-min resolution → ~280M rows |
| Observability | ₹0.6 L | 15% of compute, standard ratio |
| **Total** | **₹7.4 L/month/city** | **≈ ₹89 L/year/city; ₹10.7 Cr/year across 12 cities** |

v1's empty bracket would have landed somewhere near this; the point is that a cost section with no numbers cannot be reviewed, and a reader is right to assume the author didn't do the work.

## Modelled vs measured

The honest classification, which v1 blurred:

| Number | Value | Status |
|---|---|---|
| Current city order volume | ~50k/month | **Measured** — from current telemetry |
| Dinner-peak orders at target | ~8/sec | **Modelled** — 2M users × 0.35 orders/month × 100% ÷ (2 peak hours × 3,600s) |
| Rider location writes at target | ~3,200/sec | **Modelled** — 40k active riders ÷ 100s ping interval × 8 correction writes |
| Tracking connections | ~1,400× growth | **Modelled** — concurrent viewers ≈ 1.1 × active orders |
| Browse p95 under 300ms | 300ms | **Target** — SLO, not an observation |
| 60-second menu cache freshness | 60s | **Design choice** — bounded by the "sold out within 5 seconds" requirement |

"8 orders/sec" reads like a measurement and is not one. It is a chain of three assumptions and it drives the entire architecture. v2 says so, which is the difference between a 4.8 and a 5.

## What the architecture commits to

- **One leader per city for orders.** Synchronous replica, fail closed. Cost: 15–30 seconds with no new orders in that city during failover. Accepted because duplicate orders and lost payments are worse than a brief outage.
- **Rider location is last-write-wins, no ordering guarantee.** Pins may jump backwards. Accepted because nothing financial depends on it.
- **Discovery is cached for 60 seconds.** Accepted because a sold-out item taking up to 5 seconds to disappear is a known, tolerable error.

Those three trade-offs are the spine of the document and they're all documented as decisions with costs, not as preferences.

## The addition: failover drill

v1 asserted 15–30 seconds of failover without evidence. v2 adds the plan to prove or correct it:

- Quarterly drill: kill the city leader during a synthetic 6 orders/sec load, measure time-to-first-rejected-order and time-to-recovery.
- **If measured failover exceeds 60 seconds**, the per-city leader design is wrong and the fallback is a two-city leader with a global sequence — more expensive, but the availability requirement wins.
- Drills run in a non-production city first. The drill itself is a risk, and v1 didn't acknowledge that operating a failover is a skill the team needs to practise.

## One thing I'd add with more time

The document never addresses what happens when a city *shrinks* — a market exit, a competitor winning, a regulatory block. Twelve simultaneous city launches assumes monotonic growth. A per-city kill switch that can drain and decommission a city in under a day is the operational counterpart to the launch playbook, and without it the twelve-city plan is only half designed.
