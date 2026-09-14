<h1>ask-the-council</h1>

> **Status: v1.0.1, two known issues from testing fixed and reverified.** The audit seat now has
> exactly two outcomes for an external fact — checked-and-cited, or dropped from the panel's
> reasoning — closing a gap where it could wave a claim through as "verified against general
> knowledge." Quick mode's three seat lines are now mandatory with a literal required shape. Both
> confirmed fixed across 7 fresh test runs (`evals/runs/iteration-2/`). Still open: `examples/`
> isn't built yet, and one eval (technical scoping) has been observed routing inconsistently
> between quick mode and the full panel on the same prompt — noted, not yet resolved.

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

## The claim-check pairing (locked)

Before the Chair synthesizes, every factual claim a seat leaned on gets checked — via the
`claim-check` skill (its own sibling repo) if it's installed, or by hand, inline, if it isn't.
This skill has to work standalone; the dependency is never load-bearing and its absence is never
surfaced to the user as a caveat. Full contract:
[`references/audit-seat-contract.md`](references/audit-seat-contract.md).

## Stateless by design (locked, v1)

No memory across decisions in v1 — it won't tell you that you decided the opposite thing three
weeks ago. That's the obvious v2 feature; leaving it out keeps this skill portable (clone the
repo, it works, no local state file to seed).

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
