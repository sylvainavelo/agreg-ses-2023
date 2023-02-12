# agreg-ses-2023

Tentative d'extraction de la bibliographie du programme de l'agrégation externe 2023.

## Contexte et objectif

Dans le [programme](https://media.devenirenseignant.gouv.fr/file/agreg_externe/20/5/p2023_agreg_ext_ses_1426205.pdf) publié le 3 mai 2022 il y a 66 pages de bibliographie.

Le programme commence par 12 pages et 217 références de bibliographie pour le seul nouveau thème **Economie de l'éducation**.

L'objectif est d'en tirer le plus automatiquement possible un tableau avec nom et prénom des auteurs, année et titre. Les autres informations ont une importance moindre.

## Tentative avec JabRef

L'idée ici est de transformer la liste de références "à plat" en une base de données bibliographique au format de référence **BibTex** qui est plus facilement exportable sous différentes formes.

Le fichier [economie-de-l-education.txt](economie-de-l-education.txt) contient les références brutes dans un format importable par le logiciel [JabRef](https://www.jabref.org/), c'est-à-dire avec chaque référence sur une seule ligne et séparée de la suivante par deux lignes blanches. Par rapport au PDF du sujet, seuls les guillemets anglais et français semblaient poser un problème à JabRef à l'import et ont été retirés de certains titres.

Le fichier [economie-de-l-education.bib](economie-de-l-education.bib) est le résultat de l'import de cette liste de références dans **JabRef** avec enregistrement au format **BibTex**.

Les instructions pour réaliser un tel import sont données dans l['aide en ligne de JabRef](https://docs.jabref.org/collect/newentryfromplaintext).

JabRef utilise un service externe pour transformer les références qui s'appelle [GROBID](https://github.com/kermitt2/grobid), pour **G**ene**R**ation **O**f **B**Ibliographic **D**ata.

Format initial :

```txt
Acemoglu D., 2015, Prospérité, puissance et pauvreté : Pourquoi certains pays réussissent mieux que d'autres, Editions Markus Haller.

Acemoglu D., Johnson S., Robinson J.A., Yared P., 2005, From Education to Democracy?, The American Economic Review, Vol. 95, No. 2.
```

Format BibTex :

```bibtex
@Article{Acemoglu2015,
  author    = {Acemoglu, D},
  journal   = {Revue Projet},
  title     = {<b>PROSPÉRITÉ, PUISSANCE ET PAUVRETÉ</b>. Pourquoi certains pays réussissent mieux que d’autres},
  year      = {2015},
  number    = {5},
  pages     = {93a},
  volume    = {N° 354},
  date      = {2015},
  doi       = {10.3917/pro.354.0094},
  publisher = {CAIRN},
}

@Article{Acemoglu2005,
  author    = {Acemoglu, Daron and Johnson, Simon and Robinson, James and Yared, Pierre},
  journal   = {SSRN Electronic Journal},
  title     = {From Education to Democracy?},
  year      = {2005},
  number    = {2},
  volume    = {95},
  date      = {2005},
  doi       = {10.2139/ssrn.668542},
  publisher = {Elsevier BV},
}
```

Ici les informations de publication de la source (*Editions Markus Haller* et *The American Economic Review*) ont été remplacées par une référence doi (**D**igital **O**bject **I**dentifier) et d'autres éditeurs : *CAIRN* et *Elsevier BV*. Ces références doi sont remplacées par des liens dans l'application, respectivement https://doi.org/10.3917/pro.354.0094 qui redirige vers le site https://www.cairn.info/revue-projet-2016-5-page-93a.htm?ref=doi et https://doi.org/10.2139/ssrn.668542 qui redirige vers https://papers.ssrn.com/sol3/papers.cfm?abstract_id=668542. Ainsi toutes les références du BibTex qui comportent un doi sont cliquables.

Si pour la majorité des références la conversion est correcte, le service fait ce qu'il peut avec les références en entrée qui ont parfois des erreurs de format et des informations sont perdues au passage :

Ainsi :

```txt
Aghion P., Dewatripont M., Hoxby C., Mas-Colell A., Sapir A., [2007], Why Reform Europe’s Universities?, Bruegel.
```

devient :

```bibtex
@Misc{Aghion2007,
  author = {Aghion, P and Dewatripont, M and Hoxby, C and Mas-Colell, A and Sapir, A},
  year   = {2007},
  date   = {2007},
}
```

Le titre de l'ouvrage et l'éditeur sont complètement perdus.

## Tentative avec ChatGPT

En fournissant les 10 premières lignes de [economie-de-l-education.txt](economie-de-l-education.txt) avec l'instruction :

```txt
Montre moi le code source (à copier) d'un tableau markdown avec les colonnes : Auteurs, Année, Titre et Publication. Complète les auteurs avec leur prénom complet, dans l'ordre nom prénom sans séparer nom et prénom par une virgule.
```

Il a fallu de nombreuses tentatives pour obtenir un tableau presque correct (l'ordre nom prénom n'est pas respecté) :

Auteurs | Année | Titre | Publication
---|---|---|---
Daron Acemoglu | 2015 | Prospérité, puissance et pauvreté : Pourquoi certains pays réussissent mieux que d'autres | Editions Markus Haller
Daron Acemoglu, Simon Johnson, James A. Robinson, Philippe Yared | 2005 | From Education to Democracy? | The American Economic Review, Vol. 95, No. 2
Daron Acemoglu, Joshua Angrist | 2000 | How large are the social returns to education ? Evidence from compulsory schooling laws | NBER Macroeconomics Annual, p. 9-59
Daron Acemoglu, Philippe Aghion, Fabrizio Zilibotti | 2002 | Distance to Frontier, Selection and Economic Growth | NBER Working Paper #9066
Zoltan J. Acs | 2002 | The Emergence of the Knowledge Economy | Springer
Philippe Aghion, Emmanuel Cohen | 2004 | Éducation et croissance | La Documentation française
Philippe Aghion, Peter Howitt | 1992 | A Model of Growth through Creative Destruction | Econometrica, 60, p.323-351
Philippe Aghion, Peter Howitt | 1998 | Endogenous Growth Theory | MIT Press
Philippe Aghion, Mathias Dewatripont, Caroline Hoxby, Andreu Mas-Colell, André Sapir | 2007 | Why Reform Europe’s Universities? | Bruegel
Yann Algan, Éric Huillery, Caroline Prost | 2018 | Confiance, coopération et autonomie : pour une école du XXIe siècle | Conseil d'analyse économique, 12 p.

Comme ChatGPT est limitée en nombre de caractères saisis et que la réponse est parfois à regénérer, il faut découper la demande en plusieurs petites demandes et la procédure est finalement aussi chronophage qu'une opération manuelle avec un risque relativement important d'erreur.

## Tentative manuelle

Le tableau est dans [economie-de-l-education.md](economie-de-l-education.md).

Les informations sur l'éditeur, le numéro de la revue ou les pages ont été supprimées.