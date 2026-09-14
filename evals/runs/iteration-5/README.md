# Iteration 5 — eval 3 swapped and validated for real generalization

Eval 3's old prompt (Notion vs. Obsidian) turned out to be the Framer's own literal worked
example in `references/seat-definitions.md` — it was testing whether the model could retrieve a
documented answer, not whether the Framer generalizes. Swapped to a job-offer scenario (a
different domain, a different upstream failure mode: unverified negotiability and an unexamined
comparison axis, not habit-vs-tool) and run once, transcript read directly rather than
self-reported, per instruction.

## Verdict: genuine reasoning, not a retrieval echo

The Framer's reframe does two things the old pattern never did: reframes "which pays more" into
"what does the harder option cost that money doesn't buy back," and catches a framing bias
specific to the prompt's own wording ("you already named B 'saner' — some part of you has scored
this already, and you might be here for permission more than a decision"). That's not a
"it's-not-the-tool-it's-the-habit" swap-in with new nouns.

The panel's disagreement is genuinely heterogeneous, not a uniform reframe-and-converge:
Skeptic/Accountant/Stakeholder lean toward Job B with distinct, scenario-specific reasoning
(hidden commute costs, who else absorbs unpredictable hours); Long View opens a real, undefeated
case for Job A tied to career compounding; Framer and Builder don't take a side at all, pushing
toward two days of fact-finding instead. Step 3 correctly did NOT force a manufactured Skeptic
objection, since real disagreement already existed — the mechanism applying its own exception
correctly, not a rubber stamp.

Full transcript: [`wrong-question-detection-transcript.md`](wrong-question-detection-transcript.md).
Final user-facing output: [`wrong-question-detection-response.md`](wrong-question-detection-response.md).

## Mechanical checks

All passed: Mode line present with scenario-specific reasoning (not a generic restatement of the
routing rule), every required template section present, Strongest objection non-empty and
substantive, every seat's contribution at or under the 3-sentence full-panel cap, audit pass
correctly found zero external factual claims requiring the checked-or-dropped pipeline (and
explicitly reasoned through the one borderline case — the Skeptic's "fails the way this kind of
offer tends to fail" — before concluding it's a predicted framing, not a disguised precedent
claim).

## Not yet done

This new prompt hasn't been baseline-tested (no-skill comparison). The old eval 3's 4/4
baseline-reframe finding was specific to the Notion/Obsidian prompt and doesn't transfer here.
