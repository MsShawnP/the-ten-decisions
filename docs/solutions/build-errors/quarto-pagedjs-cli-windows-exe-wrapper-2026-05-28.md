---
title: "Quarto PDF rendering on Windows: pagedjs-cli .exe wrapper required"
date: 2026-05-28
category: build-errors
module: the-ten-decisions
problem_type: build_error
component: tooling
severity: high
symptoms:
  - "quarto render fails: 'chromium' is not a valid pdf-engine value in Quarto 1.9.x"
  - "pagedjs-cli installed globally via npm but pandoc cannot find it on Windows (findExecutable only matches .exe)"
  - "weasyprint fails with OSError: cannot load library libgobject-2.0-0.dll (GTK3 not installed on Windows)"
root_cause: config_error
resolution_type: tooling_addition
tags:
  - quarto
  - pdf-engine
  - pagedjs-cli
  - windows
  - pandoc
  - haskell-findexecutable
  - csc-exe
  - nodejs
---

# Quarto PDF rendering on Windows: pagedjs-cli .exe wrapper required

## Problem

Quarto 1.9.x on Windows cannot render `.qmd` files to PDF using a Chromium-based HTML→PDF engine out of the box, blocking projects that rely on CSS web fonts and hex color tokens (such as the Lailara design system) that LaTeX engines do not support. The correct engine name (`pagedjs-cli`) installs as a `.cmd` shim via npm, which pandoc's Haskell `findExecutable` cannot locate on Windows — so even after installing the right tool, the render aborts with "could not find pdf engine."

## Symptoms

- `pdf-engine: chromium` → Quarto validation error at render time: `"chromium"` is not in the valid engine allowlist
- `pdf-engine: pagedjs-cli` after `npm install -g pagedjs-cli` → render aborts with "could not find pdf engine pagedjs-cli" even though `pagedjs-cli.cmd` is in PATH
- `pdf-engine: weasyprint` → `OSError: cannot load library 'libgobject-2.0-0.dll': error 0x7e`

## What Didn't Work

**1. `pdf-engine: chromium`**

Quarto 1.9.37 validates the `pdf-engine` field against an explicit allowlist: `pdflatex`, `lualatex`, `xelatex`, `latexmk`, `tectonic`, `wkhtmltopdf`, `weasyprint`, `pagedjs-cli`, `prince`, `context`, `pdfroff`, `typst`. The string `"chromium"` is not in the list. Quarto rejects the config before any rendering begins. This value was assumed from the design intent ("use Chromium-based rendering") without checking the Quarto API.

**2. `pdf-engine: weasyprint`**

WeasyPrint is installable via pip on Windows, but its rendering backend requires the GTK3 runtime (`libgobject-2.0-0`). That library is not distributed with Windows. The render fails at WeasyPrint startup with an OSError before any HTML is processed.

**3. `pdf-engine: pagedjs-cli` (npm install only, no .exe wrapper)**

`npm install -g pagedjs-cli` places `pagedjs-cli.cmd` in the npm global bin directory (e.g. `C:\Users\<user>\AppData\Roaming\npm\`). That directory is in `PATH`. However, pandoc uses Haskell's `findExecutable` function on Windows, which searches `PATH` for files with `.exe` or `.com` extensions — it does not invoke the Windows shell to resolve `.cmd` batch files. Pandoc cannot find the engine even though the npm shim is present and PATH is correct.

## Solution

Compile a minimal C# `.exe` wrapper that calls Node directly with the pagedjs-cli entry point and passes all arguments through. Place it at `C:\Users\<user>\AppData\Roaming\npm\pagedjs-cli.exe` so pandoc finds it via PATH lookup.

**Wrapper source** (save as `wrapper.cs`):

```csharp
using System;
using System.Diagnostics;

class PagesJS {
    static int Main(string[] args) {
        var p = new Process();
        p.StartInfo.FileName = "node";
        p.StartInfo.Arguments = "\"" +
            System.IO.Path.Combine(
                System.Environment.GetEnvironmentVariable("APPDATA"),
                "npm", "node_modules", "pagedjs-cli", "src", "cli.js"
            ) + "\" " + string.Join(" ", args);
        p.StartInfo.UseShellExecute = false;
        p.Start();
        p.WaitForExit();
        return p.ExitCode;
    }
}
```

**Compile with the Windows built-in C# compiler** (no Visual Studio required):

```powershell
# Find csc.exe — present on all modern Windows installs
$csc = (Get-ChildItem "C:\Windows\Microsoft.NET\Framework64" -Recurse -Filter "csc.exe" |
        Sort-Object LastWriteTime -Descending |
        Select-Object -First 1).FullName

# Save the wrapper source
Set-Content -Path "$env:TEMP\wrapper.cs" -Value (Get-Content wrapper.cs -Raw)

# Compile to the npm global bin directory
& $csc /out:"$env:APPDATA\npm\pagedjs-cli.exe" "$env:TEMP\wrapper.cs"
```

The resulting binary is approximately 4 KB.

**Working `_quarto.yml` configuration:**

```yaml
format:
  pdf:
    pdf-engine: pagedjs-cli
    css: lailara.scss
    toc: false
    number-sections: false
```

**Required CSS for correct rendering:**

```css
/* Preserve background colors in printed PDF */
* {
  print-color-adjust: exact;
  -webkit-print-color-adjust: exact;
}

@page {
  size: letter;
  margin: 0.6in;
}

/* Self-hosted fonts — DO NOT use Google Fonts CDN (unavailable at render time) */
@font-face {
  font-family: 'Playfair Display';
  src: url('fonts/PlayfairDisplay-Regular.woff2') format('woff2');
  font-weight: 400;
}
```

## Why This Works

The root cause is a Windows-specific limitation in pandoc's executable discovery. Pandoc uses Haskell's `findExecutable` function, which searches `PATH` for files with recognized executable extensions. On Windows, this requires a true `.exe` binary — the function does not invoke the Windows shell to resolve `.cmd` batch wrappers (even though Windows's own shell would resolve them). npm's global CLI shim is a `.cmd` file, so pandoc never finds it regardless of PATH configuration.

The C# wrapper produces a real `.exe` at the path pandoc expects (`pagedjs-cli.exe` in the npm global bin). The wrapper delegates to `node` (which is itself a real `.exe`) with the full absolute path to the pagedjs-cli JavaScript entry point, preserving all argument passing and exit-code propagation. The binary is ~4 KB and has no external dependencies beyond Node.js.

## Prevention

**Setup order on a new Windows machine:**

1. Install Node.js (≥ v18) and Quarto (≥ 1.9). Verify both are in PATH.
2. Run `npm install -g pagedjs-cli`.
3. Confirm `$env:APPDATA\npm\node_modules\pagedjs-cli\src\cli.js` exists.
4. Compile the C# wrapper (commands above). Confirm `$env:APPDATA\npm\pagedjs-cli.exe` exists.
5. Run `pagedjs-cli --version` — exercises the full stack: pandoc lookup → .exe → Node → cli.js.
6. In `_quarto.yml`, set `pdf-engine: pagedjs-cli`.
7. In CSS, add `print-color-adjust: exact` and `@font-face` rules pointing to local `.woff2` files. No CDN font URLs resolve during headless render.

**If npm is reinstalled or the machine is replaced**, the `pagedjs-cli.exe` wrapper is deleted (it is not managed by npm). Recompile from the source above. Keep the `.cs` source file in the project root or the npm global bin directory for easy access.

**Before each render**, confirm the output PDF is not open in any application. Adobe Acrobat and similar readers hold an exclusive write lock on open PDFs. Quarto's write to `dist/` fails with `PermissionDenied` if the file is locked.

**Debugging checklist if render still fails after setup:**
- `where.exe pagedjs-cli` — should return both `pagedjs-cli.cmd` and `pagedjs-cli.exe`. If only `.cmd` appears, the wrapper was not compiled or placed in the wrong directory.
- `pagedjs-cli --version` — if Node throws a module-not-found error, the path in the wrapper does not match the actual install location. Check `$env:APPDATA\npm\node_modules\pagedjs-cli\src\cli.js` exists.
- Missing fonts in PDF: confirm `@font-face` rules point to local `.woff2` files relative to the CSS file, not CDN URLs.
- White background where a colored background is expected: add `print-color-adjust: exact` to the `html` and `body` selectors in CSS.

## Related Issues

- `product-data-health-audit/FAILURES.md` — Adjacent failure: `rsvg-convert` not found on Windows when Quarto's LaTeX pipeline tries to convert SVG. Same pattern (Quarto on Windows needing a system binary that is absent), different engine (LaTeX vs pagedjs-cli), different fix (install rsvg-convert vs compile .exe wrapper).
- `edi-preflight/DECISIONS.md` — WeasyPrint rejected as a PDF engine because it requires Cairo/Pango system libraries. Same constraint (GTK runtime absent) in a Docker context rather than bare Windows.
