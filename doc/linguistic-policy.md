# Politique linguistique de babel-malagasy

Ce document explique quelle variété de malgache est visée, d'où
viennent les choix terminologiques, quel est leur niveau de
confiance, et où se trouvent les points encore incertains. Rien
ici n'est présenté comme une norme officielle si elle ne l'est
pas.

## Variété visée

Le malgache officiel (dit "malgache des Hautes Terres" /
Merina), tel qu'utilisé dans l'enseignement, l'administration et
les médias nationaux à Madagascar. C'est aussi la variété
couverte par les données CLDR déjà présentes dans babel (tag
BCP 47 `mg`, script latin). Les autres dialectes (betsileo,
sakalava, etc.) ne sont pas traités par ce projet.

## Architecture : ce qu'on a essayé d'abord, et pourquoi ça a changé

Le brouillon initial de ce projet écrivait un fichier `.ldf`
classique (`\LdfInit`, `\ldf@finish`, à la manière de
`bosnian.ldf` ou `finnish.ldf`). En testant réellement ce
fichier avec `pdflatex` (TeX Live 2023, babel v24.1), deux faits
se sont révélés :

1. **Babel fournit déjà des données malgaches.** Le cœur de
   babel embarque `locale/mg/babel-mg.ini` et
   `locale/mg/babel-malagasy.tex`, dérivés du CLDR d'Unicode.
   Ces données donnent des mois, des jours et un `\today`
   corrects, mais leurs sections `[captions]` et
   `[captions.licr]` sont **vides** dans le fichier ini.
2. **Le mécanisme `.ldf` hérité n'est pas ce qui est consulté.**
   `\usepackage[malagasy]{babel}` seul échoue avec
   `! Package babel Error: Unknown option 'malagasy'` dans cet
   environnement, car malgache n'est pas (encore) dans la liste
   des options reconnues de babel. En revanche,
   `\babelprovide[import]{malagasy}` charge correctement les
   données ini existantes, sans erreur.

La documentation de babel indique explicitement la commande à
utiliser quand une légende manque pour une locale ini :
`\setlocalecaption{<locale>}{<legende>}{<valeur>}` — c'est
exactement le message d'avertissement que babel a lui-même
affiché pendant nos tests :

```
Package babel Warning: \contents not set for 'malagasy'. Please,
(babel)                \setlocalecaption{malagasy}{contents}{..}
```

Le brouillon `.ldf` a donc été abandonné et remplacé par un
petit package `babel-malagasy.sty` qui appelle
`\babelprovide[import]{malagasy}` puis vingt-et-une fois
`\setlocalecaption`. C'est peu de code, mais chaque commande est
une commande babel réelle et documentée, pas une invention.

Tests réels effectués (voir `testfiles/basic.lvt`) :

- `\usepackage{babel-malagasy}` puis `\selectlanguage{malagasy}`
  puis `\today` → `29 Aogositra 2026` (correct).
- Les 21 légendes standard rendent le texte malgache attendu
  (`Toko`, `Fanoroan-takila`, `Sary`, etc.), sans avertissement
  "not set".
- `\providehyphenmins{malagasy}{2}{2}` (à la façon d'un vieux
  `.ldf`) a provoqué une erreur `Missing \begin{document}`,
  parce que cette commande ne prend que DEUX arguments dans
  babel moderne (`{malagasy}{22}`), pas trois. Corrigé et
  reconfirmé sans erreur.
- Un test à trois langues (français + malgache + anglais) n'a
  pas pu être mené à bien dans cet environnement, car
  l'installation TeX Live disponible ici ne contient pas la
  collection de langue française de babel (`\usepackage[french]
  {babel}` seul échoue aussi, avec la même erreur "Unknown
  option"). C'est une limite de cet environnement de test, pas
  un problème spécifique au malgache. La combinaison
  anglais + malgache, elle, a été testée avec succès.

## Légendes (captions) : sources et statut

| Légende (clé babel) | Malgache | Statut | Source / remarque |
|---|---|---|---|
| chapter | Toko | validated | Attesté dans des manuels scolaires malgaches ("Ahitana toko roa ity fizarana ity") |
| contents | Fanoroan-takila | review | Attesté dans un document gouvernemental malgache ; variante "Fizahan-takila" également répandue (manuels scolaires) — les deux formes existent, aucune norme unique trouvée |
| abstract | Famintinana | validated | Terme courant pour "résumé/résumé de mémoire" |
| bib / ref | Bibliografia | review | Emprunt direct au français ; aucun terme natif standard trouvé dans les sources consultées |
| preface | Teny fanolorana | validated | Attesté comme en-tête de préface dans un document public |
| appendix | Fanampiny | review | Sens général "ajout, supplément" ; pas de confirmation dans un contexte académique précis |
| figure | Sary | validated | Terme courant pour "image, figure" |
| table | Tabilao | review | Emprunt ("tableau") vu dans des contextes statistiques ; pourrait être confondu avec "latabatra" (meuble table) |
| part | Fizarana | review | Sens général "partie, section" ; peut se chevaucher avec l'usage de "toko" selon les documents |
| index | Fanondroana | review | Construction régulière ("action de désigner/indiquer"), non confirmée dans un index académique réel |
| listfigure | Lisitry ny sary | review | Construction compositionnelle ("liste" + "des figures"), non attestée telle quelle |
| listtable | Lisitry ny tabilao | review | Idem, dépend du choix pour "tabilao" |
| encl | Rakitra atovana | review | Choix provisoire, faible confiance ; à revoir |
| cc | Kopia | review | Emprunt direct, plausible mais non confirmé dans un contexte de correspondance officielle |
| headto | Ho an'i | review | Choix provisoire ; babel l'utilise rarement (lettres) |
| page | Takila | validated | Confirmé par l'usage dans "Fanoroan-takila" / "Fizahan-takila" (table **des pages**) |
| see | Jereo | validated | Impératif courant de "regarder/voir" |
| also | Jereo koa | review | Construction compositionnelle de "Jereo", non attestée telle quelle |
| proof | Porofo | review | Emprunt mathématique plausible, non confirmé dans un manuel malgache |
| glossary | Rakibolana | validated | Terme courant pour "dictionnaire/glossaire" |

"validated" signifie : trouvé tel quel dans au moins une source
publique consultée pendant la préparation de ce projet.
"review" signifie : choix de travail raisonnable, mais pas
confirmé par une source publique consultée — à vérifier par un
locuteur ou une source académique avant un usage officiel.

## Dates : mois et jours

Les noms de mois et de jours viennent directement des données
CLDR déjà embarquées dans babel (`babel-mg.ini`), et ont été
recoupés avec le site de la Commission malgache de la langue
(tenymalagasy.gov.mg, page "Ahitsio ny diso" — "corrigez les
fautes"), qui liste explicitement les formes correctes :
Janoary, Febroary, Marsa, Avrily, Mey, Jona, Jolay, Aogositra,
Septambra, Oktobra, Novambra, Desambra ; et les jours :
Alatsinainy, Talata, Alarobia, Alakamisy, Zoma, Sabotsy (ou
"Asabotsy"), Alahady. Statut : **validated**. C'est la source la
plus autoritative trouvée pendant ce projet.

Aucun format de date ordinal ("faha-29 Aogositra 2026") n'est
implémenté dans la v0.1.0 ; babel utilise un format numérique
simple. Question ouverte pour une version future.

## Césure (hyphenation)

**Statut : EXPERIMENTAL / NON VALIDÉ.** Il n'existe, à la date de
préparation de ce projet, aucun fichier de patterns de césure
statistiquement généré pour le malgache dans le projet
hyph-utf8 (le code ISO 639-1 `mg` n'apparaît dans aucun
`hyph-mg.tex` trouvé). Générer de vrais patterns nécessiterait
la chaîne complète décrite dans le prompt d'origine (corpus →
syllabation → patgen → validation), qui dépasse ce que ce projet
peut accomplir de façon honnête en une seule session : on ne
fabrique pas de patterns par extrapolation créative.

Ce que fournit la v0.1.0 à la place : une courte liste
d'exceptions de césure (`\hyphenation{...}`), découpées à la
main selon une syllabation raisonnable (consonne-voyelle) pour
les mots du corpus de test. Un test réel avec `\showhyphens` a
montré un résultat qui ne correspond pas exactement à la coupure
attendue, ce qui suggère que le mécanisme d'exception n'est pas
pleinement fiable pour la locale malgache dans cette version de
babel (peut-être parce qu'aucun pattern réel n'est chargé pour
son emplacement de langue). Ce point reste ouvert.

La vraie suite logique serait de contribuer un jeu de patterns
au projet hyph-utf8 (tex-hyphen@tug.org) une fois un corpus
suffisant validé linguistiquement — pas de le refaire en
parallèle dans ce package.

## Corpus

Voir `data/corpus.csv`. Les mots proviennent de la liste fournie
dans la demande d'origine (mots courants, dérivés, vocabulaire
scientifique et universitaire) ; leur statut est `manual`
(saisis manuellement, syllabation non vérifiée par un locuteur
natif ni par un outil de syllabation automatique). Aucun mot
n'est marqué `validated`.

## Questions ouvertes

- Confirmer "Fanoroan-takila" vs "Fizahan-takila" pour la table
  des matières.
- Confirmer "Tabilao" vs une alternative pour "tableau" (donnée
  chiffrée) sans ambiguïté avec le meuble.
- Vérifier "Fanampiny", "Rakitra atovana", "Ho an'i", "Kopia",
  "Porofo" auprès d'un locuteur ou d'une source académique.
- Décider s'il faut un format de date ordinal.
- Lancer un vrai travail de génération de patterns de césure
  (hors du périmètre de cette session).
