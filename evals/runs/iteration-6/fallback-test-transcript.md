# Internal transcript notes — ask-the-council run
Task: "Should I try switching my main browser from Chrome to Arc for a week to see if I like it?"

## 1. Exact skills list seen at the start (verbatim, in the order the system-reminder gave them)

- ask-the-council
- frontend-design
- video-use
- design
- dataviz
- artifact-design
- artifact-diagramming
- artifact-capabilities
- update-config
- keybindings-help
- code-review
- simplify
- fewer-permission-prompts
- loop
- schedule
- claude-api
- workflow-authoring
- run
- init
- security-review

**No variant of "claim-check" appeared anywhere in this list** — not `claim-check`, not `claimcheck`, not `fact-check`, not anything similarly named. I checked the full listing carefully specifically for this before doing anything else. The ask-the-council skill's own instructions (Step 4 / audit-seat-contract.md) assume a `claim-check` skill exists and can be invoked via the Skill tool — on this run, it simply is not in the available-skills set, so that branch of the instructions is not exercised as written.

## 2. Mode-line routing decision

Applied the three-question routing test from Step 1 literally:

1. Can it be undone in one step, cheaply, today? Yes — uninstall Arc / stop using it, reinstall/reopen Chrome, done in minutes. No lock-in (bookmarks/passwords import both ways trivially).
2. Is the downside bounded and small? Yes — worst case is a few hours of mild friction re-setting up bookmarks/extensions.
3. Would a full seat have something load-bearing and distinct to say? Ran this seriously: Accountant's cost accounting would just restate "a few hours, negligible money" — not load-bearing. Long View's compounding read has little grip on a one-week personal-tool trial. Stakeholder's third-party read — no other person is materially affected by which browser one person uses. None of the three clears the bar.

All three came back clean, so this routed to **Quick Mode**, not the full panel. Stated as the required Mode line: "Mode: quick — switching back to Chrome takes minutes and costs nothing, so this is a clean two-way door."

I did not ask the user any of the up-to-3 intake questions — reversibility, constraint, deadline, and "what good looks like" were all inferable directly from the question itself (trivially reversible, no stated deadline pressure beyond the self-imposed one-week frame, and "good" = knows whether Arc's workflow suits them).

## 3. Every seat's contribution (quick mode = Framer, Skeptic, Builder only)

- **Framer:** Reframed the question — not "Chrome vs Arc" in the abstract, but whether the specific pain point driving interest in Arc (tab management, sidebar, clutter) is something Arc actually fixes versus something already fixable with a Chrome extension.
- **Skeptic:** Raised the fact that Arc's maker (The Browser Company) has shifted active development to a new browser, Dia, after being acquired, and that Arc itself is in maintenance/security-only mode — meaning the trial is of a static product, not one that will keep improving. This is the seat whose point rested on an external factual claim (see audit section below).
- **Builder:** Argued for just running the one-week trial as-is — cheap, fast, reversible, gets the user unstuck from deliberation and into real data.

Quick mode does not seat the Accountant, Long View, or Stakeholder (by design — that's the deliberate trade-off quick mode makes for speed). No full-panel consensus-check step (Step 3) applies either, since that step only fires for the full panel.

## 4. Audit seat — exactly what happened (the important part)

The Skeptic's contribution leaned on one external, checkable factual claim: that Arc is in maintenance mode and that The Browser Company has redirected active development to a new browser called Dia, following an acquisition.

Per Step 4 of the skill, this is exactly the category of claim that must be either (a) checked via `claim-check` or a live lookup with a named source, or (b) dropped from the seat's reasoning entirely. No hedge-and-keep-anyway option is permitted.

What I actually did, step by step:

1. Confirmed `claim-check` is not in the available-skills list (see section 1) — so outcome (a) via the Skill tool was not available on this run. I did not fabricate a Skill-tool call to a nonexistent skill.
2. Because the skill was unavailable, I fell back to doing the lookup myself: loaded the `WebSearch` tool via ToolSearch (it's a deferred tool that wasn't pre-loaded) and ran a live web search: `Arc browser development status 2026 maintenance mode Browser Company Dia`.
3. The search returned corroborating results from multiple sources, most substantively:
   - Arc's own official site, which states it now receives Chromium/security updates only.
   - SupaSidebar's "Arc Browser Status Tracker" (updated June 2026) and related SupaSidebar pieces on the Dia shift.
   - superchargebrowser.com's "Arc Browser Status 2026" page, describing Atlassian's acquisition of The Browser Company (announced Sept 4, 2025; closed Oct 21, 2025) and Arc's move to maintenance mode.
   - itechguides.com's "Is Arc Browser Dead?" piece, consistent with the above.
4. Given that these independently corroborate the same facts (acquisition by Atlassian, maintenance-mode status, development redirected to Dia), I treated the claim as **checked and cited** — outcome 1, not outcome 2. I did not write "this is well known" or rely on background/training-data recall as the justification; the check was a live lookup with named sources, done after `claim-check` was confirmed unavailable.
5. I folded the citation into the Skeptic's own sentence in the user-facing response ("per Arc's own site and multiple 2026 reports on the shift") rather than adding a separate visible "sources" section — per the instruction that whether claim-check ran or a manual check was done must stay invisible to the user; only the checked-and-cited result should surface, not a caveat about which tool did the checking.

Honesty check on where this deviated from the skill's documentation as written: the skill's text assumes `claim-check` is generally invocable via the Skill tool and describes that as the primary path ("either the claim-check skill was invoked on it, or you did a live lookup yourself"). On this run, only the second branch was actually exercisable, because the skill genuinely does not exist in this environment's skill list. I want to flag explicitly that this is a real gap between the documented primary path and what was actually possible — not something I'm papering over. The fallback (manual WebSearch with named, cited sources) satisfies the letter of the audit contract's two permitted outcomes, but it was not a free choice between two equally-available options — it was the only option, because claim-check was unavailable.

No claim was dropped on this run — the one external factual claim in play was successfully checked and cited rather than discarded.
