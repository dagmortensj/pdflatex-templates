# notes-template

LaTeX template for long-form theoretical physics and mathematics notes.
CUP-inspired book typography in article form, with theorem and exercise
environments, a JHEP-style framed table of contents, and numbered citations.

## Files

| File              | Description                                |
|-------------------|--------------------------------------------|
| `main.tex`        | Starting point — content lives here        |
| `notesstyle.sty`  | All formatting; rarely changed             |
| `references.bib`  | BibTeX references; add your own here       |
| `figures/`        | Folder for figures; loaded automatically   |

## Getting started

1. Copy the entire folder to a new project
2. Open `main.tex` and fill in title, author, abstract
3. Add references to `references.bib`
4. Compile in this order:

```
pdflatex main
bibtex   main
pdflatex main
pdflatex main
```

## Useful commands

### Citations

```latex
\cite{key}                 % [1]
\cite{k1,k2,k3}            % [1-3] (sorted and compressed)
```

### Table of contents

```latex
\framedtoc
```

Renders the contents framed by a rule above and below (JHEP-style),
with no dot leaders. In the template it sits on its own page,
between the front page and the body. Plain `\tableofcontents` still
works if you ever want an unframed list.

### Theorem environments

```latex
\begin{theorem}
  Statement of the theorem.
\end{theorem}

\begin{definition}
  Definition text.
\end{definition}

\begin{remark}
  A remark.
\end{remark}
```

All three share a single counter scoped to the section,
e.g. Theorem 2.1, Definition 2.2, Remark 2.3.

### Boxes: important and mainresult

```latex
\begin{important}
\begin{definition}
  ...
\end{definition}
\end{important}

\begin{mainresult}[Law of gravitation]   % title can be omitted
\begin{theorem}
  ...
\end{theorem}
\end{mainresult}
```

`important` sets thin dark red rules above and below the content —
for important definitions. `mainresult` sets a hairline frame
around the document's central result; with the optional argument
the title sits in letterspaced small caps breaking the top frame
rule, without it the frame stands clean. Both are wrappers around
the ordinary environments: numbering continues in the same
sequence as elsewhere, and the boxes break across pages. Use them
sparingly — box everything and the box is no longer a signal.

### Exercises

```latex
\begin{exercise}
Prompt for the exercise.

\begin{subproblems}
  \item First subproblem.
  \item Second subproblem.
\end{subproblems}
\end{exercise}
```

Exercises are numbered per section (e.g. Exercise 4.1, 4.2),
independently of the theorem counter, and use bold letter
labels for subproblems (a, b, c), with the same indent as
ordinary lists. The `subproblems` environment leaves ordinary
`enumerate` lists untouched.

Exercises are set at full width, without indentation,
separated from the prose by space: 4.5ex before and 6.75ex
after. Less room before ties the exercise to its lead-in;
more room after marks it as finished. Two consecutive
exercises share the larger distance — space never stacks.

Use `\begin{subproblems}[resume]` to continue the same letter
sequence after explanatory prose between subproblems.

### Python code

```latex
\begin{python}
import numpy as np

def f(x):
    return np.sin(x)   # example function

print(f(np.pi / 2))
\end{python}
```

Typesets Python with Gruvbox Light syntax highlighting: coloured
keywords, strings, comments, and line numbers on a warm cream background,
framed top and bottom. UTF-8 input is enabled, so Norwegian characters
(æ, ø, å) work in surrounding text and in code comments.

### Separator

```latex
\separator
```

A thin dark red rule with vertical space on either side.
Use between content blocks — after an exercise, between
examples, or at a topic shift within a section. It can be
called anywhere in the normal document flow.

### Equations

```latex
\begin{equation}
  E = mc^2.
  \label{eq:einstein}
\end{equation}
% Reference with \eqref{eq:einstein}
```

### Figures

```latex
\begin{figure}[t]
  \centering
  \includegraphics[width=0.8\linewidth]{filename}
  \caption{Figure caption.}
  \label{fig:label}
\end{figure}
```

### TikZ figures

`notesstyle.sty` does not load TikZ — add `\usepackage{tikz}` to the
custom packages block in `main.tex` when you need native figures.

The style file defines five named colors. Their roles are fixed:

| Color        | RGB          | Role                                                      |
|--------------|--------------|-----------------------------------------------------------|
| `darkorange` | 184, 92, 0   | Primary figure accent: strokes, nodes, bars               |
| `darkolive`  | 74, 107, 18  | Secondary figure accent: curves, fills                    |
| `darkblue`   | 30, 96, 140  | Third figure accent                                       |
| `darkplum`   | 110, 50, 120 | Fourth figure accent                                      |
| `darkred`    | 120, 20, 20  | Reserved — hyperlinks and separator rule; not for figures |

Black and gray are the structural colors in figures: axes, grids, guide
lines, walls, and coordinate labels. The palette colors carry content —
curves, series, and marked regions.

Typical usage:

```latex
\draw[very thick, darkorange] (0,0) -- (2,0);
\node[circle, fill=darkorange, inner sep=1.4pt] at (1,0) {};
\fill[darkorange!12] (0,0) rectangle (2,1);
\draw[darkolive, thick, domain=0:3, samples=60]
    plot (\x, {sin(deg(\x))});
\draw[->, darkolive!75] (0,0) -- (1,1);
\draw[darkblue, thick, dashed] (0,1) -- (3,1);
\draw[darkplum, thick, dotted] (0,0.5) -- (3,0.5);
```

### Tables

Use `booktabs` (\toprule, \midrule, \bottomrule) — avoid
vertical lines.

## Typography

- **Font:** MLModern (T1)
- **Page size:** A4, symmetric margins (3.0 cm L/R)
- **Line spacing:** 1.07
- **Align rows:** `\jot` = 8 pt (default 3 pt) — more air between the
  rows of `align`, shared by all the templates
- **Paragraphs:** indented, no line break
- **Microtypography:** protrusion, expansion, tracking enabled
- **Sections:** numbered, bold headings
- **Subsubsections:** quiet run-in heading, kept out of the table of contents
- **Citations:** numerical in square brackets, sorted and compressed
- **Bibliography:** `unsrtnat` (in citation order)
- **Hyperlinks:** dark red, print-safe
- **Table of contents:** JHEP-style, framed by horizontal rules

## Adding theorem-like environments

```latex
\theoremstyle{plain}
\newtheorem{lemma}[theorem]{Lemma}
\newtheorem{proposition}[theorem]{Proposition}

\theoremstyle{definition}
\newtheorem{example}[theorem]{Example}
```

The `[theorem]` argument means the new environment shares
the theorem counter — keeps numbering coherent across the
document.

## BibTeX sources

- **Google Scholar** → Cite → BibTeX
- **Inspire-HEP** (inspirehep.net) — for physics
- **arXiv** → Export Citation → BibTeX
