# Iteration 6 — audit-seat fallback path proven, with claim-check genuinely uninstalled

The `audit-seat-contract.md` says the fallback ("do the same job by hand") works when
`claim-check` isn't installed. Until this round that was untested prose. Proved it by actually
removing the skill and rerunning eval 4's prompt (Chrome vs. Arc), which reliably exercises the
audit seat via the Skeptic's claim about Arc's development status.

## Two attempts — the first taught something, the second is the real result

**First attempt (invalid, kept for the record):** renamed `~/.claude/skills/claim-check` to
`claim-check.disabled-for-test` rather than removing it. That didn't work — the agent found
`claim-check.disabled-for-test` in its skills list, tried invoking `claim-check` by its original
name anyway, and the Skill tool silently resolved and ran it in full. **Real, separate finding**:
skill name resolution goes by the `name:` field in SKILL.md frontmatter, not the folder name —
renaming a skill's directory does not disable it if the name in its own frontmatter is unchanged.
Worth knowing generally, unrelated to this test's actual question.

**Second attempt (the real result):** moved the entire skill directory out of `~/.claude/skills/`
entirely (parked in `%TEMP%`, restored afterward). Confirmed genuinely absent — the agent's
skills list (20 entries, logged verbatim in the transcript) contains no variant of `claim-check`
at all.

## Result: the fallback path works

With claim-check genuinely unavailable, the audit seat did the check by hand: fetched the
`WebSearch` tool itself (not preloaded), ran a live search, found multiple independent sources
(Arc's own site, third-party trackers, 2026 coverage) corroborating the Arc-maintenance-mode
claim, and folded a citation directly into the Skeptic's line. Checked-and-cited, not dropped,
not hedged. No tooling caveat leaked into the user-facing response.

One honest note from the agent, not a bug: the contract presents claim-check-or-manual-lookup as
two available options, but on a run where claim-check is genuinely absent, only the manual path
is actually exercisable — which is just what "uninstalled" means, not a design flaw.

Full transcript: [`fallback-test-transcript.md`](fallback-test-transcript.md).
