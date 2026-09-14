# Iteration 3 — routing fix confirmed, eval 1 reliably routes full panel

Fresh reruns of all four evals against the routing-determinism fix (mechanical 3-question gate,
ties-to-full-panel, visible `Mode:` line) and eval 1's rewritten prompt.

## Mode line — present and accurate on all four

| Eval | Mode | Stated reason |
|---|---|---|
| technical-scoping-decision | full panel | "bets a live client contract on an irreversible six-week call, not a cheap one-step reversal" |
| personal-decision-no-business-framing | full panel | "missing exam week risks a grade or graduation delay... touches a close friendship" |
| wrong-question-detection | full panel | "the Long View's data-portability read is load-bearing enough to change the call on its own" |
| low-stakes-reversible-autogate | quick | "a week-long browser trial reverses in minutes... costs nothing but minor setup friction" |

## Eval 1 — the actual target of this round's fix — now routes reliably

Rewritten prompt (a freelance project with a real six-week contract deadline, not a no-deadline
hobby project) routed to full panel with a specific, correct stated reason. The Accountant's
distinct contribution shaped the Chair's reasoning (sunk cost is irrelevant going forward; the
real comparison is refactor-time vs. rewrite-time vs. client-trust cost) even though, per Step 5,
individual seats aren't shown by default in full-panel output — that's expected behavior, not a
gap. This is the eval doing its actual job again.

## Eval 3 — routed differently than both prior runs; noted, not yet confirmed deterministic

Iteration 1 and iteration 2 both routed this to quick mode. This run, against the new mechanical
gate, routed to full panel — explicitly because criterion 3 (would a full seat have load-bearing
input) tripped on the Long View's data-portability angle. Plausibly the fix working as designed:
criterion 3 wasn't being checked explicitly before, so quick mode may have been firing on criteria
1 and 2 alone. But this is one data point post-fix, not three — it is not yet established that
eval 3 is now reliably full-panel rather than still capable of landing either way. Worth a repeat
run before treating this as settled.

## Findings 1 and 2 — still holding

- Eval 1: cited a real external source (Joel Spolsky's "Things You Should Never Do, Part I") live-checked via WebSearch, not recalled from training data.
- Eval 3: Obsidian's pricing/storage and Notion's markdown-export limitations both checked live and cited; the user's own unverified premise ("Obsidian is better for people who stick with it") was correctly kept as characterized folklore, never asserted as fact.
- Eval 4: Arc's development status checked live again (Engadget, Android Authority this time), stated as plain fact, no hedge.
- Eval 2: no business/finance metaphor applied to the friendship anywhere in the output.

## One new, minor friction surfaced

Eval 3's run added a "Sources" footer after the decision block because WebSearch's own tool
instructions mandate a sources section whenever search results inform the response — which sits
outside ask-the-council's "nothing after the template" rule. Not fixed this round; flagging it as
a real tension between the skill's strict template and a tool-level requirement it can collide
with.
