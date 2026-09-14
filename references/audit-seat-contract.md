# Audit seat: the claim-check dependency

This is a locked design decision, written before the rest of the skill so the SKILL.md body
built in the next session can drop it in directly. It governs the one place ask-the-council
depends on another skill.

## Where this fires

After the panel speaks and before the Chair synthesizes, run a fact pass over any factual claim
a seat leaned on to make its case — a stat the Accountant cited, a constraint the Specialist
named, a "this always happens" the Skeptic asserted as precedent. Opinions and predictions don't
go through this pass; only the factual claims embedded inside the panel's reasoning do.

## The dependency, and why it must not be load-bearing

`ask-the-council` is a better skill with `claim-check` installed, but it cannot *require* it.
This skill has to work the moment someone clones this repo alone, with nothing else installed —
that's the whole point of shipping it as a standalone public repo rather than bundling it inside
claim-check's. A skill that errors, refuses, or nags the user to go install a dependency first
is worse than one that just does the degraded version of its own job.

So: check once, at the start of the audit pass, whether `claim-check` is available (present in
the skills list). Don't check per-claim, don't re-check mid-panel.

## Exactly two outcomes — no third option

This is the part that failed in practice, so it's stated here without room to read around it.
Every external factual claim a seat leans on ends up in exactly one of two places:

1. **Checked and cited.** A named source backs it — claim-check's own audit, or a source you
   named yourself after actually opening it.
2. **Gone.** Not checked, not usable. The seat's point gets rewritten without it, or (only if the
   point can't survive the rewrite) the Chair's Confidence line names the unverified premise.

There is no third bucket for "plausible," "well known," "as far as I recall," or "verified against
general knowledge." **That last phrase specifically is a failure state, not a pass** — it means a
claim was used without a source, dressed in language that sounds like a check happened. If a
seat's reasoning is about to contain it, the claim it's attached to needs to move to outcome 2.

**A hedge does not rescue a claim into outcome 1.** Labeling something "unverified" or "recalled,
not confirmed live" and then using it anyway in the same paragraph is worse than not labeling it
at all — it reads as diligence while doing exactly what the label warns against. Self-awareness
that a claim is shaky is not the same as not using the claim.

## If claim-check is installed

Invoke it on the claims identified above. Use its output format and its five statuses
(`CONFIRMED` / `CONTRADICTED` / `PARTIAL` / `UNSUPPORTED` / `JUDGMENT`) as-is — don't reinvent a
parallel classification scheme. `CONFIRMED`/`CONTRADICTED`/`PARTIAL` land in outcome 1 (checked);
`UNSUPPORTED` and `JUDGMENT` land in outcome 2 (gone from the reasoning, or explicitly flagged in
Confidence if unavoidable). Let the Chair's confidence rating reflect what it found — a
`CONTRADICTED` claim a seat leaned on should visibly lower confidence, not get quietly absorbed.

## If claim-check is not installed

Do the same job by hand, inline, without announcing that a dependency is missing or suggesting
the user go install something — that's a distraction from the decision they came here for.
Concretely: for every factual claim a seat leaned on, either open a source and name it (outcome
1), or the claim is gone (outcome 2). This inline version does not need claim-check's full
five-step procedure — the panel already extracted and classified the claims by virtue of using
them — it only needs the same two-outcomes discipline applied directly, by hand.

## What "graceful" means here, precisely

Graceful degradation is not a hedge or an apology in the output. The user reading the Chair's
final recommendation should not be able to tell, from the output alone, whether claim-check was
installed — the audit either happened with the dedicated tool or happened by hand, but it always
happened, and it always shows up as a normal part of the council's output rather than a caveat
about tooling.

## Where this plugs into SKILL.md

This becomes the "audit seat" section of the main procedure, positioned after the panel section
and before the "output format" section. Keep it short in the body — a few sentences pointing at
this file for the "why," since the mechanics here are simple once stated once.
