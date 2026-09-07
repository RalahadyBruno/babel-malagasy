# À propos des tests dans ce dossier

Résultat réel obtenu en préparant ce projet : `l3build check`
rapporte **"All checks passed"** sur les 6 fichiers `.lvt`
(pdfTeX, TeX Live 2023, babel v24.1).

**Ce que ces tests vérifient réellement :** que le chargement de
`babel-malagasy.sty`, `\selectlanguage{malagasy}`,
`\foreignlanguage`, `\today`, les 21 légendes standard et
`\malagasyweekdayname` ne produisent **aucune erreur ou
avertissement TeX inattendu**, comparé à une trace de référence
(`.tlg`) enregistrée avec `l3build save`.

**Ce que ces tests ne vérifient PAS automatiquement :** le texte
exact produit par chaque légende. La normalisation de log par
défaut de `l3build` filtre les avertissements de boîtes
(`Overfull`/`Underfull hbox`) utilisés ici pour faire apparaître
le texte réellement composé — une technique nécessaire car
`\today` et les légendes des locales "ini" de babel moderne ne
sont pas utilisables telles quelles dans `\message{}` (voir
`docs/linguistic-policy.md`). En conséquence, les fichiers
`.tlg` de ce projet sont vides : ils ne capturent que "aucune
erreur ne s'est produite", pas les valeurs textuelles.

La vérification du contenu texte réel (ex. `\chaptername` →
"Toko", `\today` → "29 Aogositra 2026") a été faite manuellement
pendant le développement, en compilant des documents réels avec
`pdflatex` puis en extrayant le texte du PDF avec `pdftotext` —
voir `examples/university-example.tex`, qui sert justement de
test d'intégration visuel/manuel complémentaire à `l3build
check`.

Si vous améliorez ces tests pour qu'ils vérifient aussi le texte
exact (par exemple avec un mécanisme d'écriture dans un fichier
auxiliaire plutôt que les boîtes surchargées), pensez à relancer
`l3build save` pour régénérer des références non vides.
