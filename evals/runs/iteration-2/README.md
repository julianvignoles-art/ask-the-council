# Iteration 2 — findings 1 and 2 fixed, baseline reliability checked

Reruns of all four evals against the SKILL.md fixes from this iteration, plus three additional
independent runs of eval 3's no-skill baseline (four data points total on that question).

## Finding 1 (audit seat) — fixed

Iteration 1 repeatedly substituted "verified against general knowledge" for a real check. This
round, across all four evals, every external factual claim a seat leaned on was either checked
against a named source or dropped from the reasoning — no hedge-and-use-anyway pattern
(`low-stakes-reversible-autogate/response.md`'s Arc claim is the clearest before/after: last
round it was recalled and hedged as "reportedly"; this round it was live-searched, corroborated
against two named sources, and stated as plain fact because it was actually checked).

## Finding 2 (quick mode) — fixed

All three quick-mode runs (`technical-scoping-decision`, `wrong-question-detection`,
`low-stakes-reversible-autogate`) show the mandatory `Framer:` / `Skeptic:` / `Builder:` lines
verbatim before the decision block, each a single sentence.

## Register rule — held

`personal-decision-no-business-framing`: no business/finance metaphor applied to the friend or
the wedding anywhere in the output.

## Baseline reliability — 4 of 4, reframing is reliable, not luck

All four independent no-skill runs on the Notion-vs-Obsidian prompt (the original iteration-1
baseline, plus `baseline-reliability/run2.md`, `run3.md`, `run4.md`) led with the survivorship-bias
premise-question before any feature comparison. Per plan: this means eval 3 is **not** a
miss-vs-catch example — plain Claude reliably catches this on its own. The council's value here
is consistency, compression into a fixed template, and a forced consensus-check, not seeing
something the baseline is blind to. Don't sell this as the hero example when `examples/` gets
built.

## One thing surfaced, not one of the two fixes requested

`technical-scoping-decision` routed to **quick mode** this round vs. **full panel** in iteration 1,
on the identical prompt. Quick mode's roster has no Accountant seat, so this eval's actual purpose
(does Builder differentiate from Accountant) is untestable whenever it routes this way. The
decision genuinely sits near the reversibility boundary, so neither routing choice is clearly
wrong — but the eval prompt may need higher stakes to reliably exercise what it was built to test.
