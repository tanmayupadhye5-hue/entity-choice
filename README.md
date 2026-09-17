# Entity Structure Advisory — `/entity-choice`

A **practitioner-facing** Claude skill that helps a CPA reason through **choice of
entity** for a new business, or whether an existing entity should **convert** —
where *staying put* is always a legitimate answer, weighed against the cost of
switching.

> ⚠️ **For practitioners, not clients.** This is a decision-support tool the CPA
> runs. It is **not** a tax opinion, **not** a computation engine, and **not**
> authority. Every output is a draft for professional review. Code references
> (e.g., §1361) are pointers to verify, never conclusions of law.

## What it does

Entity types in scope: sole proprietorship, general partnership, LLP, LLC
(disregarded / partnership / S-corp taxed), S corporation, C corporation. Scope
is US federal tax plus state considerations, with Delaware, Texas, Michigan, and
New York shipping with depth.

It runs a four-stage workflow designed to avoid a 60-question interrogation:

1. **Tier 0 — Hard eliminators.** Pure logic screens that remove options outright.
2. **Tier 1 — Always-ask intake.** ~A dozen questions asked every run.
3. **Tier 2 — Conditional deep-dives.** Fire only when a Tier 1 answer triggers them.
4. **Tier 3 — Tie-breakers & Reversibility Index.** Applied to close cases.

Output is a **draft advisory memo** with the recommendation (or a withheld notice),
the runner-up and why it lost, eliminated options, unverified assumptions, what
would change the answer, open questions, and a plain-English **Client Discussion
Roadmap** for the CPA.

## Files

| File | Purpose |
|---|---|
| `skills/entity-choice/SKILL.md` | The workflow, tiers, output format, and behavior settings. |
| `skills/entity-choice/benchmarks.md` | Parameters read on **every** run — federal + DE/TX/MI/NY, plus a **user-maintained section** you edit and keep. |
| `skills/entity-choice/references/deep-dives.md` | Detailed Tier 2 tax-module analysis, loaded only when a trigger fires. |
| `.claude-plugin/marketplace.json` | Lets Claude Code install this as a plugin (see below). |

## Install in Claude Code (recommended)

This repo is a Claude Code plugin marketplace. Add it once, then install:

```
/plugin marketplace add tanmayupadhye5-hue/entity-choice
/plugin install entity-choice
```

Restart Claude Code if prompted, then run `/skills` to confirm `entity-choice`
is available.

## Install manually (any Claude with skills)

Copy the `skills/entity-choice/` folder into your skills directory — e.g.
`~/.claude/skills/entity-choice/` for Claude Code, so the path is
`~/.claude/skills/entity-choice/SKILL.md`.

## Maintain your own benchmarks

`benchmarks.md` ships with **placeholder** figures. **Verify and replace every
value before relying on it.** The shipped section carries `as_of` and `source`
fields; the separate user-maintained section holds your own state data, firm
positions, and two behavior dials (`challenge_level`, `confidence_threshold`). A
skill update should never overwrite the user-maintained section.

## Disclaimer

This project is provided as-is for professional use. It does not provide tax,
legal, or accounting advice, and produces drafts only. The practitioner is
responsible for all analysis, verification, and conclusions.
