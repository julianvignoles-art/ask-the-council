<h1>ask-the-council</h1>

A Claude skill for running a decision through a fixed panel of perspectives built to disagree
with each other, then synthesizing the disagreement into one recommendation — instead of asking
an assistant for a take and getting back five paragraphs of agreeable hedging.

## Download & install (2 steps, no terminal needed)

**1. Download the file:** **[⬇ ask-the-council.skill](https://github.com/julianvignoles-art/ask-the-council/releases/latest/download/ask-the-council.skill)**
(this link always points at the newest release)

**2. Upload it to Claude:** go to [claude.ai](https://claude.ai), open **Settings → Capabilities**
(sometimes labeled **Skills**), and either click **Upload skill** or just drag the downloaded
`ask-the-council.skill` file onto the page. That's it — no unzipping, no folders, no terminal.

*(If Claude's uploader is picky about the extension, just rename the downloaded file from
`ask-the-council.skill` to `ask-the-council.zip` — it's the same file, and both extensions are
accepted.)*

If you're using **Claude Code** (the CLI) instead of claude.ai in a browser, skip the download —
see [Install for Claude Code](#install-for-claude-code) below instead.

## What it catches

Asked "should I take Job A (15% more, brutal commute) or Job B (less pay, remote and sane)?", the
Framer seat didn't just weigh the two offers — it caught a tell in the user's own wording:

> "Notice you already named B 'saner' — some part of you has scored this already, and you might
> be here for permission more than a decision."

The panel then genuinely disagreed with itself: three seats leaned toward Job B for different
reasons, the Long View opened a real, undefeated case for Job A, and two seats didn't take a side
at all — pushing for cheap fact-finding instead. Because the disagreement was real, the
consensus-check didn't fire (it's built to fire only when everyone agrees, which is treated as a
red flag, not confirmation).

Four full runs — including one where `claim-check` was physically removed to prove the audit
seat's fallback path actually works, not just reads well — are in
[`examples/council-sample-output.md`](examples/council-sample-output.md).

## The panel (locked)

Six fixed seats, defined by what they optimize for and what they'll sacrifice — never by job
title, since "the CFO" and "the CTO" produce corporate cosplay and break the skill for personal
decisions ("should I take this job," "should I buy the cheaper tent"):

| Seat | Optimizes for | Sacrifices |
|---|---|---|
| The Framer | Asking the right question | Getting a fast answer to the wrong one |
| The Builder | Learning fast | Treating a reversible choice as permanent |
| The Skeptic | Not being wrong | Optimism about what could go right |
| The Accountant | Honest cost | Enthusiasm about upside |
| The Long View | Compounding | Winning the sprint |
| The Stakeholder | Everyone not in the room | The clean, solo-owned version of the plan |

Plus a conditional **Specialist** seat, added only when a decision genuinely hinges on domain
facts (legal, medical, tax, a hard technical constraint) — auto-chosen, with the Chair stating
out loud which specialty it seated so it can be overridden. A fake expert is worse than no
expert.

**If all seats agree, that's a flag, not a green light.** Consensus in a panel you designed
yourself is usually an artifact of how the question got framed — the Chair has to say so and
force the Skeptic to make the strongest case against before finalizing.

## The claim-check pairing (locked, and proven)

Before the Chair synthesizes, every factual claim a seat leaned on gets checked — via the
`claim-check` skill (its own sibling repo) if it's installed, or by hand, inline, if it isn't.
This skill has to work standalone; the dependency is never load-bearing and its absence is never
surfaced to the user as a caveat. Full contract:
[`references/audit-seat-contract.md`](references/audit-seat-contract.md).

This isn't just a design promise — it's tested. `claim-check` was physically removed from the
skills directory (not renamed; renaming doesn't disable a skill, it turns out) and a full run
confirmed the fallback works: a live web lookup, sources named, no hedge. See Case 4 in
[`examples/council-sample-output.md`](examples/council-sample-output.md) for the transcript,
including an honest note the run itself flagged: the contract's "two equally available options"
framing overclaims when claim-check is genuinely absent, since only one option is actually
exercisable then. Left in verbatim rather than smoothed over.

## Stateless by design (locked, v1)

No memory across decisions in v1 — it won't tell you that you decided the opposite thing three
weeks ago. That's the obvious v2 feature; leaving it out keeps this skill portable (clone the
repo, it works, no local state file to seed).

## Limitations

<a id="limitations"></a>
Naming what this skill doesn't do, on purpose — a repo that only lists wins isn't credible.

**On at least one tested decision, it didn't beat a plain, skill-less Claude — this is historical,
about a prompt no longer in the eval suite, kept here because the finding itself is still true.**
An earlier version of the wrong-question eval ("should I switch from Notion to Obsidian") was
built to show the Framer catching a reframe a baseline would miss. It didn't: run 4 times
independently with no skill installed, plain Claude reframed the same premise (survivorship bias
in "people who stick with note-taking use Obsidian") every single time, before any feature
comparison. That prompt was later replaced for an unrelated reason (it turned out to be the
Framer's own literal worked example, making it a retrieval test, not a generalization one — see
`examples/council-sample-output.md`, Case 1). But the baseline finding predates that swap and
isn't invalidated by it: on a well-known productivity-forum question like that one, a
consistent, structured, repeatable format with a forced consensus-check is this skill's real
value proposition, not "sees what a baseline can't." The current eval 3 (a job-offer scenario)
hasn't been baseline-tested, so don't assume this finding transfers to it.

**It's stateless** (see above) — no memory of past decisions, on purpose, for now.

**The Specialist seat is a generalist pretending to know one domain**, not a real expert. It's
seated rarely and the Chair says which specialty it picked so it can be overridden, but treat any
domain-specific claim it makes with the same skepticism you'd give a knowledgeable friend, not a
professional.

## Building your own skill

This skill (and its sibling, claim-check) were built with **skill-creator**, which ships in
Claude Code's official plugin marketplace, not as a standalone tool. If you go looking for it and
hit a "no such path" error, that's why — it's at:

```
~/.claude/plugins/marketplaces/claude-plugins-official/plugins/skill-creator/skills/skill-creator/SKILL.md
```

## Install for Claude Code

<a id="install-for-claude-code"></a>
Symlink or copy this repo into `~/.claude/skills/`, same as any Claude skill:

```bash
ln -s /path/to/ask-the-council ~/.claude/skills/ask-the-council
```
