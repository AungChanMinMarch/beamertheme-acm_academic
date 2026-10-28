# acm_academic — Beamer theme

Three layouts from one line, `\usetheme{acm_academic}`:

| Layout | When it appears |
|---|---|
| Title page | `\maketitle` |
| Section page (purple) | automatically at every `\section` |
| Content page (sidebar + footer) | every normal `\begin{frame} … \end{frame}` |

## Files

| File | What it is |
|---|---|
| `beamerthemeacm_academic.sty` | the theme |
| `logos/` | logo library, usable from any project by file name, e.g. `\logoA{acmlogo-siit}`. Add your own here (`.pdf`, `.png`, `.jpg`); give them a unique prefix such as `acmlogo-` so the names don't clash with other files in your TeX tree |

## Install once, use everywhere

This folder is the single source of truth. It is linked into your personal TeX
tree, so every `.tex` file on this computer finds the theme and the logos:

```bash
mkdir -p ~/texmf/tex/latex
ln -sfn ~/projects/beamertheme-acm_academic ~/texmf/tex/latex/acm_academic
kpsewhich beamerthemeacm_academic.sty     # check: prints the installed path
```

Edits here take effect in every project on the next compile. A copy of the
`.sty` next to a `.tex` file wins over the installed one, so delete local
copies. On **Overleaf**, upload the `.sty` and the logos you use into the
project instead.

## Minimal preamble

```latex
\documentclass[aspectratio=169]{beamer}
\usetheme{acm_academic}

\purpose{Thesis Proposal · Master of Engineering}   % optional, red line
\title[Short title for footer]{Full title}
\subtitle{One sentence about the talk}              % optional
\author{Aung Chan Min}
\institute{Sirindhorn International Institute of Technology\\Thammasat University}
\advisor{Name}                                      % optional
\coadvisor{Name}                                    % optional
\date{26 October 2026}                              % default: today

\logoA{acmlogo-siit}                                % optional logos (library name,
\logoB{acmlogo-thammasat}                           % or a file next to the .tex)
\logoBcaption{Thammasat\\University}                % optional, beside logo B

\begin{document}
\maketitle

\section[Motivation]{Motivation and problem}        % [short] = navigation name
\sectiondescription{Why engagement recognition matters.}   % optional, AFTER \section

\begin{frame}{Frame title}
  ...
\end{frame}
\end{document}
```

Compile **twice** (pdfLaTeX, XeLaTeX or LuaLaTeX): the section list,
"Section x of n", the page total and section descriptions are read from
the previous run, like any Beamer table of contents.

## All theme commands

| Command | Effect |
|---|---|
| `\purpose{…}` | red letter-spaced line above the title |
| `\advisor[Label]{Name}` | bottom-right line `Label: Name` (label defaults to *Advisor*) |
| `\coadvisor[Label]{Name}` | second line (label defaults to *Co-advisor*) |
| `\addtitleinfo{…}` | extra bottom-right line, e.g. `Committee: …` (repeatable) |
| `\logoA{file}` / `\logoB{file}` | logo files: a library name from `logos/` or a file next to the `.tex`. Default `logo_A` / `logo_B`, drawn only if such a file exists. `\logoA{}` = no logo. A file set here but not found shows a labelled box |
| `\logoBcaption{…}` | text beside logo B in the sidebar (default: none) |
| `\themecolors{primary=…, accent=…, highlight=…}` | HTML hex colours, any subset. *primary*: section page and block titles; *accent*: purpose line, current section, bullets; *highlight*: "Section x of n" on the section page. Also `text`, `muted`, `paper`, `sidebar`, `line`, `soft` |
| `\themelabels{section=…, appendix=…, of=…, advisor=…, coadvisor=…}` | the fixed words the theme prints, e.g. another language |
| `\sectiondescription{…}` | line under the title on the current section page |
| `\usetheme[nosectionpages]{acm_academic}` | no automatic section pages |

Footer: `Author · Short title · 3 / 23`. Title and section pages are not
counted; frames after `\appendix` are counted separately.
`\begin{frame}[plain]` hides the sidebar and footer for a full-width slide.

Fonts: IBM Plex Sans / Serif / Mono (package `plex`, available in TeX Live, MiKTeX and
Overleaf). If they are missing the theme falls back to the default fonts.
For finer control than `\themecolors`, the usual `\setbeamercolor` works, e.g.
`\setbeamercolor{section page}{bg=black}`.

## Example: a different university

```latex
\usetheme{acm_academic}
\logoA{acmlogo-myuni}   \logoB{}                 % one logo only
\themecolors{primary=003366, accent=C8102E, highlight=FFC72C}
\themelabels{section=Part, advisor=Supervisor}
```
