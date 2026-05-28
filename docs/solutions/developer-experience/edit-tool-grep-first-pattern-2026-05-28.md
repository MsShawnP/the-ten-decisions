---
title: "Grep before Edit when applying review findings to prose files"
date: 2026-05-28
category: developer-experience
module: the-ten-decisions
problem_type: developer_experience
component: development_workflow
severity: low
applies_when:
  - Applying text edits driven by review notes, session summaries, or any source other than a direct file read in the current context
  - Editing .qmd, .md, or other prose-heavy files where lines wrap at different column widths across editors
tags:
  - edit-tool
  - string-not-found
  - line-wrapping
  - grep-first
  - qmd
  - review-workflow
  - ce-review
---

# Grep before Edit when applying review findings to prose files

## Context

When applying text edits sourced from review notes, session summaries, or external documents to `.qmd` or similar prose files, the Edit tool's `old_string` must match the file exactly — character for character, including line breaks and whitespace. Review notes typically quote target text as a single run of prose on one line. If the source file wraps that same text across two lines at a different column break, the Edit call fails immediately with "String to replace not found in file."

This failure occurred five times in a single session applying 11 targeted edits to `manifesto.qmd` and `exec-summary.qmd` after a `/ce:review` pass. Every failure had the same cause: `old_string` was copied from a review finding rather than read from the file.

## Guidance

Before any Edit call where `old_string` comes from a review note, session summary, or any source other than a direct file read in the current session:

1. **Grep for a distinctive substring** — pick 4–6 unique consecutive words from the target text and run a content search. This returns the exact form in the file, including where lines break.
2. **Use the exact multi-line form** returned by Grep as the `old_string` in the Edit call.

Never use a string from a review note or session summary as `old_string` without this verification step first.

## Why This Matters

Quarto `.qmd` files (and most prose files edited by humans or `quarto fmt`) wrap text at 72–80 columns. Review notes and session summaries reconstruct those passages as single-line prose. The Edit tool requires a byte-exact match — no fuzzy matching, no whitespace normalization. A string from a review note will never match the wrapped form in the file unless by coincidence.

Without the grep step, every Edit call for a wrapped string fails with "String to replace not found," requiring diagnosis and a retry. In a session with many edits driven by review findings, this silently doubles the number of tool calls needed.

## When to Apply

- Any session driven by `/ce:review` findings, `/qa` findings, session summaries, or external review documents
- Any edit to a `.qmd`, `.md`, or other prose file where `old_string` was not just read directly from the file in the current session
- Particularly critical for files longer than ~100 lines where column wrapping may differ from the source of the edit

## Examples

**Before (fails):**

```
# old_string copied verbatim from a review note:
old_string: "it's a 13-cent structural gap on every dollar you invoice"
```
→ Edit tool: "String to replace not found in file"

**After (works):**

First grep for a distinctive substring:
```
Grep pattern: "13.cent"
```

Returns:
```
manifesto.qmd:316: statement themselves. At $25M, it's a 13-cent structural gap on every dollar you
manifesto.qmd:317: invoice
```

Then use the exact multi-line form as `old_string`:
```
old_string: "it's a 13-cent structural gap on every dollar you\ninvoice"
```
→ Edit succeeds.

**The same pattern applied to the doom-loop sentence in manifesto.qmd:**

Review note quoted: `"The cash gap delays the product data cleanup that would have stopped the next round of onboarding errors."`

Grep for `"cash gap"` revealed the sentence wrapped differently. The corrected multi-line form matched and the edit landed correctly.

## Related

- `the-ten-decisions/DECISIONS.md` — 2026-05-28 entry: "Grep before Edit when applying review findings to .qmd files" — durable rule
- `the-ten-decisions/FAILURES.md` — 2026-05-28 entry: "Edit tool 'string not found' when replacing text from review notes"
