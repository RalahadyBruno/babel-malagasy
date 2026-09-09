# babel-malagasy

Support de la langue malgache (tag BCP 47 `mg`) pour le système
**babel** de LaTeX — actuellement au stade **0.1.0,
expérimental**.

```latex
\usepackage{babel-malagasy}
\begin{document}
\selectlanguage{malagasy}
\today            % -> 29 Aogositra 2026
\end{document}
```

## Ce que fait vraiment ce projet

Babel moderne (>= v24.1) fournit déjà des données malgaches
(dates, mois, jours, depuis le CLDR d'Unicode), mais livre ses
**légendes vides** ("Chapter", "Contents", etc. ne sont pas
traduits). `babel-malagasy` complète ces légendes avec des
termes malgaches revus (voir `docs/linguistic-policy.md` pour
les sources et le niveau de confiance de chaque terme), en
utilisant `\setlocalecaption`, la commande officiellement
documentée par babel pour ce cas exact.

Ce choix d'architecture — et pas un fichier `.ldf` classique —
vient d'un test réel : `\usepackage[malagasy]{babel}` seul
échoue ("Unknown option") sur l'installation utilisée pour ce
projet, alors que `\babelprovide[import]{malagasy}` fonctionne
sans erreur. Voir `docs/linguistic-policy.md`, section
"Architecture", pour le détail complet de cette découverte et
des tests qui l'ont confirmée.

## État (v0.1.0) — vérifié dans cette session

Environnement de test : pdfTeX, TeX Live 2023, babel v24.1.

| Fonctionnalité | Statut |
|---|---|
| Chargement du package, `\selectlanguage{malagasy}` | **IMPLEMENTED / TESTED** |
| `\today` (mois validés via tenymalagasy.gov.mg) | **IMPLEMENTED / TESTED** |
| 21 légendes standard (`\setlocalecaption`) | **IMPLEMENTED / TESTED** |
| `\malagasyweekdayname{n}` (extra, non standard babel) | **IMPLEMENTED / TESTED** |
| Document universitaire complet (`examples/`) | **IMPLEMENTED / TESTED** (11 pages, 0 erreur) |
| `l3build check` (6 fichiers `.lvt`) | **TESTED** — "All checks passed" (voir `testfiles/README.md` pour la portée exacte de ces tests) |
| Césure malgache | **EXPERIMENTAL** — pas de vrais patterns hyph-utf8 pour `mg` ; liste d'exceptions manuelle au comportement non confirmé |
| pdfLaTeX | **TESTED** |
| XeLaTeX / LuaLaTeX | **NOT VERIFIED** dans cette session |
| Document à 3 langues (français+malgache+anglais) | **NOT VERIFIED** — l'installation TeX Live utilisée ici n'a pas la collection de langue française de babel ; anglais+malgache, en revanche, a été testé avec succès |
| Acceptation CTAN / intégration TeX Live | **INTEGRE** — 
Le package babel-malagasy est désormais contenu dans TeX Live |

Voir `docs/linguistic-policy.md` pour le détail de chaque choix
terminologique (avec statut `validated` ou `review`).

## Structure du projet

```
babel-malagasy.dtx / .ins   -> génèrent babel-malagasy.sty
docs/                       -> installation, usage, politique linguistique
data/                       -> captions.csv, months.csv, weekdays.csv, corpus.csv
examples/                   -> document universitaire complet
testfiles/                  -> tests l3build (.lvt) + README expliquant leur portée
build.lua                   -> configuration l3build
.github/workflows/tests.yml -> CI (non vérifiée sur GitHub, voir le fichier)
```

## Installation

Voir `docs/installation.md`.

## Auteur

RALAHADY Bruno Bakys — <ralahadybru@yahoo.fr>

## Licence

LPPL 1.3c — voir `LICENSE` et l'en-tête de `babel-malagasy.dtx`.

## Statut du projet

Author-maintained par RALAHADY Bruno Bakys
(<ralahadybru@yahoo.fr>). Contributions et corrections bienvenues,
notamment sur les termes marqués `review` dans
`docs/linguistic-policy.md` et sur la question ouverte de la
césure (un vrai travail de génération de patterns, à contribuer
idéalement au projet hyph-utf8, reste à faire).
