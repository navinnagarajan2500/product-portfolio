# 11 · AI Support Ops Assistant — v2

**Original submission:** 8 files — brief, 3 SKILL.md, 2 AGENT.md, escalation rules, source, 81 test cases, AI usage disclosure (Oct 2026)
**Status:** submitted, awaiting mentor evaluation
**Brief:** Map five support capabilities to Skill / Agent / Neither, build each standalone, test independently, no orchestration.

## What the v1 submission already does well

The document opens by telling you what it cannot prove:

> "81 of 81 test cases pass… These show the code does what it was written to do; they do not show model accuracy, because every model step ran on an offline rule-based stand-in (no network). The weakest result is escalation: on a sealed set of 36 synthetic tickets the rules caught 13 of 18 (72.2%) real escalations with 0 of 18 false pages. That is not safe to ship on its own."

That paragraph is the reason this is the most engineering-credible artefact in the portfolio. It separates *tests passing* from *system working*, which almost nobody does.

## The defect it names itself

**13/18 escalation recall, 0/18 false positives.** Zero false pages is excellent. 72.2% recall is a safety problem: 5 real escalations per 36 tickets would not page, and the recall-biased classifier designed to cover the gap has never run against a live model.

## v2: what changes

### 1. The ship gate, stated as a number

v1 says "not safe to ship" without defining safe. v2:

| Gate | Threshold | Why |
|---|---|---|
| Sealed-set escalation recall | ≥ 95% (35/36) | Missing an escalation is a customer-harm event; the cost is asymmetric |
| False pages | ≤ 5% (2/36) | Zero was achieved; 5% is the operational tolerance before analysts start ignoring pages |
| Combined rule + classifier recall | ≥ 95% with classifier on | The rules alone cannot get there; the classifier is mandatory, not a nice-to-have |
| Classifier live-model run | required | v1 never ran it, so the whole component is unproven |

**No ship below 95% recall.** That single sentence converts a vague caveat into a decision.

### 2. Recall-biased classifier: define the bias, don't just name it

v1 calls the classifier "recall-biased" without stating the operating point. v2 makes it explicit: threshold tuned so that recall is ≥95% and precision may fall to ~55%, because a false page costs an analyst 90 seconds and a missed page costs a customer a day. Then it needs a negative control — the classifier must be run on 50 tickets that are definitely *not* escalations, or the "0 false pages" result is unverified on the new path.

### 3. Test corpus, made less circular

81 hand-written tests by the author of the code is a self-assessment. v2 adds:

- **A held-out set written before the code** — 25 tickets from a support-ticket template library, written from the brief's scenarios, never inspected during implementation.
- **An adversarial set of 10** — tickets that *look* like escalations and are not: a refund request that mentions "lawyer" rhetorically, a cancellation with a legal-sounding word, a routine complaint with an angry tone.
- Reported as three columns: authored tests, held-out, adversarial. If adversarial recall collapses, the rules are keyword-matching.

### 4. The "Neither" decision, defended

v1 maps the escalation rule layer to **Neither** (not Skill, not Agent) and says it is "half of capability 1". That is the most interesting judgement in the document, because it resists the temptation to make everything an agent. v2 adds the reasoning explicitly: escalation is a deterministic, auditable policy, and putting it in a model makes it non-deterministic, unauditable, and impossible to appeal. A support system must be able to explain why it paged.

## What stays unchanged

The mapping (3 Skills, 2 Agents, 1 Neither), the no-orchestration constraint, the tool-scope table, the AI-usage disclosure. All correct. The point of a Skill/Agent test is to resist over-agentification, and v1 did that well.

## What the score will hinge on

Likely: whether the escalation gap is treated as a blocker or as a footnote. v1 put it on page one, which is honest but leaves the fix undone. v2's contribution is the ship gate — the difference between "I know this is broken" and "here is the number at which it is no longer broken."
