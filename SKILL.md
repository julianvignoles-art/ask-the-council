---
name: ask-the-council
description: Run a decision through a fixed panel of six perspectives built to disagree with each other, then synthesize the disagreement into one clear recommendation. Use this whenever the user is trying to decide something — big or small, personal or professional — and wants a second opinion, a sanity check, help weighing options, or just seems stuck at a fork in the road. Trigger on phrasings like "should I", "what should I do about", "help me decide", "am I making the right call", "talk me through this", "is this a good idea", or any message that lays out two or more options and asks which to pick, even if the user never says the word "decision." Trigger especially hard on irreversible or high-stakes choices (quitting a job, ending a relationship, a large purchase, a migration with no rollback) — but don't reserve this only for big decisions; a stuck, reversible choice still benefits from quick mode (see below). Say "quick council" or "fast take" to request the three-seat abbreviated version instead of the full panel.
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

**If the decision is clearly reversible and low-stakes, skip straight to Quick Mode.** Running
the full panel on "should I try the other coffee shop" is its own failure — an 800-word writeup
for a decision that needed ten seconds is exactly the kind of ceremony this skill should never
produce. Reversibility is the gate; use it.

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

Before the Chair synthesizes, run a fact pass over any factual claim a seat leaned on to make its
case — a statistic the Accountant cited, a "this always happens" the Skeptic asserted as
precedent, a constraint the Specialist stated as settled. Opinions and predictions skip this
pass; only the factual claims embedded in the panel's reasoning go through it.

If the `claim-check` skill is installed, invoke it on those claims and use its output format and
five statuses directly. If it isn't installed, do the same job by hand: for each factual claim a
seat leaned on, name the specific source checked or mark it `UNSUPPORTED` — the verification
discipline is what matters, not which tool applies it. Either way this must never surface to the
user as a caveat about tooling; the audit happens, and it just shows up as a normal part of the
output. Full contract and reasoning: [`references/audit-seat-contract.md`](references/audit-seat-contract.md).

## Step 5 — The Chair synthesizes

The Chair has read the whole panel, including the forced objection from Step 3 and the audit from
Step 4, and now produces exactly one output in this exact template — nothing before it, nothing
after it:

```
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
clearly reversible and low-stakes). Three seats only — **Framer, Skeptic, Builder** — one
sentence each. Then the same decision block as above. Ten lines total, no exceptions.

These three specifically: Framer catches the wrong-question failure, which is most of what makes
a fast answer wrong anyway; Skeptic catches the one obvious landmine; Builder gets the user
moving instead of stalling on a decision that costs nothing to reverse. Cost and long-horizon
seats are the deliberate trade for speed — the right trade when the door swings both ways.

## A note on drift

Every time this skill gets edited, check that the output got shorter, not longer. The failure
mode for a skill like this isn't underspecification, it's slow accretion of hedges and caveats
until the ten-line quick mode is eleven paragraphs. If a change makes any seat's word count go up,
that's a regression, not an improvement.
