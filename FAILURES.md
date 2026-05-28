# the-ten-decisions — Failure Log

What was attempted that didn't work, why it didn't work, and what was
tried next.

Lower bar than DECISIONS.md — capture failures even when they didn't
produce a durable rule. The whole point: future-you (or future-Claude)
shouldn't re-attempt dead ends because the lesson got lost.

---

## Format

### YYYY-MM-DD — [One-line failure description]

**Attempted:** [What was tried]

**Why it didn't work:** [Concrete reason, not "it broke." If the
failure mode was technical, name the specific issue. If the failure
mode was scope or approach, name that.]

**What we tried instead:** [The next attempt, which may also have
failed and may have its own entry below]

**Status:** Resolved / open / abandoned

**Tags:** [keywords for future text-search]

---

## Entries

### 2026-05-27 — `pdf-engine: chromium` is not a valid Quarto engine value

**Attempted:** Set `pdf-engine: chromium` in `_quarto.yml` format config, as specified in
the implementation plan.

**Why it didn't work:** Quarto 1.9.37 validates the `pdf-engine` field against an explicit
allowlist: `pdflatex`, `lualatex`, `xelatex`, `latexmk`, `tectonic`, `wkhtmltopdf`,
`weasyprint`, `pagedjs-cli`, `prince`, `context`, `pdfroff`, `typst`. The value `chromium`
is not in this list and causes a validation error at `quarto render` time. The design intent
was "use Chromium-based HTML→PDF rendering to support CSS and woff2 fonts" — the specific
engine name was an assumption, not a confirmed Quarto API value.

**What we tried next:** `pdf-engine: pagedjs-cli` (the correct value). pagedjs-cli installed
globally via npm. However pandoc's Haskell `findExecutable` on Windows only finds `.exe` files
— it cannot find `pagedjs-cli.cmd` even when the npm global bin is in PATH.

**Second attempt:** `weasyprint` — installed via pip, but requires GTK3 (`libgobject-2.0-0`)
which is not installed on this Windows machine. Failed with `OSError: cannot load library`.

**Resolution:** Compiled a 4KB C# wrapper `pagedjs-cli.exe` at
`C:\Users\mssha\AppData\Roaming\npm\pagedjs-cli.exe` that calls `node
node_modules/pagedjs-cli/src/cli.js`. Pandoc finds the `.exe` via PATH, the wrapper delegates
to Node.js. Smoke test passes. DECISIONS.md updated.

**Status:** Resolved (pagedjs-cli.exe C# wrapper in npm global bin)

**Tags:** quarto, pdf-engine, chromium, pagedjs-cli, windows-path, haskell-findexecutable, csc.exe

---

### 2026-05-28 — Edit tool "string not found" when replacing text from review notes

**Attempted:** Used Edit tool with strings copied from /ce:review findings to replace text in
manifesto.qmd and exec-summary.qmd. Several calls failed immediately with "String to replace
not found in file."

**Why it didn't work:** The review notes quoted strings as single-line prose, but the actual
file had the same text wrapped across two lines at a different column break. The Edit tool
requires an exact character-for-character match including all whitespace and newlines — a
string that wraps at column 72 in the file won't match if the review note had it on one line.

**What we tried instead:** Grepped for a distinctive substring of the target text (e.g., the
first 4–5 unique words) to find the exact multi-line form in the file, then used that exact
form in the Edit call. Worked every time.

**Status:** Resolved (grep-first pattern)

**Tags:** edit-tool, string-not-found, line-wrapping, grep-first, review-workflow
