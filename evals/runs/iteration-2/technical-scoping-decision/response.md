Framer: Figure out exactly what's making each new feature slower to bolt on before picking rewrite or patch, because that diagnosis determines whether a rewrite would even fix it.
Skeptic: A full rewrite risks quietly becoming the new time sink you were trying to escape, since rewrites on hobby projects rarely stay scoped to "same thing, but cleaner" once you're actually in them.
Builder: Refactor just the one piece causing the most friction right now (probably wherever config or data flow got tangled) into a cleaner interface, so you get structure without freezing feature work for months.

**Decision:** Do a targeted refactor of the specific bottleneck, not a full rewrite.
**Confidence:** medium — depends on which piece is actually causing the slowdown, which isn't fully known yet.

**Why:**
1. A rewrite competes for the exact same scarce time/energy budget that patching already strains, with the added risk of a long stretch where the dashboard works worse than it does now.
2. "Every new feature takes longer" is usually a symptom of one or two specific things (no shared data layer, config sprawl, copy-pasted scripts) — fixable by refactoring that seam, not by starting over.
3. Because this is a hobby project with no external deadline, you can afford to de-risk incrementally: refactor one module while the dashboard keeps running, rather than committing to a rewrite that has to work before it's useful again.

**Strongest objection:** If the scripts are coupled so tightly that there's no clean seam to pull out without touching everything, incremental refactoring will just be slow patching with extra steps, and a rewrite may genuinely be the only way out.
**Why it loses:** You don't know yet whether that's true — and the way to find out costs about an hour, not a rewrite.

**What would flip this:** Try to extract the single most tangled piece (often the data-collection or config layer) into a clean interface. If you can't do it without touching most of the codebase at once, that's real evidence the coupling is too deep and a rewrite is warranted.

**Do this first:** Spend an hour tracing exactly why the last feature you added took as long as it did — that answer tells you whether to refactor a seam or rewrite the whole thing.
