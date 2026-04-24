# Repository Guidelines

## Project Structure & Module Organization

This repository contains LaTeX sources for Chinese answer-sheet and score-box layouts. Primary source files live at the repository root:

- `mainscorbox.tex`: main score-box implementation/demo source.
- `subscorebox.tex`: sub-score-box source.
- `mainscorboxdemo.tex` and `mwe.tex`: example documents for visual checks.
- `*.png` and `example-image.jpg`: reference and demo assets.
- `*.pdf`: generated output examples.

There is currently no separate `src/` or `tests/` directory. Keep new reusable LaTeX macros in dedicated `.tex` files and keep generated auxiliaries out of version control.

## Build, Test, and Development Commands

Use a LaTeX distribution with CTeX support, `tabularray`, TikZ, and `latexmk`.

```powershell
latexmk -pdf -interaction=nonstopmode mwe.tex
```

Builds the full minimal working example and is the preferred smoke test.

```powershell
latexmk -pdf -interaction=nonstopmode mainscorbox.tex
latexmk -pdf -interaction=nonstopmode mainscorboxdemo.tex
latexmk -pdf -interaction=nonstopmode subscorebox.tex
```

Builds individual documents when editing a specific component.

```powershell
latexmk -C
```

Removes common generated files. The `.gitignore` already excludes LaTeX auxiliaries such as `*.aux`, `*.log`, `*.fdb_latexmk`, `*.fls`, and `*.synctex.gz`.

## Coding Style & Naming Conventions

Use 4-space indentation inside LaTeX command bodies and align key-value option blocks for readability. Prefer descriptive macro and key names, matching existing patterns such as `\mainscorebox`, `question-num`, `scorebox-ht`, and `totalscore-str`.

This project uses LaTeX3-style internals in places (`\ExplSyntaxOn`, `\keys_define:nn`, token lists). Keep internal variables consistently prefixed and scoped, and avoid introducing global state unless required.

## Testing Guidelines

There is no automated test suite. Treat successful PDF generation as the baseline test. After changes, compile the most relevant demo plus `mwe.tex`, then inspect the PDF for table alignment, Chinese text rendering, page geometry, and score-box dimensions.

Name new examples clearly, for example `feature-demo.tex` or `layout-mwe.tex`, and keep them small enough to diagnose rendering regressions.

## Commit & Pull Request Guidelines

The current Git history uses Conventional Commit style, for example `feat: initial commit`. Continue using short imperative subjects such as `fix: adjust score box width` or `docs: add contributor guide`.

Pull requests should include a concise description, the files changed, the build command used, and screenshots or PDFs when visual output changes. Link related issues when available and mention any required fonts or LaTeX packages.

## Agent-Specific Instructions

Do not commit generated auxiliary files. Before editing, check whether a file is source (`.tex`, images, documentation) or generated output (`.aux`, `.log`, `.fls`, `.fdb_latexmk`). Preserve Chinese labels and typography unless the task explicitly asks for copy or font changes.
