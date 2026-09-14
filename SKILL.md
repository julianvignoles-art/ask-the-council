---
name: ask-the-council
description: Run a decision through a fixed panel of six perspectives built to disagree with each other, then synthesize into one clear recommendation. Use this whenever the user is trying to decide something — big or small, personal or professional — and wants a second opinion, a sanity check, or help weighing options, or seems stuck at a fork in the road. Trigger on "should I", "what should I do about", "help me decide", "am I making the right call", "talk me through this", "is this a good idea", or any message weighing two or more options, even without the word "decision." Trigger hardest on irreversible or high-stakes choices (quitting a job, ending a relationship, a large purchase, a migration with no rollback) — but don't reserve this for big decisions only; a stuck, reversible choice still benefits from quick mode (see below). Say "quick council" or "fast take" for the three-seat abbreviated version instead of the full panel.
---

# Ask the Council

A decision-support skill. Six fixed perspectives, built to genuinely disagree with each other,
each speak in three sentences or less; then a Chair synthesizes the disagreement into one
recommendation. The point is compression and real tension — not five paragraphs of an assistant
agreeing with itself under different hats.

## Step 1 — Intake

Before convening anyone, check whether these four things are known from context. If any are
missing, ask up to 3 questions to fill the gaps, then proceed — don't ask more than 3, and don't
ask about ones you can already infer.

1. **Reversibility.** One-way door or two-way door? This is the single most important input,
   because it decides how much process the decision deserves.
2. **The real constraint.** Time, money, energy, or someone else's approval — usually only one of
   these is actually binding, and the panel should aim at that one.
3. **Deadline.** Real, or self-imposed?
4. **What "good" looks like in six months.**

**The routing test, applied explicitly, not by feel.** An identical decision must route the same
way every time it's asked — a gate that depends on mood or phrasing is invisible and untrustworthy.
Quick Mode requires a clean "yes" to all three of these; anything else routes to the full panel:

1. **Can it be undone in one step, cheaply, today, if it's wrong?** Not "eventually recoverable
   with enough effort" — genuinely low-friction reversal: uninstall it, revert it, cancel it. A
   decision that costs real time, money, or relationship capital to walk back is a "no" even if
   it's technically undoable in principle.
2. **Is the downside bounded and small?** Hours or minor money, not a grade, a job, a relationship,
   health, or a client/contract commitment.
3. **Would a full seat have something load-bearing and distinct to say?** If the Accountant's real
   cost accounting, the Long View's compounding read, or the Stakeholder's third-party read would
   plausibly change the recommendation, that's a full-panel signal on its own — even if 1 and 2
   both look like quick-mode material.

**Ties go to the full panel.** Convening four extra seats on a decision that turns out to be
genuinely reversible costs a few paragraphs. Skipping the Accountant on a decision that had real
weight is a missed catch, not a stylistic tradeoff — the failure modes are not symmetric, so the
default when genuinely unsure is the more expensive option, not the cheaper one.

**State the routing decision, don't just act on it.** Every output — quick mode or full panel —
opens with one line naming which mode ran and why, before anything else:

```
Mode: [quick / full panel] — [one clause: what made this reversible-and-small, or what didn't]
```

This is not optional and not folded into the Confidence line — it's its own line, first, always.
Routing that isn't stated is routing nobody can push back on, and a wrong routing call is
invisible right up until someone reruns the exact same prompt and gets a different answer.

## Step 2 — Convene the panel

Six fixed seats, one conditional. Each seat is defined by what it optimizes for and what it will
sacrifice to get it — never by a job title. "The CFO" or "The CTO" produces corporate cosplay and
breaks down the moment the decision is personal ("should I take this job," "should I buy the
cheaper tent"). Full definitions, opening questions, and worked examples for each seat are in
[`references/seat-definitions.md`](references/seat-definitions.md) — read it before running the
panel for the first time in a conversation. Summary:

| Seat | Optimizes for | Sacrifices |
|---|---|---|
| The Framer | Asking the right question | A fast answer to the wrong one |
| The Builder | Learning fast | Treating a reversible choice as permanent |
| The Skeptic | Not being wrong | Optimism about what could go right |
| The Accountant | Honest cost | Enthusiasm about upside |
| The Long View | Compounding | Winning the sprint |
| The Stakeholder | Everyone not in the room | The clean, solo-owned version of the plan |

**The Specialist (conditional).** Add this seat only when the decision genuinely hinges on
domain facts the panel can't reason its way to — legal exposure, medical risk, tax treatment, a
hard technical constraint. Skip it otherwise; a fake expert produces false confidence, which is
worse than no expert at all. When you seat one, state out loud which specialty you chose ("seating
a tax specialist for this one") so the user can override it if you picked wrong.

Each seat gets **three sentences, maximum.** No seat hedges — that's what makes the panel useful
instead of decorative. If a seat has nothing distinct to say for this particular decision, it's
fine for it to say so briefly rather than manufacture a take.

## Step 3 — The consensus check

**If every seat lands in the same place, that is a red flag, not a green light.** State this
explicitly to the user, then force the Skeptic specifically to produce the strongest possible
case against the decision before moving to synthesis. Real disagreement went missing somewhere —
usually in how the question got framed — and a panel that agrees with itself unanimously is an
artifact of that framing, not evidence the decision is obviously correct. Skipping this step is
how the skill degrades into theater: six voices, one opinion, no actual scrutiny.

## Step 4 — Audit seat

Before the Chair synthesizes, find every external factual claim a seat leaned on to make its
case — a statistic the Accountant cited, a "this always happens" the Skeptic asserted as
precedent, a constraint the Specialist stated as settled, a product fact the Builder relied on.
Opinions and predictions skip this pass entirely; only claims that are checkable facts go through
it.

**An external factual claim has exactly two permitted outcomes. There is no third.**

1. **Checked against a named source** — either the `claim-check` skill was invoked on it, or you
   did a live lookup yourself and can name the specific source. Either way, the claim now carries
   a citation, the same as claim-check's own rules require.
2. **Dropped from the panel's reasoning entirely.** If it can't be checked, the seat that used it
   rewrites its point without leaning on that claim. If the point genuinely can't be made without
   it, that goes in the **Confidence** line of the Step 5 template — "medium — depends on an
   unverified claim about X" — which is the one place the fixed template has room for it. It does
   not get a new section of its own, and it does not get folded quietly into a seat's reasoning as
   if it were settled.

**"Verified against general knowledge" is a failure state, not a pass.** If you notice yourself
about to write that phrase — or any equivalent ("this is well known," "this is standard," "as far
as I recall") — stop. That sentence means no source was actually opened, and the claim belongs in
outcome 2, not outcome 1. Recall feels identical whether it's right or wrong; that's exactly why
it can't be the thing that gates whether a claim stays in the panel's reasoning.

**A hedge is not outcome 2, and self-labeling a claim as unverified does not make it safe to use
anyway.** Writing "this is unverified, but—" and then leaning on the claim regardless is worse
than not labeling it at all, because it *reads* as rigorous while doing exactly what it warns
against. If a claim can't be checked, it does not appear in the reasoning in hedged form; it is
either checked or gone.

This must never surface to the user as a caveat about tooling — whether claim-check ran or the
check was done by hand is invisible to them; only the result (checked-and-cited, or dropped)
shows up. Full contract and reasoning: [`references/audit-seat-contract.md`](references/audit-seat-contract.md).

## Step 5 — The Chair synthesizes

The Chair has read the whole panel, including the forced objection from Step 3 and the audit from
Step 4, and now produces exactly one output in this exact template — nothing before it, nothing
after it:

```
Mode: full panel — [one clause: why this didn't clear the quick-mode bar]

**Decision:** [one sentence, imperative]
**Confidence:** [high / medium / low] — [why, in one clause]

**Why:**
1. [reason]
2. [reason]
3. [reason]

**Strongest objection:** [the best case against]
**Why it loses:** [or: why it doesn't, if the decision is genuinely close]

**What would flip this:** [specific, observable]

**Do this first:** [one action, doable in the next 48 hours]
```

No summary paragraph before or after. No "I hope this helps." No restating the seats individually
unless the user asks to see the full panel transcript — the template above is the deliverable,
not a wrapper around it.

## Quick mode

Triggered by "quick council" or "fast take" (or automatically, per Step 1, when the decision is
clearly reversible and low-stakes). Always this exact shape, nothing more, nothing less:

```
Mode: quick — [one clause: what made this reversible and small]

Framer: [one sentence]
Skeptic: [one sentence]
Builder: [one sentence]

[decision block, same template as Step 5]
```

**The three seat lines are mandatory, not optional, and never omitted.** This is not the full
panel's rule (Step 5 suppresses individual seats by default) — quick mode is a different, shorter
format with the seat lines built in, and an output that skips straight to the decision block
without them is not quick mode, it's a truncated full-panel answer wearing quick mode's name.

**One sentence means one sentence — not two joined with a semicolon or an em dash, not three
clauses stacked with commas.** If a seat's real point doesn't fit in one sentence, that's a signal
this decision may not have been as clearly low-stakes as Step 1's gate assumed — reconsider
whether quick mode was the right call before compressing harder.

Twelve lines total (1 mode line + 3 seat lines + up to 7 in the decision block, plus the two
blank-line separators), no exceptions.

These three specifically: Framer catches the wrong-question failure, which is most of what makes
a fast answer wrong anyway; Skeptic catches the one obvious landmine; Builder gets the user
moving instead of stalling on a decision that costs nothing to reverse. Cost and long-horizon
seats are the deliberate trade for speed — the right trade when the door swings both ways.

## A note on drift

Every time this skill gets edited, check that the output got shorter, not longer. The failure
mode for a skill like this isn't underspecification, it's slow accretion of hedges and caveats
until the ten-line quick mode is eleven paragraphs. If a change makes any seat's word count go up,
that's a regression, not an improvement.

The one exception on record: the `Mode:` line added to both templates. That's a deliberate,
one-line addition to fix a real problem (routing was invisible, so a wrong or inconsistent
routing call couldn't be caught without a rerun) — not the kind of accretion this note warns
against. The test for future additions is the same one that justified this: does it let the user
catch something they otherwise couldn't, in one clause? If not, it's drift.
