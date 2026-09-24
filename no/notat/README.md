# notat-mal

LaTeX-mal for langformede notater i teoretisk fysikk og matematikk.
CUP-inspirert boktypografi i artikkelformat, med teorem- og
oppgaveomgivelser, en JHEP-aktig innrammet innholdsfortegnelse, og
nummererte siteringer.

## Filer

| Fil               | Beskrivelse                                |
|-------------------|--------------------------------------------|
| `main.tex`        | Utgangspunktet — innholdet skrives her     |
| `notatstil.sty`   | All formatering; endres sjelden            |
| `referanser.bib`  | BibTeX-referanser; legg til dine egne her  |
| `figurer/`        | Mappe for figurer; lastes automatisk       |

## Kom i gang

1. Kopier hele mappen til et nytt prosjekt
2. Åpne `main.tex` og fyll inn tittel, forfatter, sammendrag
3. Legg referanser inn i `referanser.bib`
4. Kompiler i denne rekkefølgen:

```
pdflatex main
bibtex   main
pdflatex main
pdflatex main
```

## Nyttige kommandoer

### Siteringer

```latex
\cite{nokkel}              % [1]
\cite{n1,n2,n3}            % [1-3] (sortert og komprimert)
```

### Innholdsfortegnelse

```latex
\framedtoc
```

Setter innholdsfortegnelsen med en linje over og under
(JHEP-stil), uten punktledere. I malen ligger den på egen side,
mellom forsiden og brødteksten. Vanlig `\tableofcontents`
fungerer fortsatt om du heller vil ha en uinnrammet liste.

### Teoremomgivelser

```latex
\begin{teorem}
  Formuleringen av teoremet.
\end{teorem}

\begin{definisjon}
  Definisjonstekst.
\end{definisjon}

\begin{merknad}
  En merknad.
\end{merknad}
```

Alle tre deler én teller knyttet til seksjonen,
f.eks. Teorem 2.1, Definisjon 2.2, Merknad 2.3.

### Bokser: viktig og hovedresultat

```latex
\begin{viktig}
\begin{definisjon}
  ...
\end{definisjon}
\end{viktig}

\begin{hovedresultat}[Gravitasjonsloven]   % tittelen kan sløyfes
\begin{teorem}
  ...
\end{teorem}
\end{hovedresultat}
```

`viktig` setter tynne mørkerøde linjer over og under innholdet —
til viktige definisjoner. `hovedresultat` setter en hårfin ramme
rundt dokumentets sentrale resultat; med valgfritt argument står
tittelen i sperrede kapiteler brutt inn i den øvre rammelinjen,
uten står rammen ren. Begge er omslag rundt de vanlige
omgivelsene: nummereringen fortsetter i samme rekke som ellers,
og boksene er brytbare over sideskift. Bruk dem sparsomt —
bokses alt, er boksen ikke lenger et signal.

### Oppgaver

```latex
\begin{oppgave}
Oppgavetekst.

\begin{deloppgaver}
  \item Første deloppgave.
  \item Andre deloppgave.
\end{deloppgaver}
\end{oppgave}
```

Oppgaver nummereres per seksjon (f.eks. Oppgave 4.1, 4.2),
uavhengig av teoremtelleren, og bruker magre bokstavetiketter
for deloppgaver (a, b, c), med samme innrykk som vanlige
lister. `deloppgaver`-omgivelsen lar vanlige `enumerate`-lister
være urørt.

Oppgavene settes i full bredde, uten innrykk, skilt fra
prosaen av luft: 4,5 ex før og 6,75 ex etter. Mindre rom før
binder oppgaven til innledningen sin; større rom etter
markerer at den er ferdig. To oppgaver på rad deler den
største avstanden — luften stables aldri.

Bruk `\begin{deloppgaver}[resume]` for å fortsette samme
bokstavsekvens etter forklarende tekst mellom deloppgaver.

### Python-kode

```latex
\begin{python}
import numpy as np

def f(x):
    return np.sin(x)   # eksempelfunksjon

print(f(np.pi / 2))
\end{python}
```

Setter Python-kode med Gruvbox Light syntaksutheving: fargede
nøkkelord, strenger, kommentarer og linjenummer på en varm kremfarget
bakgrunn, rammet opp og ned. UTF-8 er aktivert, så norske tegn
(æ, ø, å) fungerer i den omgivende teksten og i kodekommentarer.

### Separator

```latex
\separator
```

En tynn mørkerød linje med vertikalt mellomrom på begge sider.
Bruk mellom innholdsblokker — etter en oppgave, mellom
eksempler, eller ved temaskifter innen en seksjon. Den kan
kalles hvor som helst i den vanlige tekstflyten.

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

### TikZ-figurer

`notatstil.sty` laster ikke TikZ — legg til `\usepackage{tikz}` i
pakkeblokken i `main.tex` når du trenger native figurer.

Stilfilen definerer fem navngitte farger med faste roller:

| Farge        | RGB          | Rolle                                                          |
|--------------|--------------|----------------------------------------------------------------|
| `darkorange` | 184, 92, 0   | Primær figuraksent: streker, noder, søyler                     |
| `darkolive`  | 74, 107, 18  | Sekundær figuraksent: kurver, fyll                             |
| `darkblue`   | 30, 96, 140  | Tredje figuraksent                                             |
| `darkplum`   | 110, 50, 120 | Fjerde figuraksent                                             |
| `darkred`    | 120, 20, 20  | Reservert — hyperlenker og separatorlinje; ikke til figurer    |

Svart og grå er strukturfargene i figurer: akser, rutenett, hjelpelinjer,
vegger og koordinatetiketter. Palettfargene bærer innhold — kurver, serier
og markerte områder.

Typisk bruk:

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

### Tabeller

Bruk `booktabs` (\toprule, \midrule, \bottomrule) — unngå
vertikale streker.

## Typografi

- **Font:** MLModern (T1)
- **Sideoppsett:** A4, symmetriske marger (3.0 cm V/H)
- **Linjeavstand:** 1.07
- **Align-rader:** `\jot` = 8 pt (standard er 3 pt) — mer luft mellom
  radene i `align`, felles for alle malene
- **Avsnitt:** innrykk, ikke linjeskift
- **Mikrotypografi:** protrusion, expansion, tracking aktivert
- **Seksjoner:** nummererte, fete overskrifter
- **Underunderseksjoner:** stille run-in-overskrift, holdt utenfor innholdsfortegnelsen
- **Siteringer:** numeriske i hakeparenteser, sortert og komprimert
- **Bibliografi:** `unsrtnat` (i siteringsrekkefølge)
- **Hyperlenker:** mørkerød, trygt for trykk
- **Innholdsfortegnelse:** JHEP-stil, rammet av vannrette linjer

## Legge til flere teoremomgivelser

```latex
\theoremstyle{plain}
\newtheorem{lemma}[teorem]{Lemma}
\newtheorem{proposisjon}[teorem]{Proposisjon}

\theoremstyle{definition}
\newtheorem{eksempel}[teorem]{Eksempel}
```

`[teorem]`-argumentet betyr at den nye omgivelsen deler
samme teller som teorem — holder nummereringen sammenhengende
gjennom hele dokumentet.

## BibTeX-kilder

- **Google Scholar** → Cite → BibTeX
- **Inspire-HEP** (inspirehep.net) — for fysikk
- **arXiv** → Export Citation → BibTeX
