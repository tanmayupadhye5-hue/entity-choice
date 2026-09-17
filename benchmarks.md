# Entity-Choice Benchmark File

This file ships with the skill and is read on **every** run. Edit it by hand in
any text editor. It works on first run as-is.

Two parts:
- **Shipped defaults** — maintained with the skill. Every value carries an
  `as_of` date and a `source`.
- **User-maintained section** — yours. A skill update must never overwrite it.

> All figures are benchmark estimates for practitioner reasoning, shown as
> ranges. They are not a tax computation and not authority. Verify before use.

---

# PART 1 — SHIPPED DEFAULTS

## Federal parameters

| Parameter | Value | as_of | source |
|---|---|---|---|
| SE tax — Social Security wage base | $176,100 | 2025 | SSA / IRS |
| SE tax rate (OASDI + Medicare) | 15.3% up to wage base; 2.9% Medicare above; +0.9% Additional Medicare over threshold | 2025 | IRC §1401 |
| §199A QBI deduction | 20% of QBI, subject to limits | 2025 | IRC §199A |
| §199A taxable-income thresholds (phase-in of W-2/SSTB limits) | MFJ $394,600–$494,600; Single $197,300–$247,300 | 2025 | Rev. Proc. 2024-40 |
| C corporation federal rate | 21% (flat) | 2025 | IRC §11 |
| §1202 QSBS exclusion cap | Greater of $10M or 10× basis (per pre-July-2025 rules; verify tiered changes for later acquisitions) | 2025 | IRC §1202 |
| Accumulated earnings tax rate | 20% on excess accumulations | 2025 | IRC §531 |

> **Reasonable-compensation note:** the S-corp reasonable-comp figure is the
> single most audit-sensitive input in this tool. Treat any comp assumption as
> load-bearing and surface it in the memo.

## Reasonable compensation — BLS OEWS benchmarks

Source: BLS Occupational Employment and Wage Statistics (OEWS). Ranges are
national annual wage percentiles; adjust for locality and role. `as_of` May 2024
survey vintage unless noted. **Replace/extend with occupation rows relevant to
your practice.**

| Occupation (SOC) | 25th pct | Median | 75th pct | as_of | source |
|---|---|---|---|---|---|
| Management, general/operations (11-1021) | ~$75k | ~$116k | ~$180k | 2024 | BLS OEWS |
| Software developers (15-1252) | ~$100k | ~$133k | ~$170k | 2024 | BLS OEWS |
| Accountants & auditors (13-2011) | ~$62k | ~$81k | ~$106k | 2024 | BLS OEWS |
| Marketing managers (11-2021) | ~$100k | ~$158k | ~$205k | 2024 | BLS OEWS |
| Construction managers (11-9021) | ~$78k | ~$106k | ~$142k | 2024 | BLS OEWS |

## State data — depth states

Four states ship with depth. For any other state, ask the practitioner for these
same fields and offer to save the answers into Part 2.

### Delaware
| Field | Value | as_of | source |
|---|---|---|---|
| Recognizes federal S election | Yes | 2025 | DE Div. of Revenue |
| Entity-level tax | Corporate income tax 8.7% (C corp); none at entity level for pass-throughs | 2025 | DE Code Title 30 |
| PTET available | Yes (elective) | 2025 | DE |
| Franchise tax / annual | Corp franchise tax (min ~$175, method-dependent, can be large); LLC/LP flat $300/yr | 2025 | DE Div. of Corporations |
| Formation fee | ~$90 (corp/LLC certificate) | 2025 | DE |
| Economic nexus (sales/use) | $100k sales OR 200 transactions (verify — DE has no general sales tax) | 2025 | — |
| Professional entity rules | PLLC / PA available | 2025 | DE |

### Texas
| Field | Value | as_of | source |
|---|---|---|---|
| Recognizes federal S election | Yes (no personal income tax; franchise/margin tax applies) | 2025 | TX Comptroller |
| Entity-level tax | Franchise ("margin") tax; no-tax-due threshold ~$2.47M revenue | 2025 | TX Tax Code Ch. 171 |
| PTET available | N/A (no personal income tax) | 2025 | — |
| Annual fee | Franchise tax report + Public Information Report | 2025 | TX |
| Formation fee | $300 (LLC/corp certificate of formation) | 2025 | TX SOS |
| Economic nexus (sales/use) | $500k Texas revenue | 2025 | TX Comptroller |
| Professional entity rules | PLLC / PC available | 2025 | TX BOC |

### Michigan
| Field | Value | as_of | source |
|---|---|---|---|
| Recognizes federal S election | Yes | 2025 | MI Treasury |
| Entity-level tax | Corporate income tax 6.0% (C corp) | 2025 | MI |
| PTET available | Yes (flow-through entity tax, elective) | 2025 | MI Treasury |
| Annual fee | LLC annual statement $25; corp annual report $25 | 2025 | MI LARA |
| Formation fee | LLC $50; corp $60 (+authorized-shares fees) | 2025 | MI LARA |
| Economic nexus (sales/use) | $100k sales OR 200 transactions | 2025 | MI |
| Professional entity rules | PLLC / PC available | 2025 | MI |

### New York
| Field | Value | as_of | source |
|---|---|---|---|
| Recognizes federal S election | Yes, but **separate NY S election required** (Form CT-6) | 2025 | NY DTF |
| Entity-level tax | Corporate franchise tax; NYC has its own regime (incl. NYC treatment of S corps) | 2025 | NY Tax Law |
| PTET available | Yes (NY PTET, elective; NYC PTET separately) | 2025 | NY DTF |
| Annual fee | LLC filing fee $25–$4,500 by NY-source gross income | 2025 | NY DTF |
| Formation fee | LLC $200 (+publication requirement); corp $125 | 2025 | NY DOS |
| Economic nexus (sales/use) | $500k sales AND 100 transactions | 2025 | NY DTF |
| Professional entity rules | PLLC / PC available | 2025 | NY |

---

# PART 2 — USER-MAINTAINED SECTION

*A skill update will not touch anything below this line. Put your own data,
firm positions, and settings here.*

## Behavior settings

```yaml
challenge_level: medium        # low | medium | high
# How hard the skill pushes back when you disagree with its analysis.

confidence_threshold: medium   # low | medium | high
# How marginal a case must be before the recommendation is withheld.
```

**Safety floor (cannot be suppressed by the settings above):**
reasonable-compensation sensitivity, unsettled positions, economic-nexus
threshold crossings, and load-bearing unverified inputs surface at every setting.

## My additional states

*(Ask the practitioner for these fields when a non-depth state comes up, then
save here.)*

| State | Recognizes S election | Entity-level tax | PTET | Annual fee | Formation fee | Economic nexus | Professional entity | as_of | source |
|---|---|---|---|---|---|---|---|---|---|
| | | | | | | | | | |

## Firm positions & practice traps

- *(e.g., "We do not recommend series LLCs for clients operating outside TX/DE.")*
- *(e.g., reasonable-comp study vendor and method the firm standardizes on.)*
