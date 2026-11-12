# Product Portfolio — Navin N

PM case work from the **Airtribe AI-First Product Management** program (Cohort 39, Jul–Oct 2026), rebuilt after mentor review.

Every project below was submitted, graded, and critiqued by a mentor. This repo holds the **v2 rebuild** of each one: same problem, same research, but with the specific defect the mentor named fixed. Original grades are shown so you can see what the critique was reacting to — the point isn't to hide a 2.2, it's to show what changed after being told about it.

**Source of truth for the critique:** each project's mentor evaluation on Airtribe. **These rebuilds have not been re-graded** — a mentor score can only change when the mentor re-evaluates.

## What the mentor kept telling me

Across thirteen submissions the same three failures repeat, and the v2s are organised around fixing them:

| Pattern | How it showed up | Fix applied in v2 |
|---|---|---|
| **Unauditable numbers** | "rests on numbers I can't check", "made-up numbers written as data", "₹18 crore from a baseline that appears from nowhere" | Every figure now carries a source, a derivation, or an explicit `[ASSUMPTION]` tag. Assumption ledgers added. |
| **Framework inventory instead of thinking** | "eighteen named frameworks… very little of it load-bearing", "strip the frameworks you aren't actually using" | Named frameworks removed unless they changed a decision. Each doc keeps only the one or two that did work. |
| **No closing decision** | "nothing gets cut, no experiment can stop, no percentage has a base underneath it" | Each project now ends in a decision: kill criteria, stop rules, a budget with a base, and what would prove me wrong. |

Two more, project-specific: **unfinished artefacts** (empty brackets, targets presented as measurements) and **no primary evidence** where six conversations would have settled it.

## The projects

| # | Project | Original grade | What the mentor flagged | v2 |
|---|---|---|---|---|
| 01 | [Nykaa skincare UX funnel audit](projects/01-nykaa-ux-audit.md) | 3.5 / 5 | Strategy strong, evidence unverifiable — "walk me through 5 of those 400 reviews" | Tagged-evidence appendix, sourced competitor claims, sampling method |
| 02 | [B2B AI customer-ops strategy](projects/02-b2b-ai-customer-ops.md) | 3.2 / 5 | Took the textbook-safe call every time; didn't ask if Zendesk could copy the moat | Segment cut to a falsifiable band; direct answer on incumbent copying |
| 03 | [Uber Find My Ride (pickup coordination)](projects/03-uber-find-my-ride.md) | 2.5 / 5 | Apparatus over argument; ₹18 Cr from an invented baseline; wrote "target 5/5" into the deck | Frameworks stripped, GMV rebuilt from a stated base with sensitivity, gate-timing insight kept |
| 04 | [Zepto: raising AOV](projects/04-zepto-aov.md) | 3.4 / 5 | Elegant, untested; goal-gradient doing all the work | Cheap validation protocol and a falsification test |
| 05 | [Zomato checkout UX evaluation & redesign](projects/05-zomato-checkout-ux.md) | 2.4 / 5 | Framework inventory over an interface never shown; the $108M chain | Screen-by-screen observations replacing the framework wall; revenue chain deleted |
| 06 | [VitaFit gamification & challenges PRD](projects/06-vitafit-gamification.md) | 2.2 / 5 | Volume instead of prioritisation; no flow diagram; invented targets | One flow with a real branch, target provenance, risk table cut |
| 07 | [Zomato Tier-1 funnel & retention strategy](projects/07-zomato-tier1-growth.md) | 3.2 / 5 | Numbers contradict each other; assumptions presented as data | Assumption ledger and reconciled arithmetic |
| 08 | [Airbnb India product-led growth](projects/08-airbnb-plg.md) | 4.1 / 5 ★ | Reasoning without decisions — nothing gets cut, no experiment stops | Kill criteria, budgets with a base, funded-experiment portfolio |
| 09 | [QuickBite: one city to twelve](projects/09-quickbite-system-design.md) | 4.8 / 5 | Unfinished brackets, targets marked as measurements | Closed artefacts, explicit modelled-vs-measured table |
| 10 | [PulseReel: fast-mobilising content](projects/10-pulsereel-content-response.md) | 3.3 / 5 | The system never checks whether a claim is true; viewer never learns it isn't | Hour-by-hour incident walkthrough and viewer-visible signal |
| 11 | [AI Support Ops Assistant](projects/11-ai-support-ops.md) | Submitted, awaiting evaluation | — | Evaluation framework, escalation rules, test corpus |
| 12 | [Crumb & Craft (agentic AI)](projects/12-crumb-and-craft.md) | Submitted, awaiting evaluation | — | Agent design, guardrails, evaluation |
| 13 | [Urban Company capstone](projects/13-urban-company-capstone.md) | Submitted — independent re-jury 78.4/100 | Short of the 85 bar; interviews and comprehension tests still pending | Research plan closed, comprehension-test protocol |

★ marked "noteworthy" by the mentor.

## Reading order

If you have five minutes: **08 (Airbnb PLG)** and **09 (QuickBite)** are the strongest thinking. **03** and **05** are the most instructive — the two lowest scores, and the clearest examples of what happens when frameworks substitute for evidence.

## Note on scope

These are training projects, not commercial launches. Market figures are public estimates or reasoned assumptions, labelled as such. Where a number came from a real dataset it is cited; where it did not, it says so.
