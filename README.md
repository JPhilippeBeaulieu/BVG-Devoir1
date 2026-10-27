# 🌿 Cannascope
## Analyse de l’expression de REM16 et FT1 et classification exploratoire du sexe chez *Cannabis sativa*

## Cas d’utilisation

Cannascope est un outil d’analyse développé en **R dans un document R Markdown avec Shiny**, dans le cadre du Devoir 1 du cours **BVG-7003**. Il permet d’explorer le potentiel des gènes **REM16 (LOC115699937)** et **FT1 (LOC115696989)** comme marqueurs du sexe chez *Cannabis sativa*. Son interface permet de consulter un jeu de données de référence ou d’importer un fichier CSV de structure compatible.

## Sommaire

- [Cas d’utilisation](#cas-dutilisation)
- [Organisation du dépôt](#organisation-du-dépôt)
- [Données d’entrée](#données-dentrée)
- [Instructions](#instructions)
- [Environnement utilisé](#environnement-utilisé)
- [Résultats et fichiers produits](#résultats-et-fichiers-produits)
- [Interprétation biologique](#interprétation-biologique)
- [Qualité des données et contrôles](#qualité-des-données-et-contrôles)
- [Autres livrables](#autres-livrables)
- [Dépannage](#dépannage)
- [Utilisation de l’IA](#utilisation-de-lia)

## Cas d’utilisation

### Première partie — Comparaison de l’expression selon le sexe

La première partie compare l’expression des deux gènes chez **138 plantes dont le groupe sexuel est indiqué dans les identifiants des échantillons** du jeu fourni.

Trois figures présentent :

- l’expression de REM16 selon le sexe ;
- l’expression de FT1 selon le sexe ;
- une comparaison des deux gènes.

Les groupes sont définis à partir des suffixes `_XX` et `_XY`, interprétés respectivement comme femelles et mâles pour cette activité. Le sexe n’est pas attribué à partir de l’expression du gène étudié.

### Deuxième partie — Classification exploratoire avec REM16

La deuxième partie propose une classification fondée sur l’expression de REM16, avec un seuil ajustable initialement fixé à **9,5** :

- expression **supérieure au seuil** : femelle prédite ;
- expression **inférieure au seuil** : mâle prédit ;
- expression **égale au seuil ou manquante** : **Non déterminé**.

Un tableau présente les prédictions et leur concordance avec les groupes XX/XY du fichier.

La version actuelle exige des identifiants terminés par `_XX` ou `_XY`. Elle ne prend donc pas encore en charge les plantes sans étiquette sexuelle.

Le seuil dépend de l’échelle d’expression du jeu fourni. Son application à d’autres données nécessite une échelle comparable et une validation indépendante. La concordance calculée sur le jeu de référence ne constitue pas une validation sur de nouvelles plantes.

## Organisation du dépôt

```text
BVG-Devoir1/
├── README.md
├── codes/
│   └── Cannascope_R_Shiny.Rmd
├── data/
│   └── 2_Data_RNASeq_Cannabis_Sex.csv
├── figures/
│   ├── REM16.png
│   ├── FT1.png
│   └── Comparaison.png
├── Question1/
├── Question2/
└── Question4/
```

- **README.md** : présentation de l’outil, installation, utilisation et interprétation des résultats.
- **codes/** : document R Markdown contenant l’analyse, l’interface Shiny et le code commenté.
- **data/** : jeu de données de référence.
- **figures/** : trois figures PNG produites à partir du jeu fourni.
- **Question1/** : confirmation de la configuration de Git et GitHub.
- **Question2/** : résumé scientifique réduit de 500 à 250 mots.
- **Question4/** : proposition de protocole de sexage à haut débit.

Le travail de la Tâche 3 est organisé dans les dossiers **codes/**, **data/** et **figures/**.

Les figures du dépôt ne sont pas remplacées automatiquement après un import. Pour conserver de nouveaux résultats, utiliser le bouton de téléchargement, puis déposer les fichiers souhaités dans le dépôt.

## Données d’entrée

### Chargement du jeu de référence

L’application utilise le fichier **2_Data_RNASeq_Cannabis_Sex.csv** fourni dans le dépôt. Elle recherche d’abord une copie locale dans les emplacements prévus, notamment **data/** à côté du document ou **../data/** lorsque le document est dans **codes/**.

Si le fichier est absent, elle tente de télécharger [le CSV depuis GitHub](https://raw.githubusercontent.com/JPhilippeBeaulieu/BVG-Devoir1/main/data/2_Data_RNASeq_Cannabis_Sex.csv). La source utilisée est indiquée dans l’interface.

Le fichier local permet une utilisation hors ligne. Le téléchargement nécessite Internet. La branche GitHub `main` pouvant évoluer, le fichier local du clone est préférable pour reproduire une version précise.

### Format accepté

Le CSV doit être organisé avec les **gènes en lignes et les plantes en colonnes** :

- **Première colonne** : identifiants de loci, notamment `LOC115699937` pour REM16 et `LOC115696989` pour FT1.
- **Colonnes suivantes** : niveaux d’expression numériques des plantes.
- **En-têtes** : identifiants uniques des plantes terminés par `_XX` ou `_XY`.
- **Séparateur de champs** : virgule ou point-virgule.
- **Séparateur décimal** : point, ou virgule pour les fichiers séparés par des points-virgules.
- **Loci cibles** : une seule ligne par gène demandé.

Le préfixe `Cannabis_` est accepté et retiré avant la recherche exacte des loci.

Exemple de structure avec des valeurs fictives :

```csv
locus,005_XX,006_XX,016_XY,017_XY
Cannabis_LOC115699937,10.4,10.8,8.5,8.9
LOC115696989,6.5,6.7,6.6,6.8
```

Au moins **deux valeurs valides par gène et par groupe sexuel** sont nécessaires. Un effectif différent des 138 plantes attendues est accepté, mais signalé.

La classification utilise REM16, mais l’import exige actuellement les deux gènes et les suffixes XX/XY, afin de permettre également les comparaisons graphiques et l’évaluation de la concordance.

## Instructions

1. **Installer R et RStudio**  
   Installer [R](https://cran.r-project.org/), puis [RStudio Desktop](https://posit.co/download/rstudio-desktop/).

2. **Télécharger le dépôt**  
   Depuis GitHub, sélectionner **Code → Download ZIP**, puis décompresser entièrement l’archive. Il est également possible de cloner le dépôt avec Git. Télécharger **l’ensemble du dépôt** et conserver son organisation.

3. **Installer les packages nécessaires**  
   Ouvrir RStudio et exécuter cette commande dans la **console R**, avant le premier lancement :

   ```r
   install.packages(c(
     "rmarkdown", "shiny", "ggplot2", "plotly",
     "DT", "htmltools", "knitr", "xfun", "zip"
   ))
   ```

   Attendre la fin de l’installation, vérifier qu’aucune erreur n’a été affichée, puis sélectionner **Session → Restart R**.

   Le document vérifie les dépendances, mais **ne les installe pas automatiquement**.

4. **Lancer Cannascope**  
   Ouvrir **Cannascope_R_Shiny.Rmd**, dans le dossier **codes/**, puis cliquer sur **Run Document**. Il n’est pas nécessaire d’exécuter chaque ligne séparément.

5. **Explorer les données de référence**  
   Le CSV local est chargé automatiquement. S’il est absent, l’application tente de le télécharger depuis GitHub. Consulter les onglets **REM16**, **FT1**, **Comparaison**, **Données** et **Exclusions**.

6. **Importer ses propres données**  
   Cliquer sur **Importer un CSV**, puis sélectionner un fichier compatible. Celui-ci doit contenir les gènes en lignes, les plantes en colonnes et les loci `LOC115699937` et `LOC115696989`. Le préfixe `Cannabis_` est accepté. **La version actuelle exige des identifiants de plantes terminés par `_XX` ou `_XY`.**

7. **Consulter la classification exploratoire**  
   Ouvrir l’onglet **Classification exploratoire** pour examiner les prédictions fondées sur REM16 et ajuster le seuil, initialement fixé à **9,5**. Une expression supérieure au seuil conduit à une prédiction femelle, et une expression inférieure à une prédiction mâle. Une valeur égale au seuil ou manquante est classée **Non déterminé**. Ce seuil n’est pas validé pour toutes les données transcriptomiques.

8. **Télécharger les résultats**  
   Cliquer sur **Télécharger les trois figures et les données** pour obtenir les figures PNG, les tableaux CSV et les informations de qualité dans une archive ZIP.

   Le tableau de classification peut également être téléchargé séparément : dans l’onglet **Classification exploratoire**, cliquer sur **Télécharger la classification CSV** pour obtenir **classification_REM16.csv**.

9. **Arrêter l’application**  
   Utiliser le bouton **Stop** dans RStudio. Le processus R doit rester actif pendant l’utilisation de Cannascope.

Aucune modification de chemin propre à un ordinateur n’est nécessaire pour le jeu de données fourni.

## Environnement utilisé

Le lancement de la version corrigée a été confirmé sur l’ordinateur de l’auteur avec :

| Élément | Version |
|---|---|
| R | 4.6.1 — 24 juin 2026 |
| RStudio | 2026.8.1.195 |
| rmarkdown | 2.32 |
| shiny | 1.14.0 |
| ggplot2 | 4.0.3 |
| plotly | 4.12.1 |
| DT | 0.34.0 |
| htmltools | 0.5.9 |
| knitr | 1.52 |
| zip | 3.0.2 |

Les versions des packages correspondent aux téléchargements signalés lors de l’installation. La version de `xfun` n’a pas été consignée dans ce relevé.

Pour vérifier les versions effectivement présentes dans une session :

```r
sessionInfo()
```

Ces versions constituent une référence de fonctionnement, pas une garantie pour tous les ordinateurs. Le projet ne comporte pas de fichier `renv.lock`.

## Résultats et fichiers produits

### Graphiques interactifs

L’application produit trois figures :

- **Niveau d’expression de REM16 en fonction du sexe**
- **Niveau d’expression de FT1 en fonction du sexe**
- **Niveau d’expression de REM16 et FT1 en fonction du sexe**

Chaque point représente une plante. Les boîtes montrent les quartiles et la médiane. Les trois figures utilisent une échelle verticale commune et les mêmes couleurs pour les groupes.

Les graphiques interactifs sont créés avec **Plotly**. Les figures téléchargées sont construites avec **ggplot2**, puis enregistrées au format PNG par R.

### Tableaux

Le tableau des données présente une ligne par mesure, avec l’identifiant de la plante, son groupe sexuel, le gène, son locus et son expression.

Le tableau de classification présente l’expression de REM16, le sexe prédit, le groupe connu, leur concordance et le seuil utilisé.

### Téléchargement

L’archive **Cannascope_resultats.zip** contient :

| Fichier | Contenu |
|---|---|
| `REM16.png` | Expression de REM16 selon le sexe |
| `FT1.png` | Expression de FT1 selon le sexe |
| `Comparaison.png` | Comparaison des deux gènes |
| `expression_REM16_FT1.csv` | Mesures retenues et identifiants |
| `valeurs_exclues.csv` | Mesures manquantes ou infinies exclues |
| `classification_REM16.csv` | Prédictions et seuil utilisé |
| `qualite.txt` | Source active et messages de contrôle |
| `environnement_R.txt` | Informations sur la session R |

Les PNG sont exportés en 10 × 6 pouces à 300 dpi. L’application ne modifie pas le CSV d’origine.

## Interprétation biologique

Dans le jeu fourni, **REM16 présente une expression plus élevée chez les femelles XX que chez les mâles XY**, sans chevauchement des valeurs observées. Ce résultat soutient son intérêt comme marqueur candidat dans ces échantillons.

**FT1 présente des distributions largement superposées et des médianes proches.** Il apparaît moins discriminant dans les conditions étudiées.

Ces observations sont descriptives. L’application ne réalise pas de test statistique ni de validation croisée et ne démontre pas de rôle causal dans le contrôle du sexe.

Le seuil de classification doit être validé sur des plantes indépendantes. Il ne doit pas être transféré directement à une autre échelle de mesure, notamment à des valeurs RT-qPCR.

L’interprétation présentée concerne le **jeu fourni** et ne devient pas automatiquement applicable à un autre fichier importé.

**Lien entre l’exploration, la classification et le protocole proposé.** La première partie montre que l’expression de REM16 sépare les groupes XX et XY dans le jeu fourni, tandis que FT1 présente des distributions largement superposées. Ces observations motivent le choix de REM16 pour la deuxième partie, qui applique un seuil exploratoire de **9,5**, situé entre les valeurs observées des deux groupes. Elles orientent également la proposition de sexage à haut débit de la **Question 4**, fondée sur la mesure de REM16 par RT-qPCR. Cette méthode nécessiterait toutefois une validation expérimentale et une règle de classification propre aux mesures RT-qPCR : le seuil transcriptomique de 9,5 ne peut pas y être transféré directement.

## Qualité des données et contrôles

| Observation | Importance | Traitement |
|---|---|---|
| REM16 est identifié comme `Cannabis_LOC115699937` | Une recherche sans correction manquerait le gène | Retrait du préfixe connu ; identifiant source conservé |
| FT1 est manquant pour `011_XX` | La mesure ne peut pas être représentée | Exclusion de cette mesure et journalisation |
| 20 500 lignes de gènes, contre plus de 34 000 annoncées | Écart avec le contexte de l’activité | Écart signalé ; cause non déterminée |
| Normalisation et transformation non précisées | Impossible d’affirmer une unité TPM, CPM ou log₂ | Conservation de l’échelle fournie |

Après exclusion :

- **REM16** : 69 femelles et 69 mâles ;
- **FT1** : 68 femelles et 69 mâles.

La plante `011_XX` reste incluse pour REM16.

Les valeurs extrêmes finies ne sont pas supprimées. Aucune imputation à zéro ni transformation supplémentaire n’est effectuée.

Les noms de plantes dupliqués, les loci absents ou dupliqués, les suffixes invalides et les valeurs textuelles inattendues provoquent une erreur explicite.

## Autres livrables

### Question 2 — Réduction d’un résumé scientifique

Le dossier **Question2** contient une version réduite à **250 mots** du résumé de 500 mots de l’article *Why Has the Number of Scientific Retractions Increased?* de Steen, Casadevall et Fang (2013). Elle conserve les objectifs, les principaux résultats et la conclusion du texte fourni. Le nombre de mots est indiqué à la fin du document.

### Question 4 — Proposition d’un protocole de sexage

Le dossier **Question4** contient une proposition de sexage à haut débit par **RT-qPCR ciblant REM16**. Ce choix repose sur la séparation observée entre les groupes XX et XY, tandis que FT1 présente des distributions similaires.

Le protocole décrit la collecte et le traitement des échantillons ainsi que l’utilisation envisagée de REM16. Il nécessite une validation expérimentale, notamment des gènes de référence, des conditions de mesure et de la règle de classification. Le seuil transcriptomique de 9,5 ne peut pas être appliqué directement aux mesures RT-qPCR.

## Dépannage

| Problème | Solution |
|---|---|
| Package absent | Installer les packages indiqués, puis redémarrer R |
| Package installé mais impossible à charger | Lire le détail de l’erreur et vérifier les dépendances |
| CSV local absent | Vérifier le dossier `data/` ou la connexion pour le téléchargement GitHub |
| Locus introuvable | Vérifier les identifiants dans la première colonne |
| Suffixe sexuel invalide | Utiliser des noms terminés par `_XX` ou `_XY` |
| Valeur non numérique | Examiner la cellule signalée avant de corriger le fichier |
| Absence de bouton Run Document | Vérifier l’extension `.Rmd` et la présence de `runtime: shiny` dans le YAML |
| Application inactive | Vérifier que le processus R fonctionne toujours |
| ZIP impossible à télécharger | Vérifier que le package R `zip` se charge ; aucun utilitaire ZIP externe n’est requis |
| Import trop volumineux | La limite prévue est de 100 Mo |

### Conflit entre knitr et xfun

Si le document échoue avant l’analyse avec une erreur telle que **object 'attr' is not exported by 'namespace:xfun'** :

1. Redémarrer R.
2. Exécuter dans la console :

   ```r
   install.packages(c("xfun", "knitr", "rmarkdown"))
   ```

3. Redémarrer à nouveau R, puis relancer le document.

Si l’erreur persiste, conserver le message et la sortie de `sessionInfo()` pour le diagnostic. Plusieurs bibliothèques R peuvent contenir des versions différentes.

## Utilisation de l’IA

ChatGPT/Codex a contribué au développement de Cannascope, aux commentaires, à la documentation et aux propositions de vérification.

L’étudiant demeure responsable de comprendre le code, de vérifier les résultats, d’évaluer les propositions de l’IA et de respecter les règles du Devoir 1.


