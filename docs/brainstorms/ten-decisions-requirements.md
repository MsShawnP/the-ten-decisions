# Requirements: The Ten Decisions — Manifesto & Exec Summary

**Status:** Approved  
**Date:** 2026-05-27  
**Workflow gates passed:** /clarify, /office-hours, /plan-ceo-review, /plan-eng-review, /ce:brainstorm  
**Next step:** /ce:plan

---

## What We're Building

Two Quarto documents that serve as the intellectual capstone of a specialty food
consulting practice. The documents position the practice around ten critical
operational decisions that growing specialty food brands ($3M–$50M revenue) make
blind — and quantify what that costs them.

**Artifact 1 — The Manifesto** (`manifesto.qmd` → `the-ten-decisions-manifesto.pdf`)  
~4,000-word long-form argument. Downloadable PDF. Establishes the practice's
intellectual positioning. Each of ten decisions gets 300–500 words: pain framing,
cost of blindness, and a Cinderhaven Provisions case study illustration.

**Artifact 2 — The Exec Summary** (`exec-summary.qmd` → `the-ten-decisions-exec-summary.pdf`)  
~1,000-word flowing prose argument. The same thesis, delivered for a 3-minute
read. No per-decision sections. No Cinderhaven callout boxes. Structured as an
executive memo. Used as the homepage's above-the-fold content.

---

## Primary Audience

**Primary:** CEO / founder at specialty food brands, $3M–$50M revenue. The person
who recognizes themselves in "we grew faster than our data systems."

**Secondary:** COO, CFO (who recognize specific decisions as their problem), broker
(who shares it with brands they represent), board members.

**How they arrive:** Both warm (referral, broker intro) and cold (LinkedIn, search).
The two-artifact structure handles both: exec summary for cold readers, downloadable
PDF for warm/depth-seeking readers.

---

## Success Criteria

**Primary:** One qualified C-suite person at a specialty food brand reads and
engages with the manifesto. Not a download count — a real person.

**Secondary:** The piece passes the "voice check" — a current or former C-suite
person at a food brand reads a draft and reports that no sentence sounds like
a consultant pitching them.

---

## Scope Boundaries

### In scope
- `manifesto.qmd` — ~4,000-word PDF
- `exec-summary.qmd` — ~1,000-word PDF/HTML
- `lailara.scss` — Quarto theme implementing Lailara design system
- `_quarto.yml` — project configuration (Chromium PDF engine)
- `research/cinderhaven-findings.md` — extracted data from 10 shipped repos
- `research/decision-phrasings.md` — CEO-language phrasings for all 10 decisions
- `dist/` — final distributable PDFs

### Out of scope
- Homepage HTML/CSS/JS build (user handles)
- LinkedIn launch sequence (user handles)
- Conference talk structure (explicitly ruled out)
- New Cinderhaven data or analysis (curate existing only)
- Multiple audience versions (one manifesto, one exec summary)
- CRM, lead management, SEO strategy
- Full brand identity / logo work

---

## The Ten Decisions

These are the section headers of the manifesto, in CEO language. They form a
narrative arc: diagnose the present → see clearly → decide the future → discipline.

**Arc 1 — What you have today (Decisions 1–5)**

| # | Decision (CEO language) | Portfolio piece | Engagement |
|---|---|---|---|
| 1 | "Which SKUs should we keep, kill, or double down on?" | Velocity Decision Tool | Velocity & SKU Strategy Audit ($15K–$25K) |
| 2 | "Will our product data survive the next retailer onboarding?" | Product Data Health Audit, GTIN Validator | Product Data Health Audit ($15K–$25K) |
| 3 | "How much of our top-line revenue is being clawed back — and can we fight it?" | Retailer Deduction Recovery | Deduction Recovery Diagnostic ($15K–$25K) |
| 4 | "Are operational bottlenecks quietly killing our repeat retailer orders?" | The 150 Cases | Fulfillment Impact Analysis ($15K–$25K) |
| 5 | "Is our EDI creating or preventing chargebacks?" | EDI Pre-flight | EDI Health Audit ($15K–$25K) |

**Arc 2 — Seeing clearly (Decisions 6–7)**

| # | Decision (CEO language) | Portfolio piece | Engagement |
|---|---|---|---|
| 6 | "Which channels actually make us money?" | Where the Money Actually Comes From | Channel Profitability Audit ($20K–$35K) |
| 7 | "Why does our bank account look empty when our sales pipeline looks full?" | Contract-to-Cash | Revenue Lifecycle Diagnostic ($20K–$35K) |

**Arc 3 — What's next (Decisions 8–9)**

| # | Decision (CEO language) | Portfolio piece | Engagement |
|---|---|---|---|
| 8 | "Are we ready if the next major retailer says yes?" | Retail Readiness Scorecard | Retail Readiness Audit ($10K–$25K) |
| 9 | "What does that retailer actually cost us in the first 12 months?" | Cost of Saying Yes | Retailer Launch Economics Model ($5K–$15K) |

**Arc 4 — Discipline (Decision 10)**

| # | Decision (CEO language) | Portfolio piece | Engagement |
|---|---|---|---|
| 10 | "What are the three numbers I need to see Monday morning?" | Founder Monday Morning Report | Monday Morning Report Setup ($3K–$8K) |

**Note on phrasings:** These are the starting point from the project brief. In
step B1, each phrasing must pass the "Would a CEO say this out loud in a board
meeting?" test before writing begins.

---

## Document Structure: The Manifesto

### Full structure

```
[Cold open]           ~150 words
[Setup]               ~300 words
  - Aggregate cost table (all 10 decisions)
  - Cascade framing ("doom loop")
[Decision 1]          ~350 words
[Decision 2]          ~350 words
[Decision 3]          ~350 words
[Decision 4]          ~350 words
[Decision 5]          ~350 words
[Decision 6]          ~350 words
[Decision 7]          ~350 words
[Decision 8]          ~350 words
[Decision 9]          ~350 words
[Decision 10]         ~350 words
[Close]               ~150 words
[CTA]                 ~50 words
───────────────────────────────
Total                 ~4,050 words
```

### The aggregate cost table (in Setup section)

Appears before Decision 1. Shows all ten decisions and their annual cost of
blindness at $25M revenue:

| Decision | Annual cost of blindness (at $25M) |
|---|---|
| SKU decisions blind | $50K–$150K |
| Product data not retail-ready | $25K–$100K |
| Deductions unrecovered | $180K–$350K |
| Fulfillment failures unquantified | $200K–$500K |
| EDI creating chargebacks | $25K–$50K |
| Channel profitability invisible | $300K–$500K |
| Revenue going dark between systems | $400K–$750K |
| Retailer launch unplanned | $200K–$750K |
| Retailer costs unmodeled | Entire slotting investment at risk |
| No weekly pulse | Compounds all above — caught 6–12 weeks late |
| **Total** | **$3.1M–$4.6M** |

### The cascade framing (in Setup section)

Immediately after the table, the cascade / "doom loop" must be made explicit.
Not a list of independent problems — a reinforcing loop:

> Fulfillment failures trigger deduction spikes. Deduction spikes create cash
> gaps. Cash gaps force understaffing. Understaffing causes more fulfillment
> failures.

This framing makes the aggregate feel inevitable rather than inflated.

### The repeating decision section template

Each of the ten decisions follows this exact structure:

```
## [Decision number]. [CEO-language question]

[2–3 paragraphs: pain framing]
  - What it feels like from the inside
  - Second person, present tense
  - One inline tier callout: "At $5M, this is [X]. At $25M, it's [Y]."

[1 paragraph: cost of blindness]
  - Anchored at $25M revenue
  - Specific dollar range from the aggregate table
  - No vague language ("significant cost" → "$180K–$350K/year")

[Cinderhaven Provisions callout box]
  - Labeled: "Cinderhaven Provisions — Composite case study"
  - Contains: the specific finding, the specific number, before/after if applicable
  - 40–80 words maximum
  - Data sourced from research/cinderhaven-findings.md

[1 sentence: portfolio link]
  - Plain text link to the corresponding portfolio piece
  - Format: "→ [Portfolio piece name]: [one-phrase description of what it does]"
```

### The close

~150 words. No new information. Restates the practice thesis without repeating
the ten decisions verbatim.

> "This is what we do. We build the decision infrastructure that growing
> specialty food brands need. Not dashboards. Not data for data's sake.
> Frameworks that turn your data into the ten operational decisions that
> determine whether you scale or stall."

### The CTA

~50 words. Retail Readiness Scorecard as the default entry point. Self-segmentation
framing: the reader who doesn't know where to start is routed to the diagnosis tool.

> "Not sure where to start? Take the 5-minute Retail Readiness Assessment — it
> tells you which of these ten structural leaks is threatening your margin today."

---

## Document Structure: The Exec Summary

### Full structure

```
[Cold open + thesis]      ~150 words
  - Same cold open as manifesto
  - Aggregate number immediately
[The ten decisions named]  ~400 words
  - All ten decisions named and briefly characterized
  - No subheadings, no callout boxes
  - Flowing prose through the four-arc structure
[Cascade framing]         ~150 words
  - Doom loop made explicit
[Close + CTA]             ~150 words
  - Same close as manifesto, compressed
  - Retail Readiness Scorecard CTA
────────────────────────────
Total                     ~850–1,050 words
```

### Key structural differences from the manifesto

| Feature | Manifesto | Exec summary |
|---|---|---|
| Decision sections | 10 named sections with headers | Flowing prose, no per-decision headers |
| Cinderhaven callout boxes | Yes — in every decision section | No — narrative only |
| Cost table | Yes — in setup section | No — aggregate number in cold open only |
| Tier callouts | Inline in each section | 1–2 inline in the whole document |
| Length | ~4,000 words | ~1,000 words |
| Format | Subheadings + callout boxes | Continuous prose |

---

## Cinderhaven Framing Rules

Cinderhaven Provisions is a composite case study — a fictional $25M specialty food
brand built from synthetic data to illustrate what the ten frameworks reveal.

**Required on first mention (both documents):**
> "Cinderhaven Provisions — the composite case study brand we built to show what
> these frameworks actually surface..."

**In every callout box:**
Label must read: "Cinderhaven Provisions — Composite case study"

**Never use:**
- "our client"
- "a brand we worked with"
- "results from a recent engagement"
- Any language that implies a real client relationship

**Source:** Data for callout boxes comes from `research/cinderhaven-findings.md`,
populated from the 10 shipped portfolio repos. No new data is created.

---

## Voice Standards

**Register:** Economist-style. Sober, declarative, data-forward. Opinionated.

**Person:** Second person throughout. "You" not "companies" or "brands."

**Test for every sentence:** "Would a CEO say this out loud to their board?"

**Avoid:**
- Consulting jargon ("leverage," "drive value," "best-in-class," "unlock")
- Analyst-speak ("organizations should consider implementing...")
- Vague pain ("data challenges are common")
- Hedged findings ("this may potentially cost...")

**Embrace:**
- Operational specificity ("four separate spreadsheets")
- Named consequences ("expired dispute windows," "OTIF fines")
- Direct address ("If you can't tell which SKUs paid for your payroll last
  month without opening four separate spreadsheets, you are operating blind.")
- Tier callouts that feel earned, not mechanical ("At $5M, this is a Friday
  afternoon text to your co-packer. At $25M, it's a $300K structural leak.")

---

## Technical Specification

### PDF engine
Chromium (`pdf-engine: chromium` in `_quarto.yml`). Full CSS and woff2 support.
Do not use LaTeX or Typst.

### Lailara design system (applied via `lailara.scss`)

| Element | Spec |
|---|---|
| Heading font | Playfair Display, woff2, self-hosted |
| Body font | Source Sans 3, woff2, self-hosted |
| Background | `#f5f3ee` (Canvas) — must print, not render white |
| Body text | `#333333` |
| Headings | `#0d0d0d` |
| Max-width | 900px |
| Callout box background | `#1a1a1a` (dark card) |
| Callout box text | `#ffffff` |
| Print CSS | `print-color-adjust: exact; -webkit-print-color-adjust: exact` |
| Page breaks | `page-break-inside: avoid` on decision sections |

### File structure

```
the-ten-decisions/
├── _quarto.yml
├── lailara.scss
├── fonts/
│   ├── playfair-display-700.woff2
│   ├── playfair-display-400.woff2
│   ├── source-sans-3-400.woff2
│   └── source-sans-3-600.woff2
├── manifesto.qmd
├── exec-summary.qmd
├── research/
│   ├── cinderhaven-findings.md
│   └── decision-phrasings.md
└── dist/
    ├── the-ten-decisions-manifesto.pdf
    └── the-ten-decisions-exec-summary.pdf
```

### Render command
```
quarto render manifesto.qmd
quarto render exec-summary.qmd
```
Both output to `dist/` (configured in `_quarto.yml`).

---

## Dependencies

All 10 portfolio repos must be readable to extract Cinderhaven findings:

| Repo | Decision |
|---|---|
| retail-velocity-decision-tool | Decision 1 — SKU |
| product-data-health-audit | Decision 2 — Product data |
| retailer-deduction-recovery | Decision 3 — Deductions |
| short-ship-cost (The 150 Cases) | Decision 4 — Fulfillment |
| edi-preflight | Decision 5 — EDI |
| channel-profitability-analysis | Decision 6 — Channel |
| contract-to-cash | Decision 7 — Revenue lifecycle |
| retail-readiness-scorecard* | Decision 8 — Readiness |
| cost-of-saying-yes* | Decision 9 — Launch economics |
| founder-monday-morning-report* | Decision 10 — Weekly pulse |

*Repo name to be confirmed in A2 (research pass).

---

## Key Decisions (already locked, do not re-litigate)

| Decision | Resolution |
|---|---|
| Form factor | Option B+ — manifesto-driven homepage |
| PDF engine | Chromium |
| Cinderhaven framing | Composite case study, explicitly labeled on first mention |
| Cinderhaven in sections | Named callout box with dark card styling |
| Aggregate cost presentation | Table in setup section, before Decision 1 |
| Exec summary structure | Flowing prose argument, no per-decision sections |
| Success metric | One qualified C-suite read and engagement |
| CTA | Retail Readiness Scorecard |
| Fonts | Playfair Display (headings) + Source Sans 3 (body), self-hosted woff2 |
| Stack | Quarto + Chromium + Lailara SCSS |
| Homepage build | Out of scope — user handles |
| LinkedIn sequence | Out of scope — user handles |
| Two audience versions | Rejected — two-artifact structure handles warm/cold split |
