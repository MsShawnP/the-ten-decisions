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
