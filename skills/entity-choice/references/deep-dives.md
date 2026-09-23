# Tier 2 Deep-Dive Modules

Read only the section whose trigger fired in Tier 1. Everything here is a
practitioner reasoning aid — code references are pointers to verify, not
authority. Keep this depth out of the client conversation.

## Table of contents
1. Appreciated / encumbered property contributed
2. Unequal split or sweat equity
3. Entity will carry debt
4. Early losses expected
5. Scalable business / significant exit
6. High income with working owners
7. Real estate or multiple business lines
8. Multi-state or foreign expansion
9. Existing C corp converting
10. Existing S corp
11. C corp retaining earnings

---

## 1. Appreciated / encumbered property contributed
**Trigger:** owner contributes appreciated, encumbered, or non-cash property.

- **§351 vs. §721.** Corporate formation needs the **80% control test** under
  §351 for tax-free contribution; partnership/LLC contributions under §721 have
  no control requirement — a structural advantage for property-heavy deals.
- **§357(c).** Liabilities assumed in excess of basis trigger gain even in an
  otherwise tax-free §351 exchange. Flag encumbered property early.
- **§357(b).** Assumption of liabilities with a tax-avoidance or non-business
  purpose taints the *entire* liability amount as boot — a sharper trap than
  §357(c).
- **Disguised sale (§707(a)(2)(B); Reg. §1.707-3/-5).** A liability the
  partnership assumes is sale consideration unless it is a **qualified
  liability** (broadly: incurred >2 years before the transfer, in the ordinary
  course, or allocable to capital expenditures on that property). Transfers
  within two years are presumed a sale. Clear it explicitly.
- **§704(c).** In a partnership, built-in gain on contributed property must be
  allocated back to the contributing partner. This constrains "just split it
  evenly" arrangements and is a reason a partnership may be *more* faithful to
  economics than a corporation here.

## 2. Unequal split or sweat equity
**Trigger:** profit split is unequal, or an owner receives equity for services.

- **Special allocations & substantial economic effect** (§704(b) regs). Only
  partnerships/LLCs can specially allocate items; requires capital-account
  maintenance, liquidation per positive capital accounts, and DRO or QIO.
- **Economic effect equivalence** — the "dumb-but-lucky" backstop when the
  literal test isn't met.
- **Profits interest — Rev. Proc. 93-27 / 2001-43.** A pure profits interest for
  services is generally non-taxable on grant; a **capital interest** for services
  is compensation.
- **Services-for-equity as compensation.** In a corp, stock for services is
  ordinary income (§83). A protective **§83(b) election must be filed within
  30 days** of grant - an absolute deadline with no §9100 relief. It is the
  standard precaution even for a profits interest, in case the interest is
  later recharacterised as a capital interest.

## 3. Entity will carry debt
**Trigger:** entity will borrow; owners may or may not guarantee.

- **§752.** Partners/LLC members get **outside basis for entity-level debt**
  (recourse per economic-risk-of-loss; nonrecourse per the three-tier rules).
  This is a major partnership advantage for deducting debt-funded losses.
- **S-corp basis.** Shareholders get basis only for **direct** loans to the S
  corp — not for entity-level third-party debt, even if personally guaranteed.
  Watch debt-basis **restoration** ordering when the loan is later repaid.

## 4. Early losses expected
**Trigger:** losses expected in early years and owners want them personally.

Work the loss-limitation stack **in order** — a loss must clear every gate:
1. **Basis** (§704(d) partnership / §1366(d) S corp).
2. **§465 at-risk.**
3. **§469 passive activity** (material participation).
4. **§461(l) excess business loss** limitation.
5. **NOL carryforward** (§172; 80%-of-income cap).

The stack is why "I want to deduct the losses" often points toward a
partnership/LLC (debt basis under §752) over an S corp.

## 5. Scalable business / significant exit
**Trigger:** venture-scale ambitions or a meaningful exit is foreseeable.

- **§1202 QSBS.** C-corp-only exclusion; original-issue stock, $50M gross-asset
  test, 5-year hold, active-business requirement. Often the single biggest reason
  a scalable company chooses C corp despite double taxation.
- **F-reorganization.** Common pre-sale move for S-corp targets to create a
  clean holding structure and allow a §338(h)(10)/asset-sale-equivalent.
- **Asset sale vs. stock sale.** A C corp selling assets faces **double tax**
  (corporate gain + shareholder distribution); a flow-through gets a single tier
  and buyers usually prefer asset treatment / stepped-up basis. This friction is
  frequently the deciding factor at exit.

## 6. High income with working owners
**Trigger:** high projected income with owners active in the business.

- **Reasonable compensation & audit exposure.** The S-corp SE-tax savings only
  exists to the extent comp is *reasonable*; unreasonably low comp is the
  classic audit target. Pull the benchmark from `benchmarks.md` and flag it.
- **Retirement-plan capacity.** W-2 wages (S corp) vs. SE income (sole
  prop/partnership) drive Solo-401(k)/SEP limits differently — sometimes offsets
  the SE-tax delta.
- **§199A - test each owner, with the arithmetic.** Before applying any limit,
  estimate each owner's taxable income and compare it with that owner's own
  threshold for their filing status. Below it, neither the SSTB exclusion nor
  the W-2/UBIA limit applies; above it, SSTBs lose QBI and the W-2/UBIA limits
  bite.
- **SE tax - one wage base per person.** A partner's guaranteed payment, any
  distributive share subject to SE tax, and any W-2 wages from other work all
  share one Social Security wage base. Apply 12.4% OASDI up to the unused base,
  2.9% Medicare on all net SE earnings (x 92.35%), and 0.9% Additional Medicare
  above the filing-status threshold. Whether a member's distributive share is
  SE income at all is unsettled (§1402(a)(13); *Renkemeyer*, *Soroban*); state
  the position taken.
- **State PTET.** Elective pass-through entity tax to work around the SALT cap.
- **Owner health insurance and fringe benefits.**
  - C corp: owner premiums are generally excludable (§106); the most
    favourable form.
  - S corp: a >2% shareholder (with §318 family attribution) is treated as a
    partner under §1372. Premiums the company pays are W-2 wages (box 1,
    generally not FICA), and the shareholder deducts them under §162(l).
    Cafeteria-plan and most excludable fringes are lost.
  - Partnership/LLC: premiums are guaranteed payments, deductible under
    §162(l).
  Where the intake says the entity will pay owner health insurance, state the
  treatment under each surviving form.

## 7. Real estate or multiple business lines
**Trigger:** real estate held, or several distinct business lines.

- **Charging-order protection** for single-member LLCs varies sharply by state —
  a real asset-protection consideration, not just tax.
- **Series LLC** mechanics (availability and respect by other states is
  unsettled; note firm position in `benchmarks.md`).
- **§754 election** — inside basis step-up on transfer/death; valuable for
  appreciating real estate held in a partnership.

## 8. Multi-state or foreign expansion
**Trigger:** operations or sales across state lines or abroad.

- **Post-*Wayfair* economic nexus** — sales-tax registration triggered by revenue
  and/or transaction counts per state (see `benchmarks.md`). A safety-floor flag
  when a threshold is crossed.
- **State non-recognition of S status** — some states/cities don't follow the
  federal S election (e.g., NY requires a separate election; check NYC).
- **State PTET** to bypass the $10k SALT cap where available.

## 9. Existing C corp converting
**Trigger:** an existing C corp is considering S election or conversion.

- **§1374 built-in gains tax** — 5-year recognition period on net BIG at
  conversion; a real cost of C→S in the near term.
- **Accumulated E&P** carries over and interacts with distributions.
- **Passive investment income termination** — §1362(d)(3): an S corp with C-corp
  E&P and >25% passive income for 3 consecutive years loses S status.
- **LIFO recapture (§1363(d)).** A C corp using LIFO that elects S includes its
  LIFO recapture amount (the excess of FIFO over LIFO value) in income on its
  final C-corporation return; the added tax is paid in four equal annual
  installments. A conversion to an LLC is a §331/§336 liquidation in which
  inventory is deemed sold at FMV, so the LIFO reserve is recognized there too.
  For any business carrying inventory, ask the inventory method; if it is not
  provided, list it as an unverified input.

## 10. Existing S corp
**Trigger:** an existing S corp with any risk factors.

- **Inadvertent termination** — ineligible shareholder, blown class-of-stock
  rule, etc.; §1362(f) relief exists but is costly.
- **Second class of stock** — disproportionate distributions or non-conforming
  arrangements can create a deemed second class and terminate the election.

## 11. C corp retaining earnings
**Trigger:** a C corp accumulating rather than distributing earnings.

- **Accumulated earnings tax (§531)** — 20% penalty on earnings retained beyond
  reasonable business needs.
- **Personal holding company tax (§541)** — 20% on undistributed PHC income when
  the ownership and income tests are met.
