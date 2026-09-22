---
name: entity-choice
description: >-
  Practitioner-facing decision support for choosing or converting a business
  entity structure (sole proprietorship, general partnership, LLP, LLC taxed as
  disregarded/partnership/S corp, S corporation, or C corporation) for US
  federal and state tax purposes. Use this whenever a CPA, EA, tax advisor, or
  accountant is helping a client decide what entity to form, whether to convert
  an existing entity (LLC → S corp, S corp → C corp, C corp → LLC, etc.), or is
  weighing the tax, liability, and administrative tradeoffs of entity forms.
  Trigger on phrases like "choice of entity", "entity selection", "what entity
  should my client be", "should they elect S corp", "C corp vs LLC", "convert to
  an S corp", "is it worth switching structures", reasonable-compensation or
  QBI/§199A entity questions, and similar — even when the user does not say the
  word "entity". This is NOT client-facing and NOT a tax opinion; it produces a
  draft advisory memo for the practitioner to review.
---

# Entity Structure Advisory (`/entity-choice`)

A decision-support workflow the **practitioner runs, not the client**. It helps a
CPA reason through choice of entity for a new business, or whether an existing
entity should convert — where *staying put* is always a legitimate answer,
weighed against the cost of switching.

Entity types in scope: **sole proprietorship, general partnership (GP), LLP, LLC
(disregarded / partnership / S-corp taxed), S corporation, C corporation.**

Scope is **US federal tax plus state considerations.** Delaware, Texas,
Michigan, and New York ship with depth in `benchmarks.md`. For any other state,
ask the practitioner for the state facts you need and offer to save their answers
into the user-maintained section of the benchmark file.

## What this is — and is not

Hold these boundaries on every run:

- **Not client-facing.** The client never runs this and never sees raw output.
  Everything you produce is a working draft for the advisor.
- **Not a tax opinion or authority.** Code section references (e.g., §1361) are
  *pointers for the practitioner to verify*, never conclusions of law.
- **Not a computation engine.** Dollar figures are benchmark-driven estimates,
  always shown as **ranges**, never as a precise tax calc.
- **Not self-updating.** All parameters live in `benchmarks.md`, which the
  practitioner maintains.

**Every output must close with a single line** stating it is a draft for
professional review, not a conclusion. This is non-negotiable because the whole
tool is premised on the CPA — not the model — owning the judgment.

## Load the benchmark file first

At the start of every run, read `benchmarks.md` from the skill folder. It holds
SE-tax break-even points, reasonable-compensation ranges by occupation, state fee
schedules and entity-level taxes, economic-nexus parameters, §199A thresholds,
and traps seen in practice. It has two parts:

- **Shipped defaults** — federal parameters and the four deep-state datasets.
  Every value carries an `as_of` date and a `source`.
- **User-maintained section** — the practitioner's own state data, firm
  positions, and two behavior settings. Never overwrite this section; a skill
  update must leave it intact.

The two behavior settings, and the safety floor that overrides them, are
described under [Behavior settings](#behavior-settings) below.

## The four-stage flow

Run these in order. The design goal is to **avoid a fixed 60-question
interrogation** — eliminate first, ask a lean standard set, deep-dive *only* on
triggers, then break ties.

```
Client facts
  → Tier 0: Hard eliminators        (pure logic, removes options)
  → Shortlist (usually 2–3 options)
  → Tier 1: Always-ask intake       (~a dozen questions, every run)
  → Trigger facts present?
      → Tier 2: Conditional deep-dives   (fire only on their trigger)
  → Tier 3: Tie-breakers & reversibility (close cases only)
  → Draft advisory memo for advisor review
```

Because Tier 2 modules fire only when a Tier 1 answer triggers them, a solo
consultant is never asked about special allocations, and a cash-only service
firm is never walked through §351 property mechanics.

---

## Tier 0 — Hard eliminators

Pure logic screens, run **before any analysis**. Each fact removes options
outright. State the disqualifying fact when you drop an option.

| Fact | Eliminates | Pointer |
|---|---|---|
| One owner | GP, LLP (need 2+ owners) | — |
| Non-resident alien owner | S corp | §1361(b)(1)(C) |
| Corporate or partnership owner | S corp | §1361(b)(1)(B) — but a **disregarded entity** looks through to its owner and does not itself disqualify. |
| More than 100 shareholders | S corp | §1361(b)(1)(A) |
| Needs more than one class of stock | S corp | §1361(b)(1)(D) |
| **Ineligible** trust holds interest | S corp | §1361(c)(2) — grantor, QSST, ESBT, voting and testamentary (2-yr) trusts **are eligible**; QSST/ESBT require an election. Only other trusts disqualify. |
| Liability shield required | Sole prop, GP | — |
| Licensed profession | Plain LLC in many states (PLLC/PC instead) | state law |
| Institutional outside capital planned | All but C corp (investor preference for preferred stock) | — |

After Tier 0 you should usually hold a **shortlist of 2–3 surviving options.**
Announce it before moving on.

---

## Tier 1 — Always-ask intake

Ask **one question at a time, conversationally** — not as a wall of form fields.
Three questions open every run:

1. New formation, or an existing entity considering a change?
2. State of formation, and states of operation.
3. Tax year to apply.

Then the standard twelve:

1. For **each owner**: ownership %, whether they work in the business, and whether they are
   an individual, an entity or a trust.
   - **Individuals**: filing status (single, MFJ, MFS, head of household, qualifying
     surviving spouse) and other taxable income — the §199A threshold test is applied to
     *each owner's own* taxable income, and MFJ carries roughly double the threshold.
   - **Entities**: what kind (C corp, S corp, partnership, disregarded, tax-exempt,
     foreign, ESOP), plus UBTI (§512), §1446 withholding and any blocker.
   - **Trusts**: what kind, since that decides S-corp eligibility.
2. Nature of business — service or product, and whether it is a licensed profession.
3. Projected net income for the next three years, as a range.
4. Which owners work in the business and which are passive.
5. Expected profit split — pro rata or unequal.
6. Whether the entity will borrow, and whether owners will personally guarantee.
7. Property being contributed. For each contributed asset capture the
   **contributor**, the **carryover basis** (their adjusted basis), the
   **present fair market value**, and the **liability the entity assumes** —
   these three figures decide whether the contribution is tax-free and what
   basis everyone takes.
8. Services contributed for equity by any owner.
9. Losses expected in early years, and whether owners need them personally.
10. Outside capital or equity-compensation horizon.
11. Exit horizon and likely buyer type.
12. Tolerance for formalities and ongoing administration.

**For conversions**, also ask: what the current entity is, when it was formed, and
whether prior elections have been made (S election, §754, QSST/ESBT, etc.).

**Tag every input** as `client-stated`, `practitioner-estimated`, or
`documented`. This tagging matters because the memo later surfaces which
load-bearing facts are still unverified — you can't do that if you didn't track
provenance as you went.

Each of these answers is also a potential Tier 2 trigger. Watch for the trigger
facts in the table below as you go.

---

## Tier 2 — Conditional deep-dives

Each module fires **only on its trigger fact** from Tier 1. When a trigger is
present, work the corresponding analysis and read
`references/deep-dives.md` for the detailed code-section walkthrough of that
module — keep that depth out of the conversation until it's actually needed.

| Trigger fact from Tier 1 | Module |
|---|---|
| Appreciated / encumbered property contributed | §351 control vs. §721; §357(c)/(b); §704(c) built-in gain |
| Unequal split or sweat equity | Special allocations & substantial economic effect; profits interest (Rev. Proc. 93-27); services-for-equity as comp |
| Entity will carry debt | §752 basis for entity debt; S-corp basis limited to direct shareholder loans / debt-basis restoration |
| Early losses expected | Loss-limitation stack: basis → §465 at-risk → §469 passive → §461(l) EBL → NOL carryforward |
| Scalable business / significant exit | §1202 QSBS; F-reorg for S-corp targets; asset vs. stock sale (C-corp double-tax on asset sale vs. flow-through) |
| High income with working owners | Reasonable comp & audit exposure; retirement-plan capacity (W-2 vs. SE); §199A phase-outs & SSTB; state PTET |
| Real estate or multiple business lines | Charging-order protection for SMLLCs; series LLC mechanics; §754 inside basis step-up |
| Multi-state or foreign expansion | Post-*Wayfair* economic nexus (txn counts & revenue caps); state non-recognition of S status; PTET to bypass SALT cap |
| Existing C corp converting | §1374 BIG tax & 5-year recognition; accumulated E&P; passive-investment-income termination risk |
| Existing S corp | Inadvertent-termination causes; second-class-of-stock risk from disproportionate distributions |
| C corp retaining earnings | Accumulated earnings tax; personal holding company tax |

---

## Tier 3 — Tie-breakers & Reversibility Index

Apply only to the **surviving options in a close case**:

- **SE-tax delta**, net of payroll-administration cost and retirement-plan
  capacity limits.
- **QBI eligibility delta** at the client's income level.
- **State-level treatment** — annual fees, PTET, entity-level taxes.
- **Reversibility Index** — how expensive the structure is to *unwind*. A
  cheap-to-form structure that is punishing to exit can lose to a more
  deliberate one. For example, converting a C corp back to an LLC triggers a
  constructive corporate liquidation:
  - §331/§336 — assets treated as sold at FMV.
  - Corporate-level gain recognition; likely a mandatory third-party appraisal.
  - Final corporate return; state dissolution/conversion fees.

Reversibility is a first-class tie-breaker, not a footnote — the cost of being
wrong is part of the recommendation.

---

## Output — the draft advisory memo

Print the memo to chat in this fixed structure:

```
# Entity Recommendation — DRAFT for practitioner review

## Recommendation
<Recommended entity + confidence, OR a withheld-recommendation notice>

## Runner-up
<The runner-up and the single factor on which it lost>

## Eliminated options
<Each eliminated option with its disqualifying fact>

## Contributed property consequences

*(Include this section whenever any property is contributed.)* For each
contributed property, state:
- **Built-in gain or loss** - present FMV less the contributor's carryover basis.
- **Liability assumed vs. carryover basis** - whether the liability the entity
  assumes exceeds that basis, and if so the gain triggered and roughly how much
  (§357(c) in corporate form; §752(b) deemed distribution and §731 gain in
  partnership form).
- **The entity's basis in the property** - carryover under §723 (partnership) or
  §362 (corporation), plus any gain recognised.
- **The contributing owner's outside basis** - §722, increased by their share of
  liabilities under §752 and reduced by the liability shifted to the others.
- **§704(c) layer** - the built-in gain allocated back to that contributor, and
  the method choice (traditional, curative, remedial) where it matters.
- **Disguised sale (§707(a)(2)(B), Reg. §1.707-3/-5).** Where the entity
  assumes a liability on contributed property, decide whether it is a
  **qualified liability** (broadly, incurred more than two years before the
  transfer, or in the ordinary course, or allocable to capital expenditures on
  that property). A qualified liability is generally not sale consideration; a
  non-qualified one is, to the extent it exceeds the partner's share. Reach a
  conclusion either way - "considered and qualified" and silence look identical
  to the reader.
- **Recapture exposure** - §1245/§1250 on the accumulated depreciation, and the
  carryover holding period and depreciation schedule under §168(i)(7).

§tate how the answer differs under each surviving entity form; contributed
property is frequently the fact that decides the recommendation.

## Deadlines and elections

*(Include whenever any of these apply. Several have no relief mechanism, so an
omission here is the most expensive kind.)*

- **§83(b)** - where equity is issued for services. A pure profits interest
  under Rev. Proc. 93-27 is generally non-taxable on grant, but a protective
  election is standard practice and the **30-day deadline is absolute** - there
  is no §9100 relief for missing it.
- **Form 2553** - where an S election is contemplated: generally 2 months and
  15 days from the start of the tax year it is to take effect.
- **QSST / ESBT election** - where a trust would hold S corporation stock.
- **§754 election** - where appreciated property or real estate is involved:
  filed with a timely return for the year of the transfer or death, and it binds
  the partnership going forward.
- **First-return elections** - accounting method, and the required tax year for
  a partnership or S corporation absent a §444 election.

State the deadline, not merely the election.

## Assumptions relied on (unconfirmed)
<Load-bearing facts the practitioner has not confirmed, tagged as such>

## What would change the answer
<Named trigger facts that would flip or reopen the analysis>

## Open questions before filing
<Specific items to resolve with the client>

## Client Discussion Roadmap
<3 plain-English verification questions for the CPA to ask the client verbally —
e.g. near-term outside-equity plans, family-member inclusion, geographic
expansion timing — to catch behavioral nuance a static intake misses>

---
This is a draft for professional review, not a conclusion.
```

The **Client Discussion Roadmap** is what turns the memo from analysis into a
next action for the CPA: three targeted questions to raise with the client that
tend to surface the behavioral facts intake forms miss.

Always end with the draft-disclaimer line, verbatim.

---

## Behavior settings

The user-maintained section of `benchmarks.md` holds two dials:

- **`challenge_level`** — how hard to push back when the practitioner disagrees
  with the analysis. Higher means argue the point and show your reasoning;
  lower means note the disagreement once and defer.
- **`confidence_threshold`** — how marginal a case must be before you *withhold*
  a recommendation rather than force one. A high threshold means close calls
  come back as "withheld — too close on X" instead of a pick.

### Safety floor (overrides both settings)

Neither dial can suppress a high-risk flag. Regardless of the settings, always
surface:

- Reasonable-compensation sensitivity (S-corp audit exposure).
- Unsettled or aggressive positions.
- Economic-nexus threshold crossings.
- Load-bearing **unverified** inputs.

These surface at every setting because they are the facts most likely to hurt
the client later — the point of the tool is to make sure they are never quietly
optimized away.

---

## Reference files

- **`benchmarks.md`** — parameters read on every run (federal + DE/TX/MI/NY,
  plus the practitioner's own section and behavior settings).
- **`references/deep-dives.md`** — the detailed code-section analysis for each
  Tier 2 module. Read the relevant section only when its trigger fires.
