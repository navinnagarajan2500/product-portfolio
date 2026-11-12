# 06 · VitaFit gamification & community challenges PRD — v2

**Original submission:** `VitaFit_PRD_Navin.pdf` (Sep 2026)
**Mentor score:** 2.2 / 5
**Brief:** Write a PRD that communicates a two-feature solution to an engineering and leadership audience.

## What the mentor said

> "This is a PRD shaped document, but it is volume where it should be prioritisation. Two features, three personas, a four-row risk table, five metrics in two places, and no flow diagram of the actual experience — so I can't tell what happens when a user fails a challenge on day 4. The targets (35%→55% retention) have no provenance. In a communication assignment, that's the assignment."

The score is for communication, and the document communicated ambition rather than a decision.

---

## What changed in v2

| v1 | v2 |
|---|---|
| Two features shipped together | One feature first, second gated on the first working |
| Three personas with alliteration | One primary user, defined behaviourally |
| Targets with no origin | Targets marked as hypotheses with the assumption behind each |
| Four-row risk table | Risks converted to two decisions and one monitoring rule |
| No flow | One flow diagram with a real branch on day 4 |

---

## The flow, with the branch that matters

v1 described the system but never the experience. Here is the experience, including the failure path:

```
Day 0  User finishes a session
         └─> points awarded (25) + progress bar moves
              └─> if streak crosses a badge threshold:
                    badge unlock screen, 1 tap to share  [optional]
Day 3  Challenge enrolled (7-day Yoga)
         └─> reminder at user's historical session time
Day 4  User misses a session
         └─> BRANCH A: does the challenge allow a missed day?
               ├─ Yes (7-day challenge, 1 grace day)  → grace day consumed,
               │     user sees "1 of 1 grace days used", challenge alive
               └─ No (30-day challenge)               → challenge marked
                     failed, user offered immediate re-enrolment in a
                     fresh 7-day challenge, badge progress preserved
Day 7  Challenge completed
         └─> badge + points to points balance
         └─> re-enrolment prompt for the same challenge, or a harder one
```

**Branch A is the design.** v1 had no answer to "what happens on day 4", which is the single most likely event in a 7-day challenge — and the moment where retention is won or lost. Whether a challenge forgives a miss is a product decision, and it should be in the PRD, not discovered in sprint.

Decision: **7-day challenges forgive one miss. 30-day challenges do not.** The reasoning is that forgiveness in a short challenge protects momentum, while forgiveness in a long challenge destroys the credibility of the streak. Failed users get an immediate re-enrolment offer rather than a dead end, because a dead end is churn with extra steps.

## Targets, with provenance

v1's table said retention 35%→55%, completion 45%→65%, LTV $45→$75, revenue $2.25M→$3.15M. Every one of those was invented to look like a plan.

v2 keeps two numbers and labels the rest as hypotheses:

| Metric | Value | Status |
|---|---|---|
| Current 14-day retention | 35% | **Given in brief** — treat as fact |
| Session completion | 45% | **Given in brief** |
| 14-day retention target | +6pp (35→41) | **Hypothesis.** Benchmarks for streak mechanics in fitness apps cluster around 4–8pp lifts on D14 retention; taking the low end because this is a v1 with no social graph |
| LTV / revenue | — | **Deleted.** LTV requires a retention curve we don't have and a monetisation model the brief doesn't specify |

The honest framing: the brief's 35% is the only number with a source. Everything else is a bet, and a 20pp jump in two-week retention from a points system is not a bet a serious PM makes in writing. 6pp is defensible; 20pp was theatre.

## Why gamification ships first, not both

v1 launched both features simultaneously and therefore could never learn which one worked. v2:

- **Phase 1 (weeks 1–4):** points + badges only, on session completion. No challenges. Success gate: D14 retention lift of ≥2pp against a 10% holdout.
- **Phase 2 (weeks 5–10):** challenges, only if Phase 1 clears the gate. Challenges are the expensive build (scheduling, instructor tooling, group state) and the one that depends on an engaged user base existing.

If Phase 1 fails, the points system gets one iteration and then the programme stops. That's the kill criterion v1 lacked.

## Risks, converted to decisions

v1's risk table said "users ignore gamification → make rewards generous". That's not a mitigation, it's a hope.

- **Points inflation** → reward catalogue is priced in points that *rise* with the redemption rate; cap monthly redemptions at 8% of active users. Monitored weekly.
- **Challenge abandonment at day 4** → the grace-day branch above, plus re-enrolment. This is designed, not mitigated.
- **Instructor supply** → challenges are created by 5 hand-picked instructors in Phase 2, not self-serve. Self-serve is Phase 3 and only if the format proves out.

## The communication point

The mentor's note was about communication, so: this PRD is one page of flow, one table of two sourced numbers and two hypotheses, three decisions, one gate. A leadership reader can approve or reject it in ninety seconds. That was the assignment.
