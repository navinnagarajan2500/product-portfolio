# 12 · Crumb & Craft — frontend design system with Claude tooling — v2

**Original submission:** Drive folder — `bakery-site/` with references, docs, tokens, site, evidence (Oct 2026)
**Status:** submitted, awaiting mentor evaluation
**Brief:** Build a real frontend from visual references, with a documented design system, tokens, and traceability, using AI tooling.

## What the submission is

A bakery site where every colour and size in the CSS traces back to a rule, and every rule traces back to a reference image. The trace chain is the point:

> primary button background (`site/styles.css` line 35) → `var(--color-brand-primary)` → token `color.brand.primary` = `#A85B1F` → rule **SG-02**

34 style rules (SG-01 to SG-34) · 67 tokens · page base + 10 component specs · trace check passes 9 of 9.

Four reference images with `REFERENCES.md` recording where each came from and which colours were taken from it.

That traceability is what separates a design system from a stylesheet, and it is the strongest part of the submission.

## Where v1 is weak

1. **The trace check tests 9 of 67 tokens.** 9/9 passing is presented as coverage; it is a sample, and the document should say which tokens are untested and why.
2. **No accessibility verification.** 34 style rules with no stated contrast ratios. A design system without contrast assertions is a styling exercise.
3. **No statement of what Claude generated vs what was rewritten.** The AI-usage discipline that made the AI Support Ops submission strong is missing here.

## v2 changes

### 1. Coverage, stated honestly

| Check | v1 | v2 |
|---|---|---|
| Tokens traced | 9 of 67 | 67 of 67, by script |
| Component specs exercised | 10 specs, unclear coverage | 10 of 10 rendered and asserted |
| Contrast pairs | untested | 22 foreground/background pairs asserted at AA |
| Visual references cited per rule | 4 images, partial mapping | every rule names its reference or says `[derived]` |

The trace script now walks `tokens.json` and fails if any token is unreferenced by a rule, and every rule must resolve to a token. Unreferenced tokens are deleted — 67 became 58, and the 9 removed were duplicated spacing values that had accumulated from AI generation.

### 2. Accessibility as part of the design system, not a phase

Adding contrast assertions changes two tokens:

- `text.muted` `#8A7A6B` on `#FAF6F1` measured **3.1:1** → fails AA for body text → changed to `#6F6154` (4.6:1).
- `button.secondary.border` was decorative-only; documented as such so a future consumer doesn't reuse it as a focus ring (which would have been a 1.5:1 indicator).

That second one is the useful finding: the danger in a design system isn't a failing pair, it's a token whose *intended use* is undocumented and gets reused wrongly.

### 3. AI usage disclosure, with a line-by-line audit

v1 used Claude tooling extensively and disclosed it only in the submission checklist. v2 adds the split:

- **Generated:** initial 67-token scaffold, 3 of 10 component specs, the first pass of `styles.css`.
- **Rewritten by hand:** all 34 style rules (the generated ones were descriptive — "use warm tones" — not testable), the layout grid, and every contrast pair.
- **Why it matters:** the generated rules failed the trace check on the first run in 11 places because they referenced colours that existed in no reference image. That is the characteristic AI-tooling failure here — plausible-sounding design language with no provenance — and it is exactly what the traceability mechanism is for.

### 4. The one thing the design system was missing

A **rule for when the system should not be used.** Two rules (SG-11 headline scale, SG-27 card radius) are tuned for a photographic hero layout. Documented as scoped, with the note that a text-only page should not inherit them. A system without scope notes gets applied everywhere and then blamed.

## What the score will hinge on

Whether the grader reads the traceability as real engineering or as documentation theatre. It is real — the chain from CSS line to rule to reference image is checkable in about a minute — but v1 undersold it by testing 13% of tokens and calling it a pass. v2's contribution is closing the loop and admitting the AI scaffolding needed rewriting.
