# book-template

LaTeX book template in CUP style with superscript citations.

## Files

| File                   | Description                                    |
|------------------------|------------------------------------------------|
| `main.tex`             | Starting point — structure and content         |
| `bookstyle.sty`        | All formatting; frozen, rarely changed         |
| `references.bib`       | BibTeX references; add your own here           |
| `content/chapter1.tex` | Example chapter; copy and create more          |
| `figures/`             | Folder for figures; loaded automatically       |

## Getting started

1. Copy the entire folder to a new project
2. Open `main.tex` and fill in title, author, dedication
3. Write chapters in the `content/` folder and include with `\input{content/...}`
4. Add references to `references.bib`
5. Compile in this order:

```
pdflatex main
bibtex   main
pdflatex main
pdflatex main
```

## Structure

The book is divided into three phases:

| Phase         | Command         | Contents                                         |
|---------------|-----------------|--------------------------------------------------|
| Front matter  | `\frontmatter`  | Title, dedication, TOC, preface, acknowledgments |
| Main matter   | `\mainmatter`   | Introduction, parts and chapters                 |
| Back matter   | `\backmatter`   | Bibliography, index                              |

## Useful commands

### Page templates

```latex
\booktitlepage             % Title page
\dedicationpage{...}       % Dedication (recto, centered italic)
\booktoc                   % Table of contents
\frontchapter{Preface}     % Unnumbered chapter in front matter
```

### Chapter opening with drop cap

```latex
\chapter{Chapter Title}
\chapteropening{T}{he first sentence}
continues here. The opening paragraph must be long enough
to fill the vertical space reserved by the drop cap, otherwise
the next section heading will collide with the drop cap.
```

### Citations

```latex
\cite{key}                 % superscript: ¹
\cite{k1,k2,k3}            % sorted and compressed: ¹⁻³
```

Placement: directly after the word, not after punctuation.

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

### Tables

Use `booktabs` (\toprule, \midrule, \bottomrule) — avoid
vertical lines.

## Typography

- **Font:** Latin Modern (T1)
- **Page size:** B5 (print) or A4 (draft), via `\documentclass`
- **Measure:** 116 mm — 2.36 lowercase alphabets, inside Bringhurst's
  1.8–2.4 window, the same measure as the lualatex book
- **Margins:** inner 2.6 cm, outer 3.4 cm, top 2.6 cm, bottom 3.9 cm
- **Line spacing:** 1.07
- **Align rows:** `\jot` = 8 pt (default 3 pt) — more air between the
  rows of `align`, shared by all the templates
- **Paragraphs:** indented, no line break
- **Microtypography:** protrusion, expansion, tracking enabled
- **Sections:** unnumbered, but appear in TOC
- **Citations:** superscript numbers, placed exactly where written
- **Bibliography:** `1.` instead of `[1]`, sorted by citation order

## Changing paper size

```latex
\documentclass[11pt,twoside,b5paper]{book}   % print
\documentclass[11pt,twoside,a4paper]{book}   % draft
```

The **measure** is held constant across the two, not the margins:
both give a 116 mm text block, so an A4 draft breaks lines exactly as
the printed B5 will, with over 4 cm left over for notes. Page breaks
still differ — A4 is taller.

A third mode gives page proofs: keep `b5paper` and load the style as
`\usepackage[proof]{bookstyle}` — the B5 page is typeset untouched and
centred on an A4 sheet with crop marks, so line *and* page breaks match
print exactly. Add `noinfo` to the `crop` options in the style file to
drop the info line at the top of each sheet.

## BibTeX sources

- **Google Scholar** → Cite → BibTeX
- **Inspire-HEP** (inspirehep.net) — for physics
- **arXiv** → Export Citation → BibTeX
