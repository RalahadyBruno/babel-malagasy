# Installation

## Statut

`babel-malagasy` v0.1.0 est un projet **expérimental**. Il n'est
pas sur le CTAN et n'est pas intégré à TeX Live — voir
README.md pour le détail de ce qui est vérifié ou non.

## Prérequis

- Une distribution TeX Live (ou MiKTeX) relativement récente
  avec **babel v24.1 ou plus récent** (le babel "moderne", à
  base de fichiers `.ini`). Vérifiez avec :

  ```
  kpsewhich -version babel.sty
  ```

  Ce projet a été développé et testé avec pdfTeX, TeX Live 2023,
  babel v24.1. Les moteurs XeLaTeX et LuaLaTeX n'ont pas été
  testés dans cette session (voir README.md, "Limitations").

## Installation manuelle (recommandée pour l'instant)

1. Récupérez `babel-malagasy.dtx` et `babel-malagasy.ins`.
2. Générez le fichier de package :

   ```
   tex babel-malagasy.ins
   ```

   Cela produit `babel-malagasy.sty`.
3. Placez `babel-malagasy.sty` :
   - soit dans le même dossier que votre document `.tex`
     (pratique pour tester) ;
   - soit dans votre arbre `texmf` personnel, par exemple :

     ```
     ~/texmf/tex/latex/babel-malagasy/babel-malagasy.sty
     ```

     puis lancez `texhash` (TeX Live) ou `initexmf --update-fndb`
     (MiKTeX).

## Utilisation minimale

```latex
\usepackage{babel-malagasy}
\begin{document}
\selectlanguage{malagasy}
\today
\end{document}
```

Voir `docs/usage.md` pour le multilinguisme et les exemples
complets, et `examples/university-example.tex` pour un document
universitaire complet.
