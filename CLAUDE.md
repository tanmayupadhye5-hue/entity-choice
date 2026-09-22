# entity-choice — the published Claude Code skill

A practitioner-facing skill (`/entity-choice`) that walks a CPA through choice of
entity. Published at <https://github.com/tanmayupadhye5-hue/entity-choice> and
installed by other CPA firms via:

```
/plugin marketplace add tanmayupadhye5-hue/entity-choice
/plugin install entity-choice
```

## Layout

This repo is both a **plugin marketplace** and the plugin itself:

- `.claude-plugin/marketplace.json` + `plugin.json` — what makes the `/plugin`
  commands above work
- `skills/entity-choice/SKILL.md` — the workflow: Tier 0 eliminators, Tier 1
  intake, Tier 2 trigger table, Tier 3 tie-breakers, and the required memo
  structure
- `skills/entity-choice/benchmarks.md` — parameters read every run. **Placeholder
  figures**; each practitioner is expected to verify and maintain their own.
- `skills/entity-choice/references/deep-dives.md` — the 11 Tier 2 modules, loaded
  only when their trigger fires

## Keep it in sync with the app

`C:\Claude\entity-choice-app` **vendors copies of all three files**. A change
made here alone means the app still gives the old answer. **The paths do not
mirror each other:**

| Skill (this repo) | App |
|---|---|
| `skills/entity-choice/SKILL.md` | `app/content/SKILL.md` |
| `skills/entity-choice/benchmarks.md` | `app/content/benchmarks.md` |
| `skills/entity-choice/references/deep-dives.md` | `app/content/deep-dives.md` |

From the app, `.venv\Scripts\python.exe -m scripts.check_skill_sync` reports any
drift, and its test suite fails on it. Run it after editing either side.

## Corrections already made — do not regress

- Grantor, QSST, ESBT, voting and testamentary trusts **are eligible** S
  corporation shareholders; only other trusts disqualify, and QSST/ESBT require
  an election.
- A **disregarded entity looks through** to its owner and does not itself bar an
  S election.
- Tier 1 asks per-owner facts (filing status, other income, material
  participation) because §199A and §469 are applied to each owner individually.
- Contributed property needs the **contributor, carryover basis, present FMV and
  the liability the entity assumes** — those three figures decide whether the
  contribution is tax-free.
- The memo must include **Contributed property consequences** and **Deadlines and
  elections** (§83(b)'s 30 days with no §9100 relief, Form 2553, QSST/ESBT, §754,
  first-return elections), and must *conclude* the disguised-sale question rather
  than merely mention it.
- §706(b) **majority interest is more than 50% of profits AND capital** — never
  ownership or voting percentages.
- §199A is tested **owner by owner with the arithmetic** before any limit is
  called a risk; SE tax **shares one wage base per person**.
- A benchmark figure older than the tax year is **flagged, not presented as
  current**; a figure missing from the file is never filled from memory.
