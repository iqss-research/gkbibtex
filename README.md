gkbibtex
========

** Gary King's bibtex files

* gk.bib - shared references (you maintain this)

* gkpubs.bib - references (co)authored by Gary King (do not edit)

* refs.bib - lives in each **paper** folder; coauthors add cites there only

* gkbib.tex - drop-in preamble (after `biblatex`) so the same paper works
  locally, for coauthors, and on Overleaf. Do **not** use
  `location=remote` / raw.githubusercontent.com (slow, cached, Overleaf
  cannot fetch it).

In the paper, after `\usepackage{biblatex}`:

```latex
\input{gkbib}
```

Keep `gkbib.tex`, `gk.bib`, and `gkpubs.bib` in the paper folder (Overleaf
needs the copies). Refresh those three from this repo with `./sync-gkbib`
run in that folder (`refs.bib` is left alone). If `gkbibtex` is cloned next
to the paper repo, latex uses those live files for `gk*.bib`.

Coauthors edit only `refs.bib`. To fold new keys into `gk.bib` (append
anything not already there; not a git merge):

```sh
./absorb-refs /path/to/paper/text/refs.bib
```
