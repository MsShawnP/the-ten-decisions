# the-ten-decisions — Decisions Log

Permanent record of choices that should survive session turnover.
If a decision is reversed, strike it through and add the replacement
below — don't delete.

---

## Format

Each entry:
- **Date** — when decided
- **Decision** — one sentence, imperative voice
- **Why** — the reasoning, including what was tried and rejected
- **Scope** — what this applies to (file, chunk, deliverable, or "global")
- **Do not** — explicit anti-instructions, if any

---

## Architecture & Pipeline

### ~~2026-05-27 — Use `pdf-engine: chromium`~~ — SUPERSEDED
- **Superseded by:** "Use `pdf-engine: pagedjs-cli`" (see below, 2026-05-27)

### 2026-05-27 — Use `pdf-engine: pagedjs-cli` as the Quarto PDF engine
- **Why:** The Lailara design system is CSS-based (web fonts, hex color tokens,
  SCSS). Quarto's default LaTeX PDF engine does not support CSS or woff2 fonts.
  The spirit of the decision is "Chromium-based HTML→PDF with full CSS support"
  — the correct Quarto implementation is `pagedjs-cli`, not `chromium`. Quarto
  1.9.37 does not accept `chromium` as a `pdf-engine` value; valid CSS-capable
  engines are `weasyprint` and `pagedjs-cli`. WeasyPrint requires GTK3 libraries
  not installed on this Windows machine. `pagedjs-cli` uses headless Chrome
  (already installed) via Puppeteer and supports full CSS, woff2 fonts, CSS
  custom properties, and print-color-adjust. Confirmed working in A0 smoke test
  2026-05-27.
  **Windows note:** Quarto/pandoc's Haskell `findExecutable` only looks for `.exe`
  files on Windows. `pagedjs-cli` installs as a `.cmd` wrapper in the npm global
  bin. To make it findable, a C# wrapper `pagedjs-cli.exe` (4KB) was compiled at
  `C:\Users\mssha\AppData\Roaming\npm\pagedjs-cli.exe`. If this machine is replaced
  or npm is reinstalled, recompile the wrapper from `pagedjs-cli.cs` in the npm
  global bin directory.
- **Scope:** `_quarto.yml` — set `pdf-engine: pagedjs-cli` in format config
- **Do not:** Use the default LaTeX engine. Do not set `pdf-engine: chromium`
  (invalid in Quarto 1.9.x). Do not remove `pagedjs-cli.exe` without providing
  a replacement — pandoc cannot find the `.cmd` file.
- **Print CSS deviation:** `lailara.scss` intentionally does NOT include
  `@media print { background-color: #ffffff }` — the design system's default
  print rule is overridden here to preserve the warm canvas background in the
  PDF. `print-color-adjust: exact` is required on `html` and `body` to force
  Chromium/pagedjs-cli to print the background. Documented here — do not revert.

### 2026-05-27 — Defer stack selection until after /plan-eng-review
- **Why:** Stack is TBD per the project brief. The technical approach
  (static HTML/CSS/JS vs. Next.js vs. Quarto, etc.) should emerge from
  the /ce:brainstorm spec and be confirmed in /plan-eng-review — not
  chosen arbitrarily at scaffolding time.
- **Scope:** Global
- **Do not:** Write any code or install any packages before the stack
  decision is logged here with explicit rationale.

---

## Success Metric

### 2026-05-27 — Define success as a qualified prospect visit/review, not vanity metrics
- **Why:** This is a new business venture with no existing traffic baseline.
  Download counts and page views are unmeasurable and meaningless at launch.
  The right signal is a real C-suite person at a specialty food brand
  ($3M–$50M revenue) actually reading and engaging with the manifesto.
  One qualified review confirms the piece reached the right audience.
  Surfaced in /plan-ceo-review on 2026-05-27.
- **Scope:** Post-ship evaluation
- **Do not:** Optimize for vanity metrics (total downloads, page views, shares)
  before getting a single qualified read. A prospect who says "I read your
  ten decisions piece" is the signal.

---

## Cinderhaven Framing

### 2026-05-27 — Label Cinderhaven explicitly as a composite case study, not a real client
- **Why:** Cinderhaven data is synthetic — constructed to illustrate what the
  frameworks reveal, not real client results. Presenting specific dollar figures
  ($180K–$350K in deductions, etc.) without this framing implies validated client
  outcomes, which would mislead a sophisticated CFO and undermine the practice's
  credibility when discovered. The fix is simple and actually stronger: framing
  Cinderhaven as a composite demonstrates the *tool*, not just a result.
  Surfaced in /office-hours on 2026-05-27.
- **Scope:** Every reference to Cinderhaven in both manifesto and exec summary
- **Do not:** Use language that implies Cinderhaven is a real client ("our client,"
  "a brand we worked with," "results from a recent engagement"). Always use:
  "composite case study," "fictional brand built to illustrate," or similar.
  The explicit label must appear on first mention — not buried in a footnote.

---

## Product & Positioning

### 2026-05-27 — Use Option B+ form factor: manifesto-driven homepage
- **Why:** Resolved in the project brief. Option A (homepage only) is
  too shallow for a Tier 1 positioning piece. Option C (scroll-driven
  interactive) is a time-sink. The manifesto IS the intellectual capital.
- **Scope:** Global — this determines the entire deliverable structure
- **Do not:** Reconsider this unless at least two other pieces of evidence
  suggest it's wrong. The form factor decision is settled.

### 2026-05-27 — Two artifacts: homepage exec summary + downloadable PDF manifesto
- **Why:** Homepage features 1,000-word exec summary. Full manifesto is
  ~4,000 words, downloadable. Serves two buyer types: quick-scan prospect
  and depth-seeking buyer.
- **Scope:** Global

### 2026-05-27 — Anchor all margin math at $25M revenue with inline tier callouts
- **Why:** $25M is where the pain is most acute and the numbers are most
  defensible. Tier callouts (e.g., "At $5M this is a Friday annoyance;
  at $25M it's a $300K structural leak") make the piece relevant across
  the $3M–$50M range without losing specificity.
- **Scope:** All written content
- **Do not:** Use vague ranges without anchoring at $25M first.

### 2026-05-27 — Retail Readiness Scorecard is the default CTA
- **Why:** Every prospect needs a "what do I do first" answer. The
  scorecard diagnoses which of the ten decisions is most urgent.
- **Scope:** All CTA placements

### 2026-05-27 — Build this piece LAST in the portfolio sequence
- **Why:** The umbrella references all ten pieces. Dead links and
  "coming soon" placeholders undermine the entire positioning thesis.
  Hard minimum: 8 of 10 pieces shipped. Must-haves: Where the Money,
  Retail Readiness Scorecard, Cost of Saying Yes, and C2C or Deduction Recovery.
- **Scope:** Global — project sequencing decision

### 2026-05-27 — Include Enterprise Data Architecture Blueprint as meta-offering ($50K–$100K)
- **Why:** Anchors practice value high so individual $25K diagnostics
  feel like bargains. Serves enterprise buyers who want everything
  assessed at once. Does not cannibalize individual engagements.
- **Scope:** CTA section, pricing / engagement section

---

## Data & Schema

[Decisions about data sources, schemas, transformations — to be filled
during /ce:brainstorm and /ce:plan]

---

## Visualization

### 2026-05-27 — Each decision section gets exactly ONE signature visual
- **Why:** One chart/screenshot/image per decision captures the decision
  in a single glance without overwhelming the reader. The visual gallery
  IS the first impression of the homepage.
- **Scope:** Homepage layout
- **Do not:** Use walls of text or multiple competing charts in a single
  decision section.

---

## Output Formats

[Decisions about deliverable formats, structure, organization — TBD
during /ce:brainstorm]

---

## Writing & Voice

### 2026-05-27 — Write in second person, addressed to the CEO
- **Why:** The manifesto's value comes from the CEO reading it and
  thinking "this person understands my business." Second person creates
  that direct address. Consulting-speak creates distance.
- **Scope:** All written content
- **Do not:** Slip into third person ("companies often struggle with...")
  or analyst-speak ("organizations should consider implementing...").

### 2026-05-27 — Lead with the aggregate cost number: $1.4M–$3.1M/year
- **Why:** Specific enough to feel researched, large enough to demand
  attention. The credibility marker is that each component is traceable
  to a specific portfolio piece with a specific methodology.
- **Scope:** Manifesto opening, homepage headline, all distribution

### 2026-05-28 — Grep before Edit when applying review findings to .qmd files
- **Why:** Review notes and session summaries quote text as single-line prose.
  The actual .qmd files wrap at different column breaks. Edit tool requires an
  exact character-for-character match including newlines — a string from a
  review note will fail if the file wraps it differently.
- **Scope:** Any session applying /ce:review or similar findings to .qmd source files
- **Do not:** Copy strings from review notes directly into Edit calls without
  first grepping for a distinctive substring to find the exact multi-line form.

---

## Reversed / Superseded

[Nothing reversed yet — project just initialized]
