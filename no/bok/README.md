# bok-mal

LaTeX-bokmal i CUP-stil med superskriftsiteringer.

## Filer

| Fil                    | Beskrivelse                                  |
|------------------------|----------------------------------------------|
| `main.tex`             | Utgangspunktet — struktur og innhold         |
| `bokstil.sty`          | All formatering; frosset, endres sjelden     |
| `referanser.bib`       | BibTeX-referanser; legg til dine egne her    |
| `innhold/kapittel1.tex`| Eksempelkapittel; kopiér og lag flere        |
| `figurer/`             | Mappe for figurer; lastes automatisk         |

## Kom i gang

1. Kopier hele mappen til et nytt prosjekt
2. Åpne `main.tex` og fyll inn tittel, forfatter, dedikasjon
3. Skriv kapitler i `innhold/`-mappen og inkluder med `\input{innhold/...}`
4. Legg referanser inn i `referanser.bib`
5. Kompiler i denne rekkefølgen:

```
pdflatex main
bibtex   main
pdflatex main
pdflatex main
```

## Struktur

Boken er delt i tre faser:

| Fase           | Kommando        | Innhold                                       |
|----------------|-----------------|-----------------------------------------------|
| Frontmateriale | `\frontmatter`  | Tittel, dedikasjon, innhold, forord, takk     |
| Hovedmateriale | `\mainmatter`   | Innledning, deler og kapitler                 |
| Bakmateriale   | `\backmatter`   | Bibliografi, indeks                           |

## Nyttige kommandoer

### Sidemaler

```latex
\booktitlepage             % Tittelside
\dedicationpage{...}       % Dedikasjon (recto, sentrert kursiv)
\booktoc                   % Innholdsfortegnelse
\frontchapter{Forord}      % Unummerert kapittel i frontmateriale
```

### Kapittelåpning med initial

```latex
\chapter{Kapitteltittel}
\chapteropening{D}{en første setningen}
fortsetter her. Åpningsavsnittet må være langt nok
til å fylle ut høyden av initialen, ellers vil neste
seksjonsoverskrift krasje med initialen.
```

### Siteringer

```latex
\cite{nokkel}              % superskript: ¹
\cite{n1,n2,n3}            % sortert og komprimert: ¹⁻³
```

Plassering: rett etter ordet, ikke etter tegnsetting.

### Ligninger

```latex
\begin{equation}
  E = mc^2.
  \label{eq:einstein}
\end{equation}
% Referer med \eqref{eq:einstein}
```

### Figurer

```latex
\begin{figure}[t]
  \centering
  \includegraphics[width=0.8\linewidth]{filnavn}
  \caption{Figurtekst.}
  \label{fig:etikett}
\end{figure}
```

### Tabeller

Bruk `booktabs` (\toprule, \midrule, \bottomrule) — unngå
vertikale streker.

## Typografi

- **Font:** Latin Modern (T1)
- **Sideoppsett:** B5 (trykk) eller A4 (utkast), via `\documentclass`
- **Satsbredde:** 116 mm — 2,36 lilleboksalfabeter, innenfor Bringhursts
  vindu på 1,8–2,4, samme mål som lualatex-boka
- **Marger:** innside 2,6 cm, utside 3,4 cm, topp 2,6 cm, bunn 3,9 cm
- **Linjeavstand:** 1.07
- **Align-rader:** `\jot` = 8 pt (standard er 3 pt) — mer luft mellom
  radene i `align`, felles for alle malene
- **Avsnitt:** innrykk, ikke linjeskift
- **Mikrotypografi:** protrusion, expansion, tracking aktivert
- **Seksjoner:** unummererte, men i innholdsfortegnelse
- **Siteringer:** superskript-tall, plassert nøyaktig der de står
- **Bibliografi:** `1.` istedenfor `[1]`, sortert i siteringsrekkefølge

## Endre papirstørrelse

```latex
\documentclass[11pt,twoside,b5paper]{book}   % trykk
\documentclass[11pt,twoside,a4paper]{book}   % utkast
```

Det er **satsbredden** som holdes konstant mellom de to, ikke margene:
begge gir en sats på 116 mm, så et A4-utkast brekker linjer nøyaktig som
den trykte B5-en, med over 4 cm igjen til notater. Sidebrudd blir likevel
ulike — A4 er høyere.

En tredje modus gir sidekorrektur: behold `b5paper` og last stilen som
`\usepackage[korrektur]{bokstil}` — B5-siden settes uendret og sentreres
på et A4-ark med skjæremerker, så både linje- *og* sidebrudd matcher
trykk nøyaktig. Legg til `noinfo` i `crop`-opsjonene i stilfila for å
fjerne informasjonslinjen øverst på arket.

## BibTeX-kilder

- **Google Scholar** → Cite → BibTeX
- **Inspire-HEP** (inspirehep.net) — for fysikk
- **arXiv** → Export Citation → BibTeX
