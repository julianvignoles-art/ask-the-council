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

## If claim-check is installed

Invoke it on the claims identified above. Use its output format and its five statuses
(`CONFIRMED` / `CONTRADICTED` / `PARTIAL` / `UNSUPPORTED` / `JUDGMENT`) as-is — don't reinvent a
parallel classification scheme. Fold the resulting audit table into the council's output ahead of
the Chair's synthesis, and let the Chair's confidence rating reflect what it found (a
`CONTRADICTED` claim a seat leaned on should visibly lower confidence, not get quietly absorbed).

## If claim-check is not installed

Do the same job by hand, inline, without announcing that a dependency is missing or suggesting
the user go install something — that's a distraction from the decision they came here for.
Concretely: for every factual claim a seat leaned on, name the specific source checked (a URL
actually opened, a file actually read) or mark it `UNSUPPORTED`. The same non-negotiable rule
applies here as anywhere else this problem shows up: if you can't name the source, the claim is
unsupported. This inline version does not need claim-check's full five-step procedure — the
panel already extracted and classified the claims by virtue of using them — it only needs the
verification discipline itself, which is trivial to reapply directly.

## What "graceful" means here, precisely

Graceful degradation is not a hedge or a apology in the output. The user reading the Chair's
final recommendation should not be able to tell, from the output alone, whether claim-check was
installed — the audit either happened with the dedicated tool or happened by hand, but it always
happened, and it always shows up as a normal part of the council's output rather than a caveat
about tooling.

## Where this plugs into SKILL.md

This becomes the "audit seat" section of the main procedure, positioned after the panel section
and before the "output format" section. Keep it short in the body — a few sentences pointing at
this file for the "why," since the mechanics here are simple once stated once.
