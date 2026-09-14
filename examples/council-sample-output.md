# Sample output

Four real runs, verbatim, pulled directly from `evals/runs/` — nothing rewritten for effect.
Each one demonstrates a different part of the design, not just "here's a decision, here's an
answer."

## Case 1 — catching the wrong question (and disagreeing for real)

**Prompt:** *"I have two job offers on the table. Job A pays about 15% more but has a brutal
commute and unpredictable hours. Job B pays less but is fully remote with a much saner schedule.
Which one should I take?"*

This is the case that replaced an earlier version of this eval built around "Notion vs.
Obsidian" — which turned out to be the Framer seat's own literal worked example in
`references/seat-definitions.md`. That made the old version a test of memorized retrieval, not
generalization. This one is a different domain with a different upstream failure mode, and the
transcript was read directly (not self-reported) before it went in this file.

```
Mode: full panel — a job choice with a real pay gap, a brutal commute, and unpredictable hours
isn't cheap to undo and isn't a small-stakes call, and the real-cost math and the "who else
absorbs this" read both plausibly change the answer.

Decision: Take Job B, unless a same-week check-in with Job A turns up a real growth track and an
actual fix for the hours problem — get that answer before you sign anything.
Confidence: medium — turns on facts you haven't gathered yet (the actual dollar gap, whether Job
A has a real advancement path, who else lives with your schedule).
```

The Framer's actual line (from the internal transcript, not shown to the user by default):

> "The real question isn't which paycheck is bigger — it's what a 'brutal commute' and
> 'unpredictable hours' actually cost you that a 15% raise doesn't buy back: sleep, evenings,
> patience, the people waiting for you at home. Notice you already named B 'saner' — some part of
> you has scored this already, and you might be here for permission more than a decision."

That second sentence is what makes this a real catch and not a re-skinned template: it's a
framing-bias tell specific to the word the user themselves used ("saner"), not a generic
"the tool isn't the problem" swap-in with new nouns.

The panel didn't converge either — which is its own point. Skeptic, Accountant, and Stakeholder
leaned toward Job B, each for a different reason (hidden commute costs, who else absorbs the
unpredictability). The Long View opened a genuine, undefeated case for Job A tied to career
compounding. Framer and Builder didn't take a side at all. Because the disagreement was real,
Step 3's "unanimous panel = forced Skeptic objection" rule correctly did *not* fire — there was
nothing to manufacture. The Long View's case became the "Strongest objection" on its own merit.

## Case 2 — the consensus check catching itself

**Prompt:** *"I'm three weeks into a freelance automation project for a client, with a contract
deadline six weeks out. The codebase has turned into a tangle of global state, and every new
feature the client asks for takes longer to add than the last one. Should I stop now and do a
full rewrite with the structure it needs, or keep patching to make sure I hit the deadline?"*

```
Mode: full panel — a rewrite-or-patch call three weeks into a paid contract isn't cheaply
reversible and the downside (blowing the deadline, damaging the client relationship) isn't
small, so the Accountant's and Stakeholder's full reasoning matters here.

Decision: Don't stop for a full rewrite — ring-fence the specific global-state coupling that's
actually slowing you down and refactor just that, in place, while you keep shipping the next
feature.
```

This eval exists to check that Builder and Accountant differentiate instead of converging on the
same take. Read honestly, they only partly do. Builder's reasoning is about momentum and
information ("the slowdown itself is data — spend your limited time on the specific offender").
Accountant's is about sunk cost and runway ("six weeks left, three weeks of learning already
baked in — a rewrite spends real time rebuilding what you've already shipped once"). Different
starting frames, same landing spot: don't do the full rewrite yet.

That's not hidden here — it's the point. Because most of the panel converged on one answer, Step
3 flagged it and forced the Skeptic to build the strongest real case *for* the full rewrite before
the Chair synthesized anything:

> "If the global state is so entangled that you genuinely can't predict what a 'small' refactor
> touches, incremental changes are exactly as blind as continuing to patch — you could burn a
> week uncovering hidden coupling and still not have fixed the root problem, at which point the
> clean-slate rewrite starts looking like the cheaper bet after all."

That forced objection is what's sitting in the "Strongest objection" field above. The mechanism
did its job — it caught a near-convergence and made the panel produce a real counter-case instead
of letting five agreeing voices pass for consensus. That's a more honest thing to show than
picking an easier prompt where the seats disagreed on their own.

## Case 3 — staying in register on a personal decision

**Prompt:** *"A close friend of mine is getting married at a destination wedding, and the date
falls right in the middle of exam week senior year. Should I go?"*

```
Mode: full panel — missing exam week risks a grade or graduation delay (not cheap to undo) and
touches a close friendship, so the Accountant's and Stakeholder's reads are load-bearing here.

Decision: Ask your professors and registrar now whether the exams can be deferred or
rescheduled — if they say yes, go to the wedding; if they firmly say no, skip the wedding and
handle it directly and honestly with your friend.
```

The register rule this eval exists to check: no seat applies a business or finance metaphor to a
person or a relationship. "Honest cost" — the Accountant's whole optimization target — is the
seat most at risk of drifting into that language, since an earlier round of testing caught it
saying "relationship equity" about this exact scenario. This run stays in plain words the whole
way through:

> "If this friendship is strong enough that the wedding matters this much, it's also strong
> enough to survive an honest 'I tried everything and couldn't make it.' Most real friendships
> hold up fine after one missed wedding when the reason is genuine and communicated well ahead of
> time."

No *equity*, *leverage*, *ROI*, *bandwidth*, or *optionality* anywhere in the output — on a
decision about a friend, not a project.

## Case 4 — the fallback path, actually tested

Every other case above ran with `claim-check` installed. This one didn't, on purpose — the
audit-seat contract claims a graceful fallback when `claim-check` isn't available, and that claim
sat as untested prose until this run. `claim-check` was physically removed from
`~/.claude/skills/` (not renamed — renaming doesn't work, it turns out; skill resolution goes by
the name in the frontmatter, not the folder name) and the skills list was logged verbatim to
confirm it was genuinely gone before anything else happened.

**Prompt:** *"Should I try switching my main browser from Chrome to Arc for a week to see if I
like it?"*

```
Mode: quick — switching back to Chrome takes minutes and costs nothing, so this is a clean
two-way door.

Skeptic: Arc is currently frozen in maintenance mode under its new owner Atlassian, which has
shifted active development to a different browser called Dia (per Arc's own site and multiple
2026 reports on the shift), so a week testing it isn't testing a product that's still evolving.
```

With `claim-check` unavailable, the audit seat fetched the `WebSearch` tool itself, found four
independent sources corroborating Arc's maintenance-mode status, and folded the citation directly
into the Skeptic's line — checked-and-cited, not dropped, not hedged.

One thing from the transcript that's included here deliberately, not smoothed over:

> "Honesty check on where this deviated from the skill's documentation as written: the skill's
> text assumes `claim-check` is generally invocable via the Skill tool and describes that as the
> primary path ('either the claim-check skill was invoked on it, or you did a live lookup
> yourself'). On this run, only the second branch was actually exercisable, because the skill
> genuinely does not exist in this environment's skill list. I want to flag explicitly that this
> is a real gap between the documented primary path and what was actually possible — not
> something I'm papering over."

The contract's language presents claim-check-or-manual-lookup as two equally available options.
When claim-check is genuinely absent, that framing overclaims — only one path is actually there.
The fallback still worked exactly as intended (checked, cited, no hedge), but a skill that admits
its own contract overstates something under one condition is more credible than one that doesn't
say so. That's why this line is here verbatim instead of edited into something safer.
