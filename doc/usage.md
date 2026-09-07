# Usage

## Chargement de base

```latex
\usepackage{babel-malagasy}
\begin{document}
\selectlanguage{malagasy}
\today
\end{document}
```

`babel-malagasy` charge `babel` lui-même si besoin
(`\RequirePackage{babel}`), importe la locale malgache déjà
fournie par babel (`\babelprovide[import]{malagasy}`), puis
complète les 21 légendes standard (chapitre, table des matières,
figure, tableau, etc.) qui sont vides dans les données babel
d'origine — voir `docs/linguistic-policy.md` pour le détail et
les sources.

## Document multilingue

Testé avec succès dans cet environnement (anglais + malgache) :

```latex
\usepackage{babel-malagasy}   % fournit "malagasy"
% le "main"/langue de babel reste celle par défaut si vous
% n'ajoutez pas d'options; changez-la explicitement si besoin :
% \babelprovide[import, main]{english}
\begin{document}
\selectlanguage{english}
Today: \today

\selectlanguage{malagasy}
Andro anio: \today

\foreignlanguage{malagasy}{Andro anio} and in English.
\end{document}
```

Pour ajouter le français (ou une autre langue déjà connue de
babel) dans le même document, la commande directe
`\babelprovide[import]{french}` a fonctionné de façon fiable
dans nos tests, y compris quand l'option de package
`\usepackage[french]{babel}` échouait dans cet environnement
faute de collection de langue installée (voir
`docs/linguistic-policy.md`) :

```latex
\usepackage{babel-malagasy}
\babelprovide[import]{french}
\begin{document}
\selectlanguage{french}
\today

\selectlanguage{malagasy}
\today
\end{document}
```

## Changement de langue

```latex
\selectlanguage{malagasy}   % change la langue "courante"
\foreignlanguage{malagasy}{...}   % change la langue localement,
                                    % pour un mot ou un paragraphe
```

## Date

```latex
\selectlanguage{malagasy}
\today
```
donne par exemple `29 Aogositra 2026` (mois validés auprès de
tenymalagasy.gov.mg, voir `data/months.csv`).

## Jour de la semaine (extra, non standard babel)

```latex
\malagasyweekdayname{3} % -> Alarobia (mercredi ; 1 = lundi)
```

Ce n'est pas une commande babel standard (aucune locale babel
n'a de commande "jour de la semaine" native) ; c'est une petite
extension propre à `babel-malagasy`, documentée comme telle.

## Exemple complet

Voir `examples/university-example.tex` : page de titre, table
des matières, listes de figures/tableaux, chapitres, figure,
tableau, annexe, section en français, bibliographie. Compilé
avec succès dans cette session (`pdflatex`, 11 pages, aucune
erreur).
