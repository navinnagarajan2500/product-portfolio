# 02 · B2B AI customer-operations strategy — v2

**Original submission:** `b2b_product_strategy_report.pdf` + `b2b_presentation_slides.pdf` (Jul 2026)
**Mentor score:** 3.2 / 5
**Brief:** Take a point-solution chatbot and design a land-and-expand strategy: target segment, core problem, moat, bet sizing.

## What the mentor said

> "Whenever a specific, falsifiable call is available, you take the safer, textbook-correct version instead… The moat section names Zendesk and Salesforce without asking whether they could copy the fine-tuning loop using data they already own. Pick one dimension and make the call you're currently avoiding."

The 35% threshold, the $8–$15 ticket cost and the 15-minute setup were the strongest parts. Everything around them was consensus.

---

## What changed in v2

| v1 | v2 |
|---|---|
| Segment: "mid-sized B2C & B2B, 200–1,000 employees" | Segment cut to a named band with a disqualifier |
| Moat: "data advantages and integration moats" | A specific answer to *can Zendesk copy this in 18 months?* — and the bet that they won't, with reasoning |
| Avoid list: obvious non-buyers | The list now includes a segment that looks attractive and is explicitly refused |
| One risk-free recommendation | One falsifiable call where I could be wrong |

---

## The call I was avoiding

**v1:** target 200–1,000 employee companies, 5,000–30,000 tickets/month, Zendesk/Salesforce/HubSpot installed.

**v2:** target **300–800 employee companies on Zendesk, with 8–20 agents, in e-commerce or fintech, that have already hired an AI vendor and cancelled**. Disqualify everyone else for the first two quarters.

That is deliberately narrow, and narrower than the brief's band. The reasoning:

- They have an installed helpdesk, so integration cost is low and the data is already structured.
- They have proven willingness to buy AI support *and* a specific, articulated reason the last attempt failed — which is the best sales opening that exists in this category.
- At 8–20 agents the buyer is a Support Director who feels the pain personally. At 50+ agents the buyer is a VP running a procurement process; at under 8 agents there is no budget line.

**How I could be wrong:** if churned-AI buyers turn out to be mostly *sour on the category* rather than sour on a specific tool, this segment is a graveyard and the safe band was right. The first five discovery calls decide it. Test: ask what they'd need to see to try again. If the answer is "nothing, we're done with AI", the segment is dead and I've lost two weeks, not two quarters.

## Refusing an attractive segment

v1's avoid list excluded solo founders and enterprises — nobody was going to argue. v2 adds: **Indian mid-market BPOs providing outsourced support**. They have the largest ticket volumes and the clearest cost-per-ticket maths, which makes them look like the perfect beachhead. They are refused because their business model is headcount arbitrage: a tool that deflects 40% of tickets destroys their revenue line, so the buyer's incentive is to pilot forever and never expand. Good logo, bad expansion.

## The moat question, answered directly

**Can Zendesk or Salesforce copy this using data they already own?**

Partly, and that's the point. They can copy *classification* — they have ticket corpora. They have a much harder time copying three things:

1. **Write access across systems they don't own.** Resolution requires writing to Stripe, Okta, the order DB, the CRM. Zendesk's incentive is to keep actions inside Zendesk; every external write is a reason to leave Zendesk.
2. **The failure corpus.** The valuable data isn't successful tickets, it's the 5–8% of cases where an automated action was wrong and got reversed. That data only exists if you are executing actions. An incumbent reselling a chatbot doesn't generate it.
3. **The accountability surface.** Enterprises buying automated *actions* (refunds, cancellations) need an audit log and a human-approval path per action type. Building this is unglamorous and slow — which is why an incumbent with a roadmap full of AI features will do it late.

**The bet, stated plainly:** incumbents will ship AI *assist* features (suggested replies, summarisation) because those are safe and demo well, and will lag on *execution* because execution carries liability. If I'm wrong and Zendesk ships cross-system write access with approvals within 18 months, this wedge closes and the company is a feature.

## Bet sizing, kept from v1 but now bounded

70% on the execution path for the churned-AI segment · 20% on the failure corpus and audit log · 10% on adjacency research (billing disputes, which is the highest-volume action class we saw).

Each bet gets a 90-day gate: 70% must produce 5 design partners executing ≥3 action types; 20% must show reversal-rate instrumentation working on live traffic; 10% is research only, no gate.

## What v1 was right about

The unit economics hold: at 10,000 tickets/month and $8–$15 cost per ticket, deflecting 35% returns $28k–$63k/month against a price that can comfortably sit at a fifth of that. That maths is why the segment can be this narrow and still be a business.
