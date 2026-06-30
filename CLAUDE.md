# the-ten-decisions — Project Context for Claude

## What this project is

Flagship manifesto-driven homepage and downloadable PDF manifesto positioning a
specialty food consulting practice around ten critical decisions growing brands
make blind. The piece ties together all other portfolio pieces into a coherent
practice thesis: "Ten Decisions You're Making Blind — and What the Frameworks
Look Like." Built last — requires at least 8 of 10 portfolio pieces to be
shipped before the build begins.

**Business question this project answers:** Does a prospect land on the portfolio
and immediately understand the full scope, thesis, and value of the practice —
and know exactly where to start?

**Tier:** Heavy

## Stack and tools

- Primary language: TBD — to be determined during /clarify → /ce:brainstorm → /plan-eng-review
- Key packages/libraries: TBD
- Entry point: TBD
- Hosting: Netlify or GitHub Pages (TBD)
- Note: Stack must be confirmed before any code is written. See DECISIONS.md.

## Project files

- CLAUDE.md (this file) — permanent rules and facts
- DECISIONS.md — durable choices and reasoning
- HANDOFF.md — current session state
- PLAN.md — current work arc
- FAILURES.md — things tried that didn't work
- `docs/solutions/` — structured learnings from /ce:compound, searchable by module, problem_type, and tags (use /ce:learnings-researcher to query)

Read PLAN.md and HANDOFF.md at session start. DECISIONS.md and
FAILURES.md as relevant.

## Voice and standards

- Economist style: sober, declarative, data-forward, opinionated
- Second person throughout — write to the CEO directly
- No marketing voice ("leverage," "synergy," "best-in-class," "unlock," "drive value")
- No hedging that softens a real finding
- Tone: confident, specific, empathetic — NOT arrogant or lecturing
- The CEO reading it should think "this person understands my business"
- Avoid: "You need to implement a modern data stack with automated pipeline orchestration."
- Embrace: "If you can't tell which SKUs paid for your payroll last month without opening four separate spreadsheets, you are operating blind."

## Rules

### Honesty and judgment

- Say "I don't know" or "I can't verify this" instead of guessing.
  This applies to industry context, technical claims, what code did,
  and anything else.
- Tell me what I need to hear, not what I want to hear. If a decision
  looks wrong, say so. If code I wrote has problems, say so. Honest
  assessment, not validation.
- If a rule in this file is too vague to verify whether you're
  following it, flag it for revision rather than guessing at compliance.

### Building and proposing

- No speculative abstractions. If something isn't needed right now,
  don't build it. Helper functions get added when called by real code,
  not in anticipation. Parameters get added when there's a second use
  case, not the first.
- When proposing a tool, library, or approach, present at least two
  alternatives with tradeoffs, even if one is clearly preferred. Do
  not propose a single solution and move on.
- Tie proposals back to the business question this project is
  answering. If you can't connect a proposal to that question, the
  proposal is probably fluff and should be reconsidered.

### How to work the project

- Work in vertical slices, not horizontal phases. Build one feature
  end-to-end (working from input to output) before moving to the
  next. Don't build all the backend, then all the frontend — build
  one complete piece at a time.
- When a feature is working, suggest a simple test to verify it stays
  working.
- Do not start tasks outside the current PLAN.md arc without flagging
  it to the user first.
- Do not refactor unrelated code unprompted.
- Do not rename things unless asked.

### Build sequencing — IMPORTANT

This piece is the capstone. Do not build before at least 8 of 10
portfolio pieces are shipped. Hard must-haves before build:
- Where the Money Actually Comes From
- Retail Readiness Scorecard
- Cost of Saying Yes
- Contract-to-Cash OR Retailer Deduction Recovery

### Git branching

- Before risky or experimental changes, suggest creating a branch.
- Keep it simple: `git checkout -b experiment/short-description`
  before the change, merge back to main if it works.
- Don't require branches for small, safe changes.

### Scope creep detection

- Periodically check whether the current work matches PLAN.md.
- Flag drift: "We've been working on [thing] but it's not in the
  current plan. Want to add it to PLAN.md, or should we finish the
  planned work first?"

## Working with PLAN.md

PLAN.md defines the current arc of work. Read it at session start.

- Mark tasks complete as they're finished, in the same commit as the work
- If a task is wrong-sized, in the wrong order, or no longer relevant,
  flag it rather than silently restructuring
- "Out of scope" items are decisions, not suggestions — do not pull
  them into the current arc without explicit user approval

## Session reminders

### Session start protocol

1. Read CLAUDE.md, PLAN.md, and HANDOFF.md
2. If HANDOFF.md's most recent entry is more than 24 hours old AND
   there are uncommitted changes, flag this
3. Briefly state the starting point from HANDOFF.md so the user
   confirms you're caught up
4. Confirm the current PLAN.md arc is still active
5. Remind the user what commands are available

### Suggesting commands during work

- User just finished a task → "Good time to /log that."
- User seems unsure what to do next → "Want to run /next to see
  what's queued?"
- User is about to stop → "Run /wrap before you go so your next
  session picks up here."
- User is starting a new arc → "Run /clarify to scope the work,
  then /ce:brainstorm."
- For Heavy tier, after /clarify → "/office-hours, then
  /plan-ceo-review, then /plan-eng-review before any code."

Keep suggestions to one line. Don't explain the command every time.
If the user ignores the suggestion, don't repeat it in the same session.

## Defaults

- Default to flagging gaps rather than filling with plausible-sounding
  but unverified content
- Default to short responses unless the task is substantive
- Default to asking before promoting a log entry to a DECISIONS.md entry
- Default to answering, not offering to answer

Never write secrets, tokens, or passwords into tracked files, READMEs, or commit messages — use environment variables and secret stores only.
