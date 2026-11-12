# 13 · Urban Company capstone — repair-quote verifiability

**Original submission:** `Navin_Product_Capstone_v27.pdf` + `Supporting_Artifacts_Navin_v7.pdf` (Oct 2026)
**Status:** submitted, awaiting mentor evaluation
**Independent re-jury (self-run, 3 mock reviewers):** 78.4 / 100 average; target bar 85

## The problem, in one screen

> One washing machine. Two technicians. Two different faults.
> Technician 1: "The PCB has failed." Evidence shown: none.
> Technician 2: "It's the valve." Evidence shown: none.
> The customer can look up both part prices. Can't tell which claim is true.

That is the strongest problem statement in the portfolio. It is specific, it is sourced (a consumer complaint, cited as a community complaint rather than dressed up as an interview), and it names the exact asymmetry: the price is published, the diagnosis isn't checkable, and the person diagnosing earns more if the expensive answer is true.

**Metric:** resolved visits, 41% → 58%. Resolved = approved, done, 4★+, no dispute in 7 days — *or* an honest "don't repair" that the customer accepts.

That second clause is what makes the metric honest. A system that increases approvals by convincing people to approve is not a success, and the metric refuses to count it as one.

**Personas from real survey data (n=43):** Shown-Proof Approver (approved, could verify), Burned Approver (approved, bill grew — ₹2,500 → ₹4,200), Fee-and-Flee Decliner (₹9,000 compressor vs ₹1,500 fan motor, went local), Never-Platform Household (10 of 43 used a known local technician; one family had used the same one for six years).

## Where it stands at 78.4, not 85

The mock jury's three objections, in order of severity:

1. **The survey is n=43 and self-selected.** It supports the persona taxonomy; it does not support the 41% base rate. The 41% came from the brief `[given]` — which is fine — but the deck sometimes lets the survey imply it.
2. **No comprehension test of the proposed evidence screen.** The design proposes showing "what was tested, the reading vs a healthy unit, why this part and not a cheaper one." Whether a non-technical customer can read a multimeter reading is *the* open question, and the capstone never tested it.
3. **The supply side is assumed cooperative.** Technicians earn commission on parts; asking them to show evidence that may reduce the part they install is asking them to argue against their own pay. The deck acknowledges this once and doesn't resolve it.

## v2: the three fixes

### 1. Survey framing, corrected

Every persona claim in v1 now carries its provenance inline:

- `[S]` survey, n=43, self-selected, recruited from two Urban Company complaint threads and one local WhatsApp group. **Not representative of UC's customer base.** Supports existence of a behaviour, not its frequency.
- `[R]` community complaint, cited with page number.
- `[E]` published rate card / policy, verifiable.
- `[I]` inference.
- `[given]` supplied in the brief.

And one sentence added that v1 lacked: *"The 41% base rate is from the brief. Nothing in this capstone independently measures it, and the survey cannot."*

### 2. The comprehension test, specified

This was the missing piece and it is cheap:

**Protocol.** 8 participants, screened as "has paid for an appliance repair in the last 2 years, not an engineer." Shown three versions of the evidence screen, in random order:
- **A:** raw multimeter reading + healthy-unit reference
- **B:** A plus a one-line plain-language verdict ("this reading means the board is not switching")
- **C:** B plus the price delta between this part and the cheaper alternative

**Questions after each:** (i) What did the technician find? (ii) Would you approve at the quoted price? (iii) What would you ask before deciding?

**Pass condition:** 6 of 8 answer (i) correctly on version B. If A outperforms B, the plain-language layer is wrong and should be cut. If C doesn't move approval confidence, the price-delta element is decoration.

**This costs one week** and it is the difference between a design that reads well in a deck and one that works on a phone in a customer's kitchen.

### 3. The incentive problem, answered instead of noted

v1 notes the commission conflict. v2 makes a call:

**Pay the technician for the diagnosis, not the part.** A flat diagnosis fee (₹150, on top of the ₹299 visit) paid regardless of outcome, plus a reduced parts commission. Cost implication: at ~40k diagnosis visits/month this is ₹60L/month gross, offset if the resolved rate moves as the metric predicts — a 17pp move on 40k visits is ~6,800 additional resolved visits, and at an average repair value of ₹2,800 with UC's margin, that more than covers the fee.

**And a monitor that catches gaming:** if part-attach rate rises while the dispute rate stays flat, the fee has been absorbed as a bonus and the diagnosis is still commission-driven. That is the falsifier. Without it, "we fixed the incentive" is an assertion.

## What's already strong and stays

- The metric definition, including the "honest don't-repair" clause.
- The evidence-first design: *what was tested, the reading vs healthy, why this part, what declining costs.*
- The refusal to claim the problem is bigger than the evidence shows — the complaint is cited as a community complaint, not an interview.
- The 30-day UC Cover warranty and ₹10,000 damage protection framing, which are existing, verifiable commitments and are the right place to anchor trust.

## What the mentor will likely test

The same thing the mock jury did: *"Show me the customer reading the multimeter."* v2's answer is now a one-week protocol with a pass condition, rather than a slide that asserts comprehension.
