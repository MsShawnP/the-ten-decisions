---
title: "feat: Produce Ten Decisions Manifesto and Exec Summary"
status: completed
created: 2026-05-27
origin: docs/brainstorms/ten-decisions-requirements.md
---

# feat: Produce Ten Decisions Manifesto and Exec Summary

**Origin:** `docs/brainstorms/ten-decisions-requirements.md`  
**Depth:** Deep  
**Created:** 2026-05-27

---

## Problem Frame

A specialty food consulting practice has 10 shipped portfolio pieces — tools,
case studies, audits, and diagnostics — with no organizing framework explaining
what the practice does or why the pieces belong together. A prospect landing on
the portfolio sees individual tools but not a coherent thesis.

This plan produces two Quarto documents that serve as the intellectual capstone:

- **`manifesto.qmd`** → `dist/the-ten-decisions-manifesto.pdf` (~4,000 words): a deeply argued PDF manifesto covering ten decisions growing specialty food brands make blind, with the Cinderhaven Provisions composite case study woven through each section.
- **`exec-summary.qmd`** → `dist/the-ten-decisions-exec-summary.pdf` (~1,000 words): a flowing prose exec summary for the homepage's above-the-fold content.

**Success criteria (from origin):**
- One qualified C-suite person at a specialty food brand reads and engages with the manifesto
- The piece passes the "voice check" — a C-suite reader reports no sentence sounds like a consultant pitching them

---

## Output Structure

```
the-ten-decisions/
├── _quarto.yml                               ← Chromium PDF engine, dist/ output
├── lailara.scss                              ← Lailara design system theme
├── fonts/
│   ├── playfair-display-700.woff2
│   ├── playfair-display-400.woff2
│   ├── source-sans-3-400.woff2
│   └── source-sans-3-600.woff2
├── manifesto.qmd                             ← ~4,000-word manifesto
├── exec-summary.qmd                          ← ~1,000-word exec summary
├── research/
│   ├── cinderhaven-findings.md               ← Extracted from 10 portfolio repos
│   └── decision-phrasings.md                 ← 10 CEO-language phrasings
└── dist/
    ├── the-ten-decisions-manifesto.pdf       ← Distributable
    └── the-ten-decisions-exec-summary.pdf   ← Distributable
```

---

## Key Technical Decisions

| Decision | Resolution | Rationale |
|---|---|---|
| PDF engine | Chromium (`pdf-engine: chromium`) | Lailara design system is CSS-based. LaTeX PDF engine does not support CSS or woff2 fonts. Chromium renders HTML→PDF with full CSS control. (see origin) |
| Fonts | Playfair Display + Source Sans 3, self-hosted woff2 | Required by Lailara design system. woff2 works with Chromium PDF. (see origin) |
| Canvas background in print | `#f5f3ee` with `print-color-adjust: exact` | **Intentional deviation from design system print rule** — the spec says revert to white in print, but this project requires warm canvas in PDF. This deviation is documented in `DECISIONS.md`. |
| CSS custom properties | All color tokens declared as CSS vars, referenced by name | Prevents Lailara drift. This project has no web frontend as a visual check — token drift only caught by inspection. Pattern from `product-data-health-audit/quarto/assets/report.css`. |
| Quarto container selectors | Target `main.content`, `#quarto-document-content` for max-width | Quarto wraps content in a constrained column. Must widen the container, not just the content inside it. (see learnings) |
| Cinderhaven framing | Explicit composite case study label on first mention | Never implies real client. (see origin) |
| Callout box style | Dark card — `background: #1a1a1a`, `color: #ffffff` | Named callout box per section: "Cinderhaven Provisions — Composite case study". |
| Exec summary structure | Flowing prose, no per-decision sections or callout boxes | At ~1,000 words, 10 sections would be too compressed to be meaningful. (see origin) |
| Cost table placement | Setup section, before Decision 1 | Front-loads credibility. Reader sees full $1.4M–$3.1M breakdown before first decision section. (see origin) |
| Commit message quoting | Heredoc pattern for any message containing `$` | PowerShell/bash variable expansion silently strips `$` in double-quoted strings. Use `git commit -m "$(cat <<'EOF' ... EOF)"`. (see learnings) |
| Decision 1 repo | `where-the-money-comes-from` | Requirements doc listed `retail-velocity-decision-tool` — corrected by repo scan. Actual directory is `where-the-money-comes-from`. |

---

## Existing Patterns to Follow

| Pattern | Source | Used in |
|---|---|---|
| CSS custom property tokens | `product-data-health-audit/quarto/assets/report.css` | U2 — `lailara.scss` |
| Quarto container selector targeting | `product-data-health-audit/quarto/assets/report.css` | U2 — `lailara.scss` |
| `_quarto.yml` project structure | `product-data-health-audit/quarto/_quarto.yml` | U2 — `_quarto.yml` (note: copy project structure only — LaTeX PDF settings do not transfer to Chromium) |
| Cinderhaven findings format | Existing portfolio repo outputs | U3 — `research/cinderhaven-findings.md` |

**Do not copy:** The PDF-specific settings from `product-data-health-audit/quarto/report.qmd` (LaTeX document class, tcolorbox, `\definecolor`, `\widowpenalty`) — these are LaTeX-specific and will break or be ignored by Chromium.

---

## Scope Boundaries

### In scope
- `manifesto.qmd`, `exec-summary.qmd`, `_quarto.yml`, `lailara.scss`, `fonts/`
- `research/cinderhaven-findings.md`, `research/decision-phrasings.md`
- `dist/the-ten-decisions-manifesto.pdf`, `dist/the-ten-decisions-exec-summary.pdf`

### Out of scope
- Homepage HTML/CSS/JS build (user handles separately)
- LinkedIn launch sequence (user handles separately)
- New Cinderhaven data or analysis (curate existing only)
- Multiple audience versions

### Deferred to Follow-Up Work
- DECISIONS.md entry for print CSS deviation (log during U2, not separately planned)
- `research/cinderhaven-findings.md` for decisions 1, 4, 5, 8 (edi-preflight, short-ship-cost, retail-readiness-scorecard, where-the-money-comes-from) — data exists in repos, will be extracted in U3

---

## Pre-Build Research: Known Cinderhaven Data

The following data points were extracted during planning and will seed `research/cinderhaven-findings.md` in U3. They do not need to be re-researched:

| Decision | Repo | Key finding |
|---|---|---|
| 2 — Product data | `product-data-health-audit` | Annual chargebacks from data defects: ~$5K/month run rate; GTIN/UPC failures in full catalog; label/barcode share of chargebacks = `data_defect_pct`%; fix time = `total_fix_hours` hours total |
| 3 — Deductions | `retailer-deduction-recovery` | $534,903.85/year; 16.52% recovery rate; 9,757 deductions never disputed ($1.02M); 12,604 labor hours = 6.06 FTE |
| 6 — Channel profitability | `channel-profitability-analysis` | Retailers retain 80–83¢/dollar; distributors retain 90¢/dollar; 3 margin points gap between best and worst retailer; Walmart largest by gross but not best by net margin % |
| 7 — Revenue lifecycle | `contract-to-cash` | 86.5¢ per dollar invoiced reaches cash; combined leakage $2.178M; B2B leakage 12.5%; time-to-cash 22–29 days |
| 9 — Launch economics | `cost-of-saying-yes` | Walmart 4-SKU case: Year 1 net = -$36,320; peak cash trough Month 4 = -$165,000; break-even Month 9; working capital required $165K |
| 10 — Weekly pulse | `monday-morning-report` | 12-week Cinderhaven example: cash position $1.5M–$2.5M; disputed AR declined from $195K to $88K over 12 weeks; recovered shelf position worth $80K–$150K annual velocity |

Repos still to research in U3: `where-the-money-comes-from` (Decision 1), `short-ship-cost` (Decision 4), `edi-preflight` (Decision 5), `retail-readiness-scorecard` (Decision 8).

---

## Implementation Units

### U1. PDF Engine Smoke Test

**Goal:** Confirm Chromium PDF rendering works end-to-end with Lailara fonts and canvas background before any real work begins. Twenty minutes that prevent a half-day redo.

**Requirements:** Validates the Chromium PDF pipeline before any SCSS work is invested (origin: PDF engine decision).

**Dependencies:** None.

**Files:**
- `test.qmd` (create, render, then delete)
- `_quarto.yml` (create minimal version for smoke test)

**Approach:**
- Create a minimal `_quarto.yml` with `format: pdf` and `pdf-engine: chromium`, `output-dir: dist`
- Create `test.qmd` with one paragraph, one heading, and a `div` with `background-color: #f5f3ee` and `print-color-adjust: exact` set inline
- Load one Playfair Display woff2 font via `@font-face` in an inline `<style>` block
- Run `quarto render test.qmd` from the terminal
- Inspect the rendered PDF: font renders correctly, canvas background is visible (not white), no Chromium errors in console
- On success: delete `test.qmd`. On failure: document the exact error and resolve before proceeding to U2.

**Test scenarios:**
- Smoke test — one-page PDF renders without error: `quarto render test.qmd` exits 0
- Font present — PDF heading uses Playfair Display (verify visually in the rendered PDF)
- Canvas background prints — `#f5f3ee` is visible in the PDF background (not white)
- `dist/test.pdf` is created at the expected output path

**Verification:** `dist/test.pdf` exists, opens, and shows correct font and background color. If any of the three checks fail, do not proceed — document the failure in `FAILURES.md` and resolve it first.

---

### U2. Quarto Project Structure + Lailara Theme

**Goal:** A working Quarto project with both target documents rendering cleanly using the Lailara design system — correct fonts, canvas background, dark callout box style, and page break rules.

**Requirements:** Foundation for all writing units. Must be complete before any `.qmd` content is added. (see origin: Technical Specification)

**Dependencies:** U1 (smoke test passed).

**Files:**
- `_quarto.yml` (full project config)
- `lailara.scss` (Lailara design system theme)
- `fonts/playfair-display-700.woff2`
- `fonts/playfair-display-400.woff2`
- `fonts/source-sans-3-400.woff2`
- `fonts/source-sans-3-600.woff2`
- `manifesto.qmd` (skeleton — title, author, date, one placeholder section)
- `exec-summary.qmd` (skeleton — title, author, date, one placeholder section)

**Approach:**

*`_quarto.yml`:*
- `project: type: default`, `output-dir: dist`
- `format: pdf` with `pdf-engine: chromium`
- Reference `lailara.scss` as the CSS theme
- `execute: echo: false`
- Page size: US Letter; margins: 0.6in per Lailara print spec

*`lailara.scss`:*
- Declare all color tokens as CSS custom properties (pattern from `product-data-health-audit/quarto/assets/report.css`) — never repeat hex values inline
- **Do not** include `@media print { background-color: #ffffff; }` — intentional deviation from the design system print rule (document in DECISIONS.md)
- Add `print-color-adjust: exact; -webkit-print-color-adjust: exact` on both `html` and `body`
- Target `main.content` and `#quarto-document-content` for the 900px max-width constraint (not just `body` or figure elements)
- Typography: Playfair Display for all headings (H1–H3), Source Sans 3 for body, labels, footnotes
- `@font-face` declarations for all four woff2 files in `fonts/`
- Dark card callout block style: `.callout-cinderhaven { background: #1a1a1a; color: #ffffff; padding: 16px; border-radius: 2px; page-break-inside: avoid; }`
- Decision section style: `section.decision { page-break-inside: avoid; }` (or equivalent Quarto div class)
- Body text: 17px, `line-height: 1.6`, `max-width: 660px` for prose columns
- Running footer: Source Sans 3 9pt, `#595959` (Lailara print spec)

*Font files:*
- Download woff2 files from Google Fonts or equivalent; place in `fonts/`
- Do not use Google Fonts CDN (Lailara spec: self-host)

*Skeleton `.qmd` files:*
- `manifesto.qmd`: YAML frontmatter with title, date, format reference; one `## Placeholder` section
- `exec-summary.qmd`: same

*After U2:* Log the print CSS deviation (intentional override of design system print rule) to `DECISIONS.md` before proceeding.

**Patterns to follow:** `product-data-health-audit/quarto/assets/report.css` for CSS token structure and Quarto container selectors.

**Test scenarios:**
- `quarto render manifesto.qmd` produces `dist/manifesto.pdf` with no errors
- `quarto render exec-summary.qmd` produces `dist/exec-summary.pdf` with no errors
- Playfair Display renders for H1 heading in both PDFs (verify visually)
- Source Sans 3 renders for body text (verify visually)
- Canvas background `#f5f3ee` is visible in both PDFs (not white)
- A test callout div with class `.callout-cinderhaven` renders with dark background and white text
- Max-width is respected — body text does not span the full page width
- Page breaks: a second `## Section` heading appears on a new page (not orphaned)

**Verification:** Both skeleton `.qmd` files render to `dist/` with correct fonts, background, and page layout. No default Quarto styling visible.

---

### U3. Research: Collect Cinderhaven Findings from All 10 Repos

**Goal:** A complete `research/cinderhaven-findings.md` with one entry per decision — specific dollar figure, key finding in one sentence, and source repo/file — ready to populate the ten callout boxes.

**Requirements:** Callout boxes must contain specific, traceable dollar figures (see origin: Cinderhaven Framing Rules). No new data created — curate only.

**Dependencies:** U1 (can run in parallel with U2 — research requires no rendered output).

**Files:**
- `research/cinderhaven-findings.md` (create)

**Approach:**

Six of the ten data points are already known from planning research (see "Pre-Build Research: Known Cinderhaven Data" above). Read the following repos to extract the remaining four:

| Decision | Repo to read | What to find |
|---|---|---|
| 1 — SKU decisions | `where-the-money-comes-from` | SKU performance finding — which SKUs paid for payroll, velocity spread, underperformer cost |
| 4 — Fulfillment | `short-ship-cost` | OTIF failure cost, short ship cost, lost shelf / repeat order impact |
| 5 — EDI | `edi-preflight` | Chargeback count or dollar tied to EDI errors, pre-flight failure rate |
| 8 — Retail readiness | `retail-readiness-scorecard` | Scorecard score, which readiness dimension failed, what it cost |

For each finding, record in `research/cinderhaven-findings.md`:
```
## Decision [N]: [name]
**Source repo:** [repo name], [file path]
**Dollar figure:** [exact amount]
**Finding:** [one sentence, in CEO language]
**Before/After (if available):** [what changed with the framework]
```

Use fictional retailer chain names throughout (Southside Grocers, Green Basket Market, Prairie Provisions, Mountain Pantry Co, Harbor Fresh). Whole Foods appears directly. Do not use real retailer names for the fictional chains.

**Test scenarios:**
- `research/cinderhaven-findings.md` has exactly 10 entries, one per decision
- Every entry has a specific dollar figure (no vague ranges without a number)
- Every entry has a source repo and file path
- No entry uses language implying a real client ("our client," "a brand we worked with")

**Verification:** File exists; 10 entries; each passes: "specific dollar figure present AND source file cited."

---

### U4. Draft Ten CEO-Language Decision Phrasings

**Goal:** Ten one-sentence decision questions in exact CEO language, ready to use as section headers, confirmed against the "Would a CEO say this out loud in a board meeting?" test.

**Requirements:** These are the section headers and the core creative work. All writing depends on them being right. (see origin: Note on phrasings)

**Dependencies:** U3 (phrasings should be grounded in the actual Cinderhaven findings).

**Files:**
- `research/decision-phrasings.md` (create)

**Approach:**

Starting point: the ten phrasings from `docs/brainstorms/ten-decisions-requirements.md`. For each, apply the test: Does this sound like something a CEO would say at their kitchen table at 6am, not in a board deck? Revise any that feel like consultant framing.

Common failure patterns to catch:
- Passive constructions ("Are our data systems aligned with...")
- Jargon ("operational cadence," "channel optimization," "data hygiene")
- Overly formal questions a CEO would never say aloud

Record all ten in `research/decision-phrasings.md` with:
- The final phrasing
- Whether it was revised from the brief's version (and why)

**Test scenarios:**
- 10 phrasings exist in `research/decision-phrasings.md`
- Read each phrasing aloud — it must sound natural, not formal
- No phrasing contains consulting jargon (flag any with "leverage," "optimize," "align," "cadence," "hygiene," "infrastructure" — these are the failure words)
- Each phrasing is a question, not a statement

**Verification:** All 10 phrasings pass the read-aloud test. Any revisions from the brief are noted with rationale.

---

### U5. Write Manifesto Frame (Cold Open + Setup + Close + CTA)

**Goal:** The structural backbone of the manifesto — cold open, setup with aggregate cost table and cascade framing, close, and CTA — as standalone prose in `manifesto.qmd`.

**Requirements:** Frame must include the aggregate cost table and cascade framing. CTA routes to Retail Readiness Scorecard. (see origin: Document Structure: The Manifesto)

**Dependencies:** U4 (phrasings needed for the setup section to reference the ten decisions).

**Files:**
- `manifesto.qmd` (add frame sections — cold open, setup, close, CTA)

**Approach:**

*Cold open (~150 words):*
- Opens with the immediate recognition statement
- Establishes the $25M anchor and the "grew faster than your data systems" framing
- No setup, no context, no credentials — straight to the pain

*Setup (~300 words):*
- Introduces the aggregate cost number ($1.4M–$3.1M) immediately
- Presents the aggregate cost table (all 10 rows, source: origin)
- Makes the cascade / doom loop explicit as a paragraph (not a list): "Fulfillment failures trigger deduction spikes. Deduction spikes create cash gaps..." — this framing makes the aggregate feel inevitable, not inflated
- Introduces Cinderhaven Provisions on first mention: "To show what these frameworks actually surface, we built Cinderhaven Provisions — a composite case study brand modeled on real industry patterns at the $25M scale."

*Close (~150 words):*
- Restates the practice thesis without repeating the ten decisions verbatim
- "This is what we do. We build the decision infrastructure that growing specialty food brands need. Not dashboards. Not data for data's sake. Frameworks that turn your data into the ten operational decisions that determine whether you scale or stall."

*CTA (~50 words):*
- "Not sure where to start? Take the 5-minute Retail Readiness Assessment — it tells you which of these ten structural leaks is threatening your margin today."
- Plain URL/link to the Retail Readiness Scorecard

**Voice test:** Read every sentence aloud. Any sentence that sounds like it belongs in a consulting deck — not at a CEO's kitchen table — must be rewritten before this unit is complete.

**Test scenarios:**
- Cold open: no credentials, no setup, no preamble — pain is present in the first sentence
- Aggregate cost table renders correctly in the PDF (Quarto table Markdown)
- Cascade framing is a paragraph, not a bullet list
- Cinderhaven Provisions label on first mention: "composite case study"
- Close does not repeat the ten decisions verbatim
- CTA contains link to Retail Readiness Scorecard
- Word count: cold open + setup + close + CTA = 550–700 words

**Verification:** Frame renders in `manifesto.qmd` PDF. Word count within range. Voice test passed.

---

### U6. Write Manifesto Decisions 1–5 ("What You Have Today")

**Goal:** Five complete decision sections — SKU decisions, product data, deductions, fulfillment, EDI — each following the repeating section template, with Cinderhaven callout boxes populated from `research/cinderhaven-findings.md`.

**Requirements:** Each section: pain framing → cost of blindness ($25M anchor + tier callout) → Cinderhaven callout box → portfolio link. 300–500 words each. (see origin: Document Structure)

**Dependencies:** U2 (Lailara theme for callout box rendering), U3 (Cinderhaven data), U4 (final decision phrasings).

**Files:**
- `manifesto.qmd` (add Decision 1–5 sections)

**Approach:**

For each of the five decisions, follow the template exactly:

```
## [N]. [CEO-language phrasing from decision-phrasings.md]

[2–3 paragraphs pain framing]
  — Second person, present tense
  — One inline tier callout: "At $5M, [X]. At $25M, [Y]."

[1 paragraph cost of blindness — specific dollar figure from aggregate table]

::: {.callout-cinderhaven}
**Cinderhaven Provisions — Composite case study**

[40–80 words. The specific finding and dollar figure from cinderhaven-findings.md.
Before/after if available. No vague summaries.]
:::

→ [Portfolio piece name]: [one-phrase description]
```

Tier callout examples for these five decisions:
- Decision 1 (SKU): "At $5M, you know your top SKU because it's the one your broker calls about. At $25M, not knowing which SKUs are losing you shelf space costs $50K–$150K a year."
- Decision 3 (Deductions): "At $5M, a late deduction dispute is a bad Tuesday. At $25M, it's $180K–$350K in expired dispute windows."
- Decision 4 (Fulfillment): "At $5M, a short ship is a text message to your co-packer. At $25M, it's OTIF fines and canceled reorders."

**Voice test:** The five-sentence test for each section — would a CEO say every single one of these sentences? Not "does it sound professional" — does it sound like them, not you.

**Test scenarios:**
- All 5 sections present in `manifesto.qmd`, each with a heading matching `research/decision-phrasings.md`
- Each section contains exactly one callout block with `.callout-cinderhaven` class
- Each callout box has the label "Cinderhaven Provisions — Composite case study"
- Each callout box dollar figure traces back to a `research/cinderhaven-findings.md` entry
- Each section closes with a portfolio link in the `→ [name]: [description]` format
- Each section has exactly one tier callout inline
- Word count per section: 300–500 words
- PDF renders without callout box page breaks (callout must not split across pages)

**Verification:** Sections render in PDF. Callout boxes visible with dark background. Word count in range per section.

---

### U7. Write Manifesto Decisions 6–7 ("Seeing Clearly")

**Goal:** Two complete decision sections — channel profitability and revenue lifecycle — the "seeing clearly" arc that bridges operational decisions and forward-looking decisions.

**Requirements:** Same template as U6. These are the two highest-dollar decisions by leakage amount. (see origin)

**Dependencies:** U2, U3, U4.

**Files:**
- `manifesto.qmd` (add Decision 6–7 sections)

**Approach:**

Follow the same template as U6. Key callout data is already known from planning research:

- **Decision 6 (Channel Profitability):** Retailers retain 80–83¢/dollar; distributors retain 90¢/dollar; 3 margin points gap between best and worst retailer. Signature visual reference: per-unit contribution chart from `channel-profitability-analysis`.
- **Decision 7 (Revenue Lifecycle):** 86.5¢ per dollar invoiced reaches cash; combined leakage $2.178M; B2B leakage 12.5%. Signature visual reference: Sankey from `contract-to-cash`.

The signature visual callouts (Sankey, per-unit contribution chart) should be referenced in prose — "the per-unit contribution chart shows..." — since the PDF manifesto does not include interactive visuals. These are hooks for the homepage version.

**Test scenarios:**
- Both sections present, both callout boxes populated with specific dollar figures
- Decision 6 callout references the channel margin gap
- Decision 7 callout references the 86.5¢ per dollar figure or the $2.178M leakage
- Word count: 300–500 words each

**Verification:** Both sections render in PDF with correct callout box styling.

---

### U8. Write Manifesto Decisions 8–10 ("What's Next + Discipline")

**Goal:** Three complete decision sections — retail readiness, launch economics, and weekly pulse — closing the arc with the forward-looking and discipline decisions.

**Requirements:** Same template. Decision 10 must read as the natural close of the arc, not an afterthought. (see origin)

**Dependencies:** U2, U3, U4.

**Files:**
- `manifesto.qmd` (add Decision 8–10 sections)

**Approach:**

Follow the same template as U6/U7. Key callout data from planning research:

- **Decision 9 (Launch Economics):** Walmart Year 1 net = -$36,320; peak cash trough Month 4 = -$165,000; break-even Month 9. "Saying yes to Walmart without modeling it can mean funding a $165,000 cash hole for four months."
- **Decision 10 (Weekly Pulse):** Disputed AR declined from $195K to $88K over 12 weeks with a Monday morning dashboard in place. The weekly pulse decision is the closing of the arc — it's not about a one-time fix but about discipline that prevents all nine prior decisions from drifting back to blind.

**Decision 10 close note:** This section is the final decision section before the close and CTA. Its final paragraph should transition into the close — the sense that "with these ten frameworks in place, this is what the business looks like on a Monday morning." The section should not end abruptly.

**Test scenarios:**
- All 3 sections present with callout boxes and portfolio links
- Decision 9 callout references the $165K cash trough or the -$36,320 Year 1 net
- Decision 10 final paragraph transitions naturally to the close
- Word count: 300–500 words each

**Verification:** All 3 sections render. Arc narrative feels complete at Decision 10.

---

### U9. Assemble `manifesto.qmd` — Render and Word Count Check

**Goal:** Full `manifesto.qmd` assembled from frame + 10 decision sections + close/CTA. Clean PDF render. Word count 3,800–4,200 words. Arc coherent from cold open to close.

**Requirements:** Complete manifesto PDF ready for voice calibration. (see origin: Definition of done)

**Dependencies:** U5, U6, U7, U8.

**Files:**
- `manifesto.qmd` (complete — verify section order, word count, transitions)
- `dist/the-ten-decisions-manifesto.pdf` (rendered output)

**Approach:**

- Confirm section order: Cold open → Setup (with table) → Decisions 1–5 → Decisions 6–7 → Decisions 8–10 → Close → CTA
- Read through the assembled manifesto for arc coherence: does "diagnose → see clearly → decide → discipline" feel like a progression, not a list?
- Check transitions between arc sections (between Decision 5 and Decision 6, and between Decision 9 and Decision 10)
- Run word count — target 3,800–4,200 words total
- Render PDF: `quarto render manifesto.qmd`
- Inspect PDF: page count reasonable (~12–16 pages), callout boxes visible, no orphaned headings, no broken table

**Test scenarios:**
- `quarto render manifesto.qmd` exits 0 with no errors
- `dist/the-ten-decisions-manifesto.pdf` created
- Word count: 3,800–4,200 words (use `wc -w manifesto.qmd` or equivalent, accounting for YAML frontmatter)
- All 10 decision sections present in correct order
- All 10 callout boxes visible in PDF with dark background
- Aggregate cost table in Setup section (visible and formatted correctly)
- No Quarto rendering artifacts (broken images, placeholder text, missing sections)

**Verification:** PDF opens cleanly. All 10 sections visible. Word count in range. Arc reads as: diagnose → see clearly → decide → discipline.

---

### U10. Write `exec-summary.qmd`

**Goal:** A ~1,000-word flowing prose exec summary — same thesis, same arc, no per-decision sections, no callout boxes — structured as an executive memo.

**Requirements:** Flowing prose argument. All ten decisions named and characterized. No Cinderhaven callout boxes. Aggregate number in cold open. (see origin: Document Structure: The Exec Summary)

**Dependencies:** U9 (exec summary is distilled from the complete manifesto).

**Files:**
- `exec-summary.qmd` (write complete content)
- `dist/the-ten-decisions-exec-summary.pdf` (rendered output)

**Approach:**

Structure:
```
[Cold open + thesis]     ~150 words — same cold open, aggregate number immediately
[Ten decisions named]    ~400 words — all ten named and briefly characterized,
                          flowing prose through four arcs, no headers
[Cascade framing]        ~150 words — doom loop made explicit
[Close + CTA]            ~150 words — same close compressed, Retail Readiness CTA
Total                    ~850–1,050 words
```

This is a distillation, not a compression. Every sentence earns its place. A reader who only reads this gets the full thesis and knows exactly what to do next.

The ten decisions are named in flowing prose — not as a list. Example:
> "The first five decisions are about what you have today: which SKUs are paying their way, whether your product data will survive the next retailer onboarding, how much revenue is being clawed back in deductions, whether operational failures are quietly killing repeat orders, and whether your EDI is generating chargebacks. Most brands at $25M are making all five blind."

No callout boxes. No tier callouts (maximum 1–2 in the entire document). No cost table — only the aggregate number.

**Test scenarios:**
- `quarto render exec-summary.qmd` exits 0 with no errors
- `dist/the-ten-decisions-exec-summary.pdf` created
- Word count: 950–1,050 words
- No subheadings per decision (flowing prose only)
- No Cinderhaven callout boxes
- All ten decisions named
- Aggregate cost number (`$1.4M–$3.1M`) present in cold open
- Retail Readiness Scorecard CTA present at close
- Read-through: a reader who only reads this document understands the full thesis and knows what to do next

**Verification:** PDF renders. Word count 950–1,050. No structural elements from the manifesto leaked in (no callout boxes, no per-decision headers).

---

### U11. CEO-Voice Calibration Edit (Both Documents)

**Goal:** Both documents pass the read-aloud test — no sentence sounds like a consultant pitching a CEO.

**Requirements:** Voice calibration is 80% of the value of this piece. (see origin: Voice Standards)

**Dependencies:** U9, U10.

**Files:**
- `manifesto.qmd` (edit pass)
- `exec-summary.qmd` (edit pass)

**Approach:**

Read both documents aloud. For every sentence that makes you think "this person is lecturing me" or "this sounds like a deck":
- Flag it
- Rewrite until it sounds like a peer who understands the business

Specific failure modes to hunt:
- Consulting jargon: "leverage," "drive value," "best-in-class," "unlock," "optimize," "align," "cadence," "hygiene," "infrastructure"
- Analyst-speak: "organizations should consider," "brands may benefit from," "this can potentially"
- Passive voice as a hedge: "it can be seen that," "there may be a risk of"
- Vague pain: "data challenges are common," "many brands face similar issues"
- Hedged findings: "this may potentially cost," "approximately in the range of"

The test is not "is this grammatically correct" — the test is "would the CEO reading this feel understood."

**Test scenarios:**
- Full read-aloud of both documents (can be done by the AI — read sentence by sentence, flag any that fail)
- Consulting jargon list check: none of the flagged words appear in non-quoted text
- Passive voice check: no sentences using passive voice as a hedge
- Specific dollar figure check: every cost claim has a specific number (no "significant cost")
- Direct address check: "you" is used throughout, not "companies" or "brands"

**Verification:** Both documents pass the read-aloud test. No flagged words remain. A C-suite reader has reviewed (or is scheduled to review) the manifesto draft.

---

### U12. Lailara Design System Styling Pass

**Goal:** Both documents render with the full Lailara design system applied correctly — no default Quarto styling visible.

**Requirements:** Lailara spec must be honored in the PDF output. (see origin: Technical Specification)

**Dependencies:** U9, U10. Can run in parallel with U11.

**Files:**
- `lailara.scss` (final pass — verify and correct any styling gaps discovered during content writing)

**Approach:**

Side-by-side check against the Lailara design system reference (`lailara-design-system/LAILARA_DESIGN_SYSTEM.md`):

| Element | Lailara spec | Check in PDF |
|---|---|---|
| H1/H2 headings | Playfair Display 700, `#0d0d0d` | Visually correct? |
| Body text | Source Sans 3 400, `#333333`, 17px, 1.6 line-height | Visually correct? |
| Background | `#f5f3ee` Canvas | Prints (not white)? |
| Callout box | `#1a1a1a` background, `#ffffff` text | Correct dark card? |
| Max-width | 900px content, 660px prose | Not spanning full page? |
| Footer | Source Sans 3 9pt, `#595959` | Present? Correct style? |
| Border radius | 2px | No pill shapes or sharp corners? |

For any element that does not match: fix in `lailara.scss` and re-render to verify.

**Test scenarios:**
- Side-by-side comparison of rendered PDF against spec for all elements in the table above
- No Bootstrap, Cosmo, or default Quarto theme colors visible
- All 10 callout boxes render with correct dark card style
- Page numbers present in footer (Lailara print spec: right-aligned, Source Sans 3 9pt)
- Canvas background `#f5f3ee` visible on all pages

**Verification:** All elements in the check table pass. No default Quarto styling visible.

---

### U13. Final Render + Word Count + Distributable PDFs

**Goal:** Both `.qmd` files render cleanly to final distributable PDFs in `dist/`, correctly named, ready to hand off.

**Requirements:** Both PDFs are the final artifacts that will be hosted for download. (see origin: Definition of done)

**Dependencies:** U11, U12.

**Files:**
- `dist/the-ten-decisions-manifesto.pdf` (final render)
- `dist/the-ten-decisions-exec-summary.pdf` (final render)
- `_quarto.yml` (confirm `output-dir: dist` and correct naming)

**Approach:**

- Configure `_quarto.yml` so that rendered PDFs use the final distributable names (`the-ten-decisions-manifesto.pdf`, `the-ten-decisions-exec-summary.pdf`) rather than the `.qmd` filename defaults
- Run clean renders of both documents
- Verify word counts
- Inspect both PDFs for any remaining rendering artifacts (broken tables, orphaned headings, clipped callout boxes, missing pages)
- Commit both PDFs to `dist/` with a commit message using the heredoc pattern (dollar signs in commit messages require this on Windows — see Key Technical Decisions)

**Test scenarios:**
- `quarto render manifesto.qmd` produces `dist/the-ten-decisions-manifesto.pdf`
- `quarto render exec-summary.qmd` produces `dist/the-ten-decisions-exec-summary.pdf`
- Manifesto word count: 3,800–4,200 words
- Exec summary word count: 950–1,050 words
- Both PDFs: no rendering artifacts, no placeholder text, no broken formatting
- Both PDFs: open in standard PDF viewer without error
- `dist/` contains exactly two PDF files with the correct names

**Verification:** Both PDFs are in `dist/`, correctly named, open cleanly, and word counts are within range. Committed to git.

---

## Dependency Graph

```
U1 (smoke test)
│
├── U2 (Quarto structure + Lailara theme)
│   └── [dependency for all content writing — must complete before U5–U10]
│
└── U3 (Cinderhaven research)  ← can run in parallel with U2
    └── U4 (decision phrasings)
        ├── U5 (manifesto frame)
        ├── U6 (decisions 1–5)     ← also depends on U2
        ├── U7 (decisions 6–7)     ← also depends on U2
        └── U8 (decisions 8–10)    ← also depends on U2
            └── U9 (assemble manifesto)
                └── U10 (exec summary)
                    └── U11 (voice edit) ──┐
                        U12 (styling pass) ─┤ both depend on U9 + U10
                                           └── U13 (final PDFs)
```

**Parallel opportunities:**
- U2 and U3 can run in parallel (research doesn't require a rendered Quarto theme)
- U11 and U12 can run in parallel (voice edit and styling pass are independent)
- U5 (frame) can begin as soon as U4 is done, without waiting for U2 if working on content only (U2 is needed for callout box rendering, not for writing prose)

---

## Risks and Mitigations

| Risk | Likelihood | Mitigation |
|---|---|---|
| Chromium PDF engine produces unexpected layout | Medium | U1 smoke test catches this before any SCSS investment. U2 done-when criteria include explicit callout box and page break checks. |
| Canvas background reverts to white in PDF | High (common Chromium print issue) | `print-color-adjust: exact` in `lailara.scss`. Explicitly checked in U2 and U12. |
| Lailara token drift (wrong hex values) | Medium | CSS custom properties declared once and referenced by name — never inline hex. Pattern enforced in U2. |
| Voice calibration fails | Medium | External C-suite reader check in U11. Read-aloud test is explicit step, not optional. |
| Cinderhaven data missing for 4 repos | Low | Pre-build research confirmed 6/10. U3 has specific guidance on what to find in the remaining 4. |
| Dollar signs in commit messages silently stripped | High (known Windows issue) | Heredoc pattern required for any commit with $ amounts. Noted in Key Technical Decisions. |
| Decision 1 repo name | Resolved | `where-the-money-comes-from`, not `retail-velocity-decision-tool`. Confirmed by repo scan. |

---

## Deferred Implementation Notes

- Exact CSS selector names for Quarto's HTML structure (e.g., whether `main.content` or `#quarto-document-content` is the right container target for this Quarto version) — verify by inspecting rendered HTML output during U2, not before
- Exact word counts per section (target ranges given; actuals will vary slightly during writing)
- Whether `research/decision-phrasings.md` requires revisions to any of the ten phrasing from the brief — determined during U4
- Exact portfolio URLs for the "→ [Portfolio piece]:" links in each section — confirm live URLs before U13 final render
