# the-ten-decisions — Current Work Plan

The current arc of work. Updated when the arc changes, not every
session. For session-by-session state, see HANDOFF.md.

---

## Goal — 2026-05-27 (/clarify confirmed)

Produce two Quarto documents — a ~4,000-word PDF manifesto and a 1,000-word
homepage executive summary — that position the specialty food consulting
practice around ten decisions growing brands make blind, woven through with
Cinderhaven findings from all ten shipped portfolio pieces.

## Why this arc, why now

All 10 portfolio pieces are shipped. The build constraint is cleared.
This is the capstone that transforms a portfolio of individual tools into
a coherent practice with a thesis — and it's the primary conversion asset
for every inbound prospect.

## Business question this arc answers

Does a prospect land on the portfolio and immediately understand the full
scope, thesis, and value of the practice — and know exactly where to start?

## Tasks

Work in vertical slices — complete each artifact end-to-end before moving
to the next.

**Phase 1 — Workflow gates (Heavy tier)**
- [x] /clarify — 95% confidence on scope and requirements ✓ 2026-05-27
- [x] /office-hours — Cinderhaven framing resolved ✓ 2026-05-27
- [x] /plan-ceo-review — product gate passed ✓ 2026-05-27
- [x] /plan-eng-review — architecture gate passed ✓ 2026-05-27

**Phase 2 — Content development**
- [x] /ce:brainstorm — produce the full spec document ✓ 2026-05-27
- [x] /ce:plan — detailed implementation plan with task breakdown ✓ 2026-05-27
- [x] Research: pull Cinderhaven findings from all 10 shipped repos ✓ 2026-05-27
- [x] Draft manifesto (~4,000 words, 10 decision sections × 300–500 words each) ✓ 2026-05-27
- [x] Draft exec summary (1,000 words, tight thesis distillation) ✓ 2026-05-27
- [x] Edit pass: pacing, vocabulary, CEO-voice calibration ✓ 2026-05-27
- [x] Quarto formatting: Lailara design system applied, PDF renders cleanly ✓ 2026-05-27
- [x] /ce:review — reviewer ensemble on final drafts ✓ 2026-05-27
- [ ] Fix pass: implement Tier 1 + Tier 2 review findings (11 edits, see HANDOFF.md)

## Out of scope

- Homepage HTML/CSS/JS build (user builds this themselves)
- LinkedIn launch sequence (user does this themselves)
- Conference talk structure (explicitly ruled out)
- SEO optimization beyond basic
- CRM or lead management
- Full brand identity work
- New Cinderhaven data or analysis (curate and connect only — no new data)

## Definition of done

- [x] `manifesto.qmd` renders to clean PDF, ~4,000 words — 3,828 words, 13 pages ✓
- [x] `exec-summary.qmd` renders to clean PDF/HTML, exactly ~1,000 words — 1,049 words, 4 pages ✓
- [x] Every decision section includes: pain framing, cost of blindness
      (anchored $25M with tier callouts), Cinderhaven finding, portfolio link ✓
- [x] Voice calibration check passed: reads as CEO-direct, not consultant-speak ✓
- [x] Lailara design system applied: Playfair Display headings, Source Sans 3
      body, canvas background, correct type scale ✓
- [x] /ce:review complete — 11 findings delivered (4 Tier-1, 7 Tier-2) ✓ 2026-05-27
- [ ] Fix pass: Tier 1 + Tier 2 edits implemented and re-rendered
- [x] HANDOFF.md updated, committed, pushed ✓
- [ ] Success metric logged: one qualified C-suite prospect at a specialty
      food brand visits and reviews the manifesto

---

## Decomposition: Content development (Phase 2)

Goal: Produce two polished Quarto documents — a ~4,000-word PDF manifesto and a
~1,000-word exec summary — that are CEO-voice calibrated, Lailara-styled, and
woven through with specific Cinderhaven findings from all 10 shipped repos.

---

### Phase A — Foundation

- [x] **A0: PDF engine smoke test** *(pre-A1, ~20 min)*
    - Depends on: Phase 1 workflow gates complete
    - What: Create a one-page `test.qmd` with `pdf-engine: chromium` in
      `_quarto.yml`. Load one Lailara font (Playfair Display woff2) and
      set `background-color: #f5f3ee` with `print-color-adjust: exact`.
      Render to PDF and confirm: correct font renders, canvas background
      prints (not white), no Chromium errors.
    - Done when: `quarto render test.qmd` produces a one-page PDF with
      correct font and canvas background visible. Delete test.qmd after.
    - **Why first:** Catches the wrong PDF engine assumption in 20 minutes
      rather than after a half-day of SCSS work.

- [x] **A1: Set up Quarto project structure + Lailara theme**
    - Depends on: Phase 1 workflow gates complete
    - What: Create `manifesto.qmd`, `exec-summary.qmd`, `_quarto.yml`,
      `lailara.scss`, and `research/` directory. Translate Lailara brand
      design kit tokens into Quarto's SCSS system — Playfair Display headings,
      Source Sans 3 body, `#f5f3ee` canvas background, correct type scale,
      PDF-specific margins and print rules. Self-hosted fonts woff2 files.
      **Note: Lailara Quarto theme has not been built before. Size as a
      half-day task, not a quick setup.**
    - Done when: `quarto render manifesto.qmd` produces a PDF with correct
      fonts, canvas background visible (not white), page breaks clean across
      sections, and no default Quarto styling visible. Print CSS includes
      `print-color-adjust: exact` and `page-break-inside: avoid` on sections.

- [x] **A2: Research — collect Cinderhaven findings from all 10 repos**
    - Depends on: A1
    - What: Read each of the 10 shipped portfolio repos, extract the specific
      Cinderhaven data point(s) for each decision: the dollar amount, the
      finding, the before/after. Write to `research/cinderhaven-findings.md`.
    - Done when: `research/cinderhaven-findings.md` has one entry per decision
      with: (1) the specific cost figure, (2) the finding in one sentence,
      (3) the source repo/file. No vague summaries — exact numbers only.

---

### Phase B — Raw material

- [x] **B1: Draft the ten CEO-language decision phrasings**
    - Depends on: A2
    - What: Write (or refine from the brief) the exact one-sentence question
      for each decision — in the language a CEO would use, not consultant-speak.
      These are the section headers and the core creative work.
    - Done when: 10 phrasings exist in `research/decision-phrasings.md`,
      each passes the test: "Would a CEO say this out loud in a board meeting?"
      If any feel like consultant-speak, rewrite before moving on.

---

### Phase C — Draft manifesto

- [x] **C1: Write the manifesto frame**
    - Depends on: B1
    - What: Cold open, setup paragraph (aggregate cost, cascade framing),
      and close + CTA (~500–700 words total, not counting decision sections).
    - Done when: The frame prose exists as a standalone block; the "doom loop"
      cascade is made explicit; the close lands on Retail Readiness Scorecard CTA.

- [x] **C2: Write manifesto decisions 1–5** ("what you have today")
    - Depends on: A2, B1
    - What: Five sections — SKU decisions, product data, deductions, fulfillment,
      EDI. Each: pain framing → cost of blindness (anchored $25M with tier callout)
      → Cinderhaven finding → one-line portfolio link. ~300–500 words per section.
    - Done when: All 5 sections exist with no placeholder text; every section
      has a specific dollar figure traceable to `cinderhaven-findings.md`.

- [x] **C3: Write manifesto decisions 6–7** ("seeing clearly")
    - Depends on: A2, B1
    - What: Two sections — channel profitability (Where the Money) and
      revenue lifecycle (Contract-to-Cash). Same structure as C2.
    - Done when: Both sections complete, Sankey and per-unit chart references
      woven in as signature visual callouts.

- [x] **C4: Write manifesto decisions 8–10** ("what's next + discipline")
    - Depends on: A2, B1
    - What: Three sections — retail readiness, launch economics, Monday morning
      report. Decision 10 closes the arc. Same structure as C2.
    - Done when: All 3 sections complete; Decision 10 reads as the natural
      close of the arc, not an afterthought.

- [x] **C5: Assemble `manifesto.qmd`**
    - Depends on: C1, C2, C3, C4
    - What: Combine frame + all 10 decision sections into one `.qmd` file.
      Check total word count, section flow, narrative arc coherence.
    - Done when: `quarto render manifesto.qmd` produces a clean PDF;
      word count is 3,800–4,200 words; arc reads as: diagnose → see clearly
      → decide → discipline.

---

### Phase D — Exec summary

- [x] **D1: Write `exec-summary.qmd`**
    - Depends on: C5
    - What: Distill the manifesto to ~1,000 words. Same thesis, same arc,
      same voice — but every sentence earns its place. No section feels missing;
      no sentence feels padded.
    - Done when: `quarto render exec-summary.qmd` produces a clean PDF/HTML;
      word count is 950–1,050 words; a reader who only reads this gets the
      full thesis and knows exactly what to do next.

---

### Phase E — Polish

- [x] **E1: CEO-voice calibration edit** (both documents)
    - Depends on: C5, D1
    - What: Read both documents aloud. Flag any sentence that sounds like
      consulting jargon, analyst-speak, or marketing fluff. Rewrite until
      the entire piece sounds like a peer talking to a CEO.
    - Done when: No sentence remains that would make a CEO think "this person
      is lecturing me." Every cost figure is specific. Every pain point is
      something they've felt on a Tuesday morning.

- [x] **E2: Lailara design system styling pass**
    - Depends on: C5, D1
    - What: Verify `lailara.scss` correctly implements: Playfair Display for
      all headings, Source Sans 3 for body/labels, `#f5f3ee` canvas background,
      `#333333` body text, correct type scale from the design system reference,
      `900px` max-width, proper margins.
    - Done when: Both PDFs rendered side-by-side match the Lailara design
      system spec. No default Quarto styling visible.

- [x] **E3: Final render + word count check + distributable PDFs**
    - Depends on: E1, E2
    - What: Clean render of both documents. Word count verification. No
      formatting artifacts, broken references, or orphaned headings.
      Generate the final named PDFs that will be hosted and downloaded:
      `the-ten-decisions-manifesto.pdf` and `the-ten-decisions-exec-summary.pdf`.
      Commit both PDFs to `dist/`.
    - Done when: Both `.qmd` files render in one command with zero errors;
      manifesto is 3,800–4,200 words; exec summary is 950–1,050 words;
      both PDFs are in `dist/`, correctly named, ready to hand off to
      the homepage build.

---

**Start with:** A1 (Quarto setup) — no dependencies, sets the foundation
for everything else. But A1 is blocked until Phase 1 workflow gates pass.

---

## Arc history

When an arc completes, archive its goal, completion date, and outcome
here. Then start a new arc above. Provides continuity without bloating
the active plan.

### 2026-05-27 — Ten Decisions manifesto + exec summary
- Outcome: Both documents complete. manifesto.qmd 3,828 words / 13 pages; exec-summary.qmd 1,049 words / 4 pages. Distributable PDFs in dist/. Plan status = completed.
- Remaining: /ce:review + success metric log

### 2026-05-27 — Project foundation
- Outcome: Repo scaffolded, state files created, GitHub remote connected
- Tag: v0.1-foundation

---

## Improvement history

Track when this project was reviewed and improved via /improve.
Each entry records what was found, what was fixed, and when to
check again.

<!-- Entries are added by /improve — don't delete this section -->
