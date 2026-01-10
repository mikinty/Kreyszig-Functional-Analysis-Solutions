# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

LaTeX solutions manual for Kreyszig's *Introductory Functional Analysis with Applications*. The book has 4 parts and 11 chapters covering metric spaces, Banach spaces, Hilbert spaces, and operators.

## Build Commands

```bash
# Build PDF (run twice for references)
pdflatex main.tex
pdflatex main.tex

# Or use latexmk for automatic rebuilds
latexmk -pdf main.tex

# Build to specific output directory
latexmk -pdf -output-directory=build main.tex
```

To see if compilation succeeded, please check `build/main.log`

## Project Structure

```
main.tex              # Entry point - includes all chapters via \include
preamble.tex          # All packages, custom commands, theorem environments
chapters/
  chapter1.tex        # Chapter wrapper - sets \currChapter, inputs sections
  chapter1/
    chapter1-1.tex    # Section file - actual solutions content
    chapter1-2.tex
    ...
  chapter2.tex
  chapter2/
    ...
```

**Pattern**: Chapter wrappers define `\def\currChapter{N}` then use `\input{\subDir{M}}` to include section files. The `\subDir` macro expands to `chapters/chapterN/chapterN-M`.

## Key LaTeX Conventions

### Exercise Format
```latex
\bx{
  Exercise content here...
  \begin{proof}
    Proof content...
  \end{proof}
}
```

### Common Macros (from preamble.tex)
- **Spaces**: `\R`, `\C`, `\N`, `\Z`, `\Q`, `\K` (generic field), `\F`
- **FA notation**: `\Lp{p}`, `\lp{p}`, `\Bop`, `\Kop`, `\Hilb`, `\weakto`, `\weakstarto`
- **Operators**: `\Ker`, `\Ran`, `\Dom`, `\Span`, `\codim`, `\diam`, `\supp`
- **Delimiters**: `\pa{}`, `\pbra{}`, `\pbrac{}` for auto-sized parens/brackets/braces
- **Lists**: `\ea{}` for enumerate with (a), (b), (c) labels
- **Inner products**: Use `\ip{x}{y}` from physics package
- **Integrals**: Use `\dd{t}` for differentials (e.g., `\int_a^b f(t) \dd{t}`)
- **Absolute value/norm**: Use `\abs{}` and `\norm{}` from physics package

### Theorem Environments
- `exercise` - numbered by section
- `tip` - for hints
- `definition` - provided by ntheorem[standard]
- `proof` - provided by ntheorem[standard]

### Cross-references
```latex
\begin{exercise}
\label{ex:name}
...
\end{exercise}

% Later:
By Exercise~\ref{ex:name}...
```

## TikZ Diagrams

When creating diagrams:
- Draw hatching/fills first, then curves, then labels (for proper layering)
- Use `\fill[white, inner sep=2pt]` on labels to prevent overlap with hatching
- Use `[scale=0.6]` or similar when placing multiple diagrams side-by-side
