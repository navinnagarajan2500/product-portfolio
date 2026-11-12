# 10 · PulseReel: fast-mobilising content — v2

**Original submission:** `PulseReel_PRD_Navin_N.pdf` (Oct 2026)
**Mentor score:** 3.3 / 5

## What the mentor said

> "You've built a very careful triage system for content that is *spreading fast*, and you have been honest that you are not determining whether it is *true*. But the viewer never learns that. The label says 'spreading fast', the analyst clears or confirms, and nowhere does the person watching the video find out that the analysis concluded it was false. Walk me through one incident hour by hour and this becomes a strong PRD."

The gap between "we flagged this as fast-moving" and "we concluded this was false" — and the viewer sitting in that gap — is the whole issue.

---

## What changed in v2

1. **An hour-by-hour incident walkthrough** — the mentor's actual request.
2. **A viewer-visible outcome state** — the label now has a terminal state that reaches the viewer.
3. **An explicit statement of what the system does not decide**, kept from v1 but moved from a footnote to the first page, because it's the honesty that made this PRD decent.
4. Removed the assumed stakeholder pains that had `[ASSUMPTION]` tags on all six — if every pain is assumed, the document is a hypothesis list, not a PRD.

---

## The incident, hour by hour

A fabricated claim about a local infrastructure failure, posted at 21:10 IST.

| Time | Event | System state | Human action |
|---|---|---|---|
| 21:10 | Reel posted, 40 views | Below all thresholds | None |
| 21:34 | 12k views in 4 min, 89% non-follower | Velocity signal fires. Risk tier **2**. Enters evidence queue | — |
| 21:36 | Geography: 71% from one state; 4 negative checks pass (no trusted source, no geotag conflict, no prior flag) | Case assembled, tier 2 | — |
| 21:41 | Analyst opens case. Sees velocity chart, geography, 4 negative checks, and related-content cluster (7 similar reels, 3 accounts) | — | Analyst **escalates to Policy**, does not clear |
| 21:44 | Policy lead reviews; no government request; claim unverifiable either way | — | Applies **"Unverified — spreading fast"** label at distribution layer, region-scoped |
| 21:50 | Label live. Reel stays up, reach limited in the affected state | Tier held | — |
| 22:15 | **Local newsroom publishes a debunk** with a source document | New negative check: credible contradiction | Analyst sees alert, reopens case |
| 22:22 | Analyst **confirms the flag** | Case → **Confirmed false** | — |
| 22:24 | **Viewer label changes** from "Unverified — spreading fast" to "This claim was assessed as false. [source]" | Terminal state reaches viewers, including those who already watched | — |
| 02:40 | Government takedown request arrives for a *different* reel citing this one | Override path | Routed to legal, distinct from automated tiers |
| Next day 10:00 | Immutable timeline exported for regulator response | Audit complete | — |

**The 22:24 row is the fix.** v1's PRD ended at "analyst confirms flag" — the flag existed in the system and never reached the person watching. A trust-and-safety system whose output is invisible to its users is a compliance artefact, not a product.

## The viewer-visible state machine

v1 had one label. v2 has four states, and — critically — the label is *sticky*: it follows the content, including for users who already viewed it.

```
UNVERIFIED ──(credible contradiction found)──> CONFIRMED_FALSE
           ──(credible source confirms)──────> CONFIRMED_TRUE
           ──(analyst clears, no evidence)───> CLEARED
```

- Each transition notifies previous viewers **once**, via an in-feed card, not a push (push on a false claim amplifies it).
- `CLEARED` matters as much as `CONFIRMED_FALSE`: the system must be able to say "we flagged this and we were wrong", or creators have no reason to trust it and the fast-lane appeal in v1 is worthless.
- Creator-facing notice names the affected region and what remains visible, which v1 specified correctly.

## What the system does not do (stated up front now)

It **does not determine truth**. It ranks mobilisation risk and routes to humans, who apply a label. Every screen in the analyst tool states this, because an analyst who believes the system is a truth-detector will rubber-stamp its output.

v1 buried this in a scope note. It is now the first paragraph, because it is the design's most important constraint and the reason the human-in-the-loop exists.

## What was cut

Six stakeholder pains, each tagged `[ASSUMPTION]`. In a PRD, that's a tell: it means no one was interviewed. v2 keeps only the two pains that are structurally necessary for the design to make sense (Trust & Safety has no mobilisation-ranked queue; viewers have no distinction between "trending" and "unverified") and drops the rest rather than padding the section to look thorough.

Also cut: the 5-minute appeal SLA for creators. v1 promised a decision in 5 minutes, which the analyst staffing model in the same document could not support at the stated case volume. Replaced with a 4-hour commitment and an expedited path for accounts above a follower threshold — slower, but deliverable.

## What v1 got right

The separation of **mobilisation risk from truth** is genuinely the correct framing for this problem, and the "distinct inspectable safety signal applied without rewriting the ranking system" requirement is exactly how a ranking team would want to be asked. Both are kept, and the second is why the label can ship as a distribution-layer overlay rather than a model change.
