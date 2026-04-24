# Repository Guidelines

## Project Structure & Module Organization

This repository is a LaTeX/CTeX answer-sheet project. Core files are kept at the repository root:

- `mwe.tex`: current integrated answer-sheet example and active development target.
- `mainscorbox.tex` and `subscorebox.tex`: standalone score-box sources.
- `*.pdf`: generated visual outputs for inspection.
- `*.png` and `example-image.jpg`: reference/demo image assets.
- `LICENSE` and `.gitignore`: project metadata and ignored LaTeX auxiliaries.

There is no `src/` or `tests/` directory. Keep reusable LaTeX code in clearly named `.tex` files, and avoid scattering new macros through the document body when they belong in the preamble.

## Build, Test, and Development Commands

Use a TeX Live installation with CTeX, TikZ, `tabularray`, and `latexmk`.

```powershell
latexmk -pdf -interaction=nonstopmode mwe.tex
```

Builds the main example for visual inspection.

```powershell
latexmk -pdf -interaction=nonstopmode mainscorbox.tex
latexmk -pdf -interaction=nonstopmode subscorebox.tex
```

Builds standalone score-box sources.

```powershell
latexmk -C
```

Cleans generated LaTeX auxiliaries. Do not commit `.aux`, `.log`, `.fls`, `.fdb_latexmk`, or `.synctex.gz` files.

## Coding Style & Naming Conventions

Use 4-space indentation inside macro bodies and align key-value blocks for readability. For LaTeX3 code, use module-scoped internal names such as `\l__scorebox_..._tl`, `\l__scorebox_..._int`, and `\l__scorebox_..._dim`.

Keep public commands concise and semantic, for example `\scorebox` and `\choicetable`. Prefer key-value options for configurable dimensions, labels, and counts.

## Testing Guidelines

There is no automated test suite. Treat successful PDF generation plus visual inspection as the baseline test. Check table alignment, Chinese font rendering, page geometry, seal-line placement, and logical page footers.

Do not run `latexmk -pdflua` unless the user explicitly permits it in the current turn.

## Commit & Pull Request Guidelines

Recent history uses short imperative or Conventional Commit-style messages, such as `feat: initial commit` and `adjust command sequence`. Keep subjects concise and specific.

Pull requests should describe the visual/layout change, list edited source files, mention the build command used, and include updated PDFs or screenshots when output changes.

## Agent-Specific Instructions

Before editing, inspect current worktree state and avoid reverting unrelated user changes. Preserve Chinese labels, typography, and layout unless asked otherwise. Prefer static checks when the user has restricted compilation.
