gkbibtex
========

** Gary King's bibtex files

* gk.bib - references from many papers; feel free to add whatever references you like, following rules listed at the top of the file

* gkpubs.bib - references (co)authored by Gary King

* gkbib.tex - drop-in preamble (after `biblatex`) so the same paper works
  locally, for coauthors, and on Overleaf. Do **not** use
  `location=remote` / raw.githubusercontent.com (slow, cached, Overleaf
  cannot fetch it).

In the paper, after `\usepackage{biblatex}`:

```latex
\input{gkbib}
```

Keep `gkbib.tex`, `gk.bib`, and `gkpubs.bib` in the paper folder (Overleaf
needs the copies). Refresh them from this repo with `./sync-gkbib` run in
that folder. If `gkbibtex` is cloned next to the paper repo (the usual
`~/Documents/github/` layout), latex uses those live files and ignores the
copies — so your own builds stay fast.
