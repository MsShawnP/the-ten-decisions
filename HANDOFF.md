# the-ten-decisions — Handoff Log

Session-by-session state. Updated by /log mid-session and /wrap at
session end.

For durable choices, see DECISIONS.md.
For the current work arc, see PLAN.md.
For things that didn't work, see FAILURES.md.

---

## 2026-05-27 — Project initialized

**Started from:** New project setup via /new-project.

**Did:** Created repo, set up CLAUDE.md/DECISIONS.md/HANDOFF.md/PLAN.md/
FAILURES.md/README.md, configured project structure, created GitHub
private remote, tagged v0.1-foundation.

**State:** Foundation in place. PLAN.md arc defined (Phase 1 workflow
gates). Ready to begin /clarify.

**Next:** Run /clarify to scope the work at 95% confidence. This is a
Heavy-tier project — follow the full 11-step workflow:
1. /clarify
2. /office-hours
3. /plan-ceo-review
4. /plan-eng-review
5. /ce:brainstorm
6. /ce:plan
7. /ce:work
8. /ce:review
9. /qa
10. /ce:compound
11. Ship

**Critical constraint:** Do not build until at least 8/10 portfolio
pieces are shipped. Hard must-haves: Where the Money, Retail Readiness
Scorecard, Cost of Saying Yes, and Contract-to-Cash or Deduction Recovery.

---

## 2026-05-27 17:45 — All Phase 1 workflow gates complete; requirements doc written

**What changed:** Ran /clarify, /office-hours, /plan-ceo-review, /plan-eng-review,
and /ce:brainstorm. All four Heavy-tier gates passed. Full requirements document
written to `docs/brainstorms/ten-decisions-requirements.md`.

**Why:** This is the planning foundation — all scope, structural, and voice
decisions are now locked so writing can begin without revisiting them.

**State:** All Phase 1 gates checked off in PLAN.md. DECISIONS.md has 9 locked
decisions. Requirements doc covers section template, Cinderhaven callout box
spec, aggregate cost table placement, exec summary structure, file layout, and
Lailara theme spec. No writing started. No code written.

**Key decisions locked this session:**
- Cinderhaven = composite case study, explicitly labeled (not implied real client)
- Each decision section has a named Cinderhaven callout box (dark card style)
- Aggregate cost table in Setup section before Decision 1
- Exec summary = flowing prose argument, no per-decision sections or callout boxes
- PDF engine = Chromium (CSS + woff2; LaTeX ruled out)
- A0 smoke test added before A1 (20-min PDF render check catches engine issues early)
- Success metric = one qualified C-suite read and engagement

**Next:** Run /ce:plan to produce the concrete implementation plan with task
breakdown and effort estimates. Then start A0 → A1 → A2 → B1 → C1–C5.

---

## 2026-05-27 18:45 — Complete The Ten Decisions — manifesto (3,828 words, 13 pages) and exec summary (1,049 words, 4 pages) delivered as distributable PDFs

**What changed:** All 13 implementation units (U1–U13) executed; both portfolio documents written, styled, and rendered to PDF.

**Why:** /ce:work executed the full plan — Cinderhaven findings collected, decision phrasings written, manifesto and exec summary authored, CEO-voice calibration pass completed, Lailara design system styling verified.

**State:** manifesto.qmd (3,828 words, 13 pages) and exec-summary.qmd (1,049 words, 4 pages) render cleanly via pagedjs-cli. dist/the-ten-decisions-manifesto.pdf (228 KB) and dist/the-ten-decisions-exec-summary.pdf (83 KB) are the distributable outputs. Plan status = completed. Nothing broken.

**Next:** Run /ce:review to run the reviewer ensemble on both documents before shipping.

---

## 2026-05-27 — /ce:review complete — 11 prioritized findings delivered; ready to fix

**What changed:** All 4 reviewer agents completed (correctness, coherence, project-standards, adversarial). Consolidated findings report delivered.

**Why:** Final quality gate before shipping. No structural failures — documents hold. The errors found are fixable in one editing pass.

**State:** Both .qmd files and dist/ PDFs are unchanged. 4 Tier-1 must-fix errors identified:
1. Cost-table arithmetic: rows sum to $3,150K; document states $3.1M — fix one row by -$50K
2. Decision 7 table entry ($400K–$750K) contradicts body text ($2M+) — add scope qualifier to table
3. "invoice-to-cash" used 3× in Decision 7 instead of canonical "Contract-to-Cash"
4. "13-cent gap" throughout, but source data shows 13.5¢ — round to "14 cents" or use "13.5 cents"

7 Tier-2 worth-fixing findings (fill rate rounding, D5→D6 arc transition error, 2 jargon/hedging phrases, D4 table scope gap, CTA framing, short-ship spelling consistency).

Nothing is broken. dist/ PDFs are ready to use as-is if needed urgently.

**Next:** Implement Tier 1 + Tier 2 fixes in manifesto.qmd and exec-summary.qmd. Re-render both documents. Copy distributable PDFs to dist/. Then /ce:review is checked off in PLAN.md and the project is ready to ship.

---

## 2026-05-28 — All review findings resolved; documents ship-ready

**Started from:** /ce:review complete with 11 findings pending implementation.

**Did:** Implemented all 11 Tier 1 + Tier 2 fixes (cost table arithmetic, D7/D4 scope qualifiers, Contract-to-Cash terminology, 13.5-cent precision, fill rate, D5→D6 transition rewrite, jargon/hedging, CTA framing, short-ship spelling). Fixed A3 doom loop (bandwidth argument, not cash). Verified A7 not a real double-count. Fixed A5 Cinderhaven framing ("practitioner benchmarks"). Pushed all commits.

**State:** manifesto.qmd 3,842 words / 13 pages. exec-summary.qmd 1,049 words / 4 pages. All /ce:review findings resolved. dist/ PDFs current. All pushed. Nothing broken.

**Next:** Run /ce:compound to capture learnings. Homepage build is out of scope — user handles separately.

---

## 2026-05-28 — /ce:compound complete; project fully closed

**Did:** Ran /ce:compound (Full mode). Two solution docs written and validated:
- `docs/solutions/build-errors/quarto-pagedjs-cli-windows-exe-wrapper-2026-05-28.md`
- `docs/solutions/developer-experience/edit-tool-grep-first-pattern-2026-05-28.md`
CLAUDE.md updated with docs/solutions/ discoverability entry. v1.0-ship-ready tag on dist/ PDFs.

**State:** Project complete. dist/ PDFs ship-ready. Homepage build explicitly out of scope — user handles separately. One open item: success metric (one qualified C-suite read).

**Next:** Success metric — when a qualified prospect at a specialty food brand ($3M–$50M) reads and engages with the manifesto, log it against PLAN.md's remaining checkbox.

---
