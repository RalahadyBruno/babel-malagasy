# Changelog

## [0.1.0] - 2026-08-29

Première version, expérimentale.

### Ajouté
- `babel-malagasy.dtx` / `.ins` générant `babel-malagasy.sty`.
- Chargement de la locale malgache déjà fournie par babel via
  `\babelprovide[import]{malagasy}`.
- Les 21 légendes standard de babel traduites en malgache via
  `\setlocalecaption` (statuts `validated`/`review` documentés
  dans `docs/linguistic-policy.md` et `data/captions.csv`).
- `\malagasyweekdayname{n}`, extension non standard donnant le
  nom du jour de la semaine en malgache.
- Liste d'exceptions de césure expérimentale (`\hyphenation{}`).
- Documentation : `docs/installation.md`, `docs/usage.md`,
  `docs/linguistic-policy.md`.
- Données : `data/captions.csv`, `data/months.csv`,
  `data/weekdays.csv`, `data/corpus.csv`.
- Exemple d'intégration complet :
  `examples/university-example.tex` (compilé avec succès,
  11 pages).
- Suite de tests `l3build` (`testfiles/*.lvt`), "All checks
  passed" sur pdfTeX/TeX Live 2023/babel v24.1 — voir
  `testfiles/README.md` pour la portée exacte de ces tests.
- `.github/workflows/tests.yml` (non vérifié sur GitHub dans
  cette session).

### Non implémenté / expérimental
- Aucun pattern de césure statistiquement généré (pas de
  `hyph-mg.tex` dans hyph-utf8 à ce jour).
- Aucun test réalisé avec XeLaTeX ou LuaLaTeX.
- Aucun test réussi à 3 langues (français+malgache+anglais) :
  limite de l'environnement de test, pas du package (voir
  `docs/linguistic-policy.md`).
- Aucune soumission CTAN ni intégration TeX Live.
