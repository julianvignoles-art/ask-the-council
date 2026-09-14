Mode: full panel — this bets a live client contract on an irreversible six-week call, not a cheap one-step reversal.

**Decision:** Don't stop everything for a full rewrite; run a short, time-boxed diagnostic on the worst global-state offender, then do a scoped refactor of just that layer while you keep shipping — and if the diagnostic proves the coupling is unfixable piecemeal, tell the client now and renegotiate scope, not at week eight.

**Confidence:** medium — depends on whether the coupling is actually as deep as it feels, which you don't know yet.

**Why:**
1. Six weeks against a real contract deadline is not a door you can walk back through for free — a full rewrite is the classic way to lose a project's remaining runway. Joel Spolsky's 2000 case against Netscape's ground-up rewrite is the concrete version of this: they set out to rebuild Communicator "properly" and went roughly three years between major releases while competitors ate their market ([Joel on Software, "Things You Should Never Do, Part I," Apr 6 2000](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/)).
2. The actual symptom you described — every new feature taking longer because of global state — is almost always localized to a specific layer, not the whole system; isolating that layer behind an interface typically recovers most of the lost velocity without betting the whole contract on a from-scratch build finishing in time.
3. Clients pay for visible progress against agreed deliverables, not architectural cleanliness; going dark to rewrite risks trust and payment even if the result is better, while a disclosed, scoped refactor ("here's why the last few features were slow, here's the fix") keeps them informed and still gets you the structural win.

**Strongest objection:** The panel converged fast here, which is itself a flag, so weigh this seriously: if the global state is genuinely load-bearing everywhere — a true ball of mud where nothing moves without touching everything — then incremental refactor-while-shipping is a fantasy; every patch adds another tendril, the codebase never stabilizes, and you spend six weeks getting slower instead of faster, making an early, disciplined rewrite of the core the actually cheaper path.

**Why it loses:** That case is only real if you've actually tested the coupling rather than just feeling it — a lot of "everything touches everything" code is really "everything got dumped in the same place because it was fastest at the time," which isolates fine once you try. The fix is to find out cheaply before committing six weeks in either direction, which is exactly what the diagnostic below does.

**What would flip this:** A 1–2 day spike to isolate the single most-patched feature's state behind a module boundary either works cleanly (proceed with scoped refactor) or reveals the coupling truly can't be contained without touching most of the codebase (proceed with a scoped rewrite of the state layer only, and flag the timeline risk to the client immediately).

**Do this first:** This week, time-box a 1–2 day spike: take the feature area that's been slowest to touch, pull its state behind an interface, and see whether that alone restores velocity — let that evidence, not the accumulated frustration, decide the rewrite question.
