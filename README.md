# The Ten Decisions — the operational blind spots costing growing specialty food brands $1.4M–$2.4M a year

> *Ten Decisions You're Making Blind — and What the Frameworks Look Like*

The flagship positioning piece for a specialty food consulting practice: a
long-form manifesto and a companion executive summary, written for founders and
CEOs of brands in the $3M–$50M revenue range, rendered to print-quality PDF
with Quarto.

## What it does

This project produces two documents:

- **`manifesto.qmd`** — the full manifesto (~4,000 words). Walks through ten
  operational decisions — SKU rationalization, product data readiness,
  deduction recovery, fulfillment failure tracking, EDI compliance, channel
  profitability, revenue lifecycle, retail readiness, launch economics, and
  weekly operational discipline — and quantifies what making each one without
  data costs at $25M revenue.
- **`exec-summary.qmd`** — a 1,000-word, 3-minute brief covering the same
  thesis for the quick-scan reader.

Both render to PDF (output in `dist/`) using the Lailara design system:
CSS-based theming (`lailara.scss`), web fonts, and a Chromium-based PDF
pipeline so the print output matches the web design exactly.

## Why it matters

This is the capstone of a consulting portfolio. Every other portfolio piece
(tools, case studies, audits, diagnostics) maps to one of the ten decisions;
this piece ties them into a single practice thesis a prospect can grasp in one
read.

**The thesis:** a specialty food brand at $25M revenue is likely leaving
$1.4M–$2.4M per year on the table across ten structural blind spots. Each
component figure is traceable to a specific framework and methodology — for
example, deductions unrecovered ($350K–$500K/yr) or fulfillment failures that
vanish from the records when the legacy system overwrites the original PO
quantity ($298K/yr).

The success metric is deliberately not a vanity metric: the piece exists to
make a qualified executive reader recognize their own blind spots and start a
conversation — not to collect page views.

## Quick start

Prerequisites: [Quarto](https://quarto.org) and
[pagedjs-cli](https://www.npmjs.com/package/pagedjs-cli) (the Chromium-based
PDF engine configured in `_quarto.yml`).

```bash
# Render both documents to PDF in dist/
quarto render

# Or render one document
quarto render manifesto.qmd
quarto render exec-summary.qmd
```

Pre-rendered PDFs are checked in under `dist/`
(`the-ten-decisions-manifesto.pdf`, `the-ten-decisions-exec-summary.pdf`).

## Tech stack

- **Quarto** — authoring and rendering (`.qmd` source, `_quarto.yml` config)
- **Paged.js (`pagedjs-cli`)** — Chromium-based PDF engine, so print output
  uses the same CSS as the web design system
- **SCSS** — `lailara.scss`, the Lailara design system theme, with bundled
  web fonts in `fonts/`

## Project structure

```
manifesto.qmd       Full manifesto (~4,000 words)
exec-summary.qmd    3-minute executive brief
_quarto.yml         Render config (PDF via pagedjs-cli)
lailara.scss        Design-system theme
fonts/              Bundled web fonts
research/           Source findings and phrasing notes behind the figures
dist/               Rendered PDFs
```

## License

MIT
