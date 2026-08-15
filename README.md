# gkbibtex

Shared bibliography for Gary King’s papers. Clone this repo **next to**
each paper (the usual `~/Documents/github/` layout):

```text
~/Documents/github/gkbibtex/
~/Documents/github/sibs/
~/Documents/github/my-new-paper/
```

Do **not** use `\addbibresource[location=remote]{https://raw.githubusercontent.com/...}`.
That is slow, GitHub caches it for minutes, and Overleaf cannot fetch it.

## Files

| File | Who edits it | Where it lives |
|---|---|---|
| `gk.bib` | Gary only | this repo (copies in each paper are snapshots) |
| `gkpubs.bib` | Gary only | this repo — **nobody else edits this** |
| `refs.bib` | Coauthors (paper-local cites) | each paper’s tex folder |
| `gkbib.tex` | — | preamble snippet; copy into the paper |

`sync-gkbib` copies `gk.bib`, `gkpubs.bib`, and `gkbib.tex` into a paper.
It never touches `refs.bib`.

`absorb-refs` appends to `gk.bib` any `refs.bib` entries whose keys are
not already there. It never writes `gkpubs.bib`. It is not a git merge.

## Preamble (same for everyone)

After `\usepackage{biblatex}`:

```latex
\input{gkbib}
```

Latex looks for `gk.bib` / `gkpubs.bib` in this order (first hit wins):

1. A `gkbibtex` clone next to the paper (your machine)
2. A `gkbibtex/` folder in the project (optional submodule)
3. Copies sitting next to the `.tex` file (Overleaf / paper-only clone)

Then it loads `refs.bib` from the paper folder if that file exists.

## You, on an existing paper (e.g. sibs)

Edit references in **this** repo (`gk.bib` / `gkpubs.bib`). Run `ltx` in
the paper — it uses these live files. No wait.

When Overleaf or a coauthor needs a cite you just added:

```sh
cd ~/Documents/github/sibs/text
~/Documents/github/gkbibtex/sync-gkbib
# then commit and push the paper
```

To fold coauthor cites from `refs.bib` into `gk.bib`:

```sh
~/Documents/github/gkbibtex/absorb-refs ~/Documents/github/sibs/text/refs.bib
# then commit and push gkbibtex; sync-gkbib if Overleaf should get the new gk.bib
```

If a key is already in `gk.bib`, that `refs.bib` entry is skipped. Same
paper under two different keys: both stay until you delete one by hand.

## You, creating a new paper repo

1. Clone the paper next to `gkbibtex` (see layout above).
2. After `\usepackage{biblatex}`, add `\input{gkbib}`.
3. In the folder with the `.tex` file:

```sh
~/Documents/github/gkbibtex/sync-gkbib
cat > refs.bib <<'EOF'
% Paper-local cites only. Do not edit gk.bib or gkpubs.bib.
EOF
```

4. Commit `gkbib.tex`, `gk.bib`, `gkpubs.bib`, and `refs.bib`.

## Coauthors (not Overleaf)

Clone the paper and build. Use the copies of `gk.bib` / `gkpubs.bib` in
the paper. Add new cites only to `refs.bib`. Do not edit `gk.bib` or
`gkpubs.bib`. No preamble changes.

If they also clone `gkbibtex` next to the paper, they get the same
live-file behavior as you.

## Coauthors on Overleaf

Overleaf is the paper project only. It uses the copies in the project
plus `refs.bib`. Nothing to configure.

When they add a cite: they edit `refs.bib` in Overleaf. When you want
that in the shared file: `absorb-refs`, then `sync-gkbib` and push the
paper so Overleaf’s `gk.bib` matches.

## Adding entries to gk.bib

Check the key is not already there, then add at the **end**. Key rules
(or use Google Scholar’s key):

- one author: `Tobler79`
- up to three authors: `KinTomWit00`
- extra letter if needed: `King02`, `King02b` (first has no `a`)
