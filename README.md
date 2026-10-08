# 🧬 Les oLLMpiques 2026 | oLLMpics 2026

### Défi bioinformatique collaboratif · Collaborative Bioinformatics Challenge

**Navigation :** [Français](#francais) · [English](#english) · [Structure du dépôt / Repository structure](#repository-structure)

> **Important — ce dépôt devient votre Devoir 1.**  
> Chaque étudiant·e doit travailler dans **son propre dépôt GitHub public**. Pendant les oLLMpiques, vous pouvez résoudre les tâches en équipe, mais chacun·e doit conserver et pousser les livrables dans son propre dépôt.

---

<a id="francais"></a>
# 🇫🇷 Français

## Objectif

Bienvenue aux **oLLMpiques 2026**. Vous travaillerez en équipe sur quatre tâches de bioinformatique conçues pour réviser des compétences vues dans le cours et comparer différentes façons de résoudre un problème avec ou sans l'aide d'un grand modèle de langage (LLM), comme **Microsoft Copilot** ou **ChatGPT**.

Il ne s'agit **pas d'une compétition entre les équipes**. Travaillez ensemble, discutez de vos approches et avancez à votre rythme.

Pour les quatre tâches des oLLMpiques :

- choisissez **deux tâches** à réaliser avec l'aide d'un LLM;
- réalisez les **deux autres sans LLM**, en utilisant par exemple Google, vos notes de cours ou l'aide de l'équipe enseignante.

> Cette règle concerne **l'activité en classe**. Après les oLLMpiques, les règles d'utilisation de l'IA du **Devoir 1** sont celles indiquées dans les consignes officielles du devoir.

## Votre dépôt GitHub individuel

Chaque étudiant·e doit créer son **propre dépôt GitHub** pour cette activité. Ce dépôt servira ensuite de point de départ pour le **Devoir 1**.

À la fin de l'activité, votre dépôt doit notamment contenir les dossiers `Question_1`, `Question_2` et `Question_4`. Le travail de la **Tâche 3** sera ensuite développé en outil reproductible pour le devoir.

<a id="repository-structure"></a>
### Structure recommandée

```text
votre-depot/
├── Question_1/
│   └── README.md
├── Question_2/
│   └── ...
├── Question_4/
│   └── ...
├── code/
├── data/
├── figures/
└── README.md
```

Les dossiers `code/`, `data/` et `figures/` peuvent être créés ou réorganisés après l'activité lorsque vous développerez la Tâche 3 pour le Devoir 1.

---

## Tâche 1 — Préparer votre dépôt GitHub

Clonez le dépôt du cours afin d'accéder aux fichiers nécessaires pour les tâches suivantes, puis préparez votre **dépôt GitHub personnel** qui contiendra votre travail.

**Livrable**

- Créez le dossier `Question_1/` dans votre dépôt personnel.
- Ajoutez-y un petit fichier `README.md` indiquant simplement que la configuration Git/GitHub a été complétée.
- Faites au moins un `commit` et un `push` vers votre dépôt GitHub personnel.

> Les dossiers vides ne sont pas suivis par Git; le fichier `README.md` permet donc de conserver `Question_1/` dans votre dépôt.

---

## Tâche 2 — Réduire un résumé scientifique à 250 mots

Vous avez reçu le résumé d'un article scientifique :

**Titre :** *Why Has the Number of Scientific Retractions Increased?*  
**Auteurs :** R. Grant Steen, Arturo Casadevall, Ferric C. Fang  
**Revue :** *PLOS ONE*  
**Année :** 2013

Le texte se trouve dans le dossier contenant les fichiers fournis pour l'activité.

Votre objectif est de réduire le résumé de 500 mots à **exactement 250 mots**.

**Livrable**

- Placez la version révisée dans `Question_2/`.
- Indiquez le **nombre de mots** à la fin du document.
- Vous pouvez vérifier le nombre de mots avec **bash**, **Python**, ou une autre méthode appropriée.

**Conseil :** il est souvent plus facile de lire un fichier Markdown directement dans GitHub que dans `nano`.

---

## Tâche 3 — Analyser l'expression de REM16 et FT1

### Contexte biologique

Vous êtes une équipe de biologistes computationnels qui étudie le contrôle génétique du sexe chez *Cannabis sativa*. Deux gènes, **REM16** (`LOC115699937`) et **FT1** (`LOC115696989`), sont considérés comme des marqueurs candidats permettant de distinguer les plantes mâles et femelles.

Vous disposez d'un jeu de données d'expression génique normalisée provenant de **138 plantes**. Le jeu de données contient plus de **34 000 gènes**.

### Votre tâche

À l'aide de **R** ou **Python** :

1. extrayez les données d'expression de **REM16** (`LOC115699937`);
2. extrayez les données d'expression de **FT1** (`LOC115696989`);
3. produisez trois figures :
   - un boxplot de l'expression de **REM16** selon le sexe;
   - un boxplot de l'expression de **FT1** selon le sexe;
   - une figure combinée comparant l'expression des deux gènes, avec les groupes sexuels clairement identifiés.

Utilisez les **identifiants de loci** pour trouver les gènes dans le jeu de données, mais utilisez les noms **REM16** et **FT1** dans vos figures. Choisissez des axes, étiquettes et unités qui rendent les figures faciles à interpréter.

Si vous rencontrez un problème de qualité ou de structure dans les données, votre code doit le traiter explicitement.

**Livrables pour l'activité en classe**

- un script R/Python, un document RMarkdown ou un notebook Jupyter;
- les trois figures demandées.

### Lien avec le Devoir 1

Cette tâche constitue le **point de départ du Devoir 1**. Après l'activité, vous développerez cette analyse en un outil reproductible dans votre dépôt GitHub personnel. Le Devoir 1 demandera notamment une organisation claire du code, des données et des figures, des instructions d'exécution reproductibles, une interprétation biologique et un court walkthrough vidéo.

Les exigences détaillées et les critères d'évaluation se trouvent dans les **consignes et la rubrique officielles du Devoir 1**.

---

## Tâche 4 — Concevoir un protocole de sexage à haut débit

À partir des données transcriptomiques analysées à la Tâche 3, proposez une méthode à haut débit permettant de déterminer le sexe de plantes de cannabis à l'aide de **REM16**, **FT1**, ou des deux marqueurs.

Dans votre proposition, considérez notamment :

- la collecte et le traitement des échantillons;
- les étapes permettant de déterminer le sexe à partir des marqueurs;
- l'adaptation de la méthode à un contexte à haut débit.

**Livrable**

- une proposition de **250 mots maximum** au format `.txt` ou `.md`;
- placez le fichier dans `Question_4/` de votre dépôt personnel.

---

## À la fin des oLLMpiques

Avant de quitter la classe, vérifiez que :

- votre travail est dans **votre propre dépôt GitHub**;
- `Question_1/`, `Question_2/` et `Question_4/` sont présents et contiennent leurs livrables;
- votre travail initial pour la Tâche 3 est sauvegardé et poussé sur GitHub;
- votre dépôt est prêt à être développé pour le **Devoir 1**.

---

<a id="english"></a>
# 🇬🇧 English

## Objective

Welcome to the **2026 oLLMpics**. You will work through four bioinformatics tasks as a team. The activity is designed to reinforce skills from the course while comparing different approaches to problem solving with and without a large language model (LLM), such as **Microsoft Copilot** or **ChatGPT**.

This year, the two teams are **not competing against each other**. Work together, discuss your approaches, and progress through the tasks at your own pace.

Across the four oLLMpics tasks:

- choose **two tasks** to complete with the help of an LLM;
- complete the **other two without an LLM**, using resources such as Google, your course notes, or help from the teaching team.

> This restriction applies to the **in-class activity**. After the oLLMpics, AI use for **Assignment 1** is governed by the rules in the official assignment instructions.

## Your individual GitHub repository

Each student must create and maintain **their own GitHub repository** for this activity. That repository will then become the starting point for **Assignment 1**.

By the end of the activity, your repository should contain `Question_1`, `Question_2`, and `Question_4` directories. Your work from **Task 3** will be developed further into the reproducible analysis tool assessed in Assignment 1.

### Recommended structure

```text
your-repository/
├── Question_1/
│   └── README.md
├── Question_2/
│   └── ...
├── Question_4/
│   └── ...
├── code/
├── data/
├── figures/
└── README.md
```

The `code/`, `data/`, and `figures/` directories can be created or reorganized after the activity as you develop Task 3 for Assignment 1.

---

## Task 1 — Prepare your GitHub repository

Clone the course repository so that you can access the files needed for the remaining tasks, then prepare the **personal GitHub repository** that will contain your work.

**Deliverable**

- Create a `Question_1/` directory in your personal repository.
- Add a short `README.md` stating that the Git/GitHub setup was completed.
- Make at least one `commit` and `push` to your personal GitHub repository.

> Git does not track empty directories, so the small `README.md` ensures that `Question_1/` remains in your repository.

---

## Task 2 — Trim a scientific abstract to 250 words

You have been provided with the abstract of the following scientific article:

**Title:** *Why Has the Number of Scientific Retractions Increased?*  
**Authors:** R. Grant Steen, Arturo Casadevall, Ferric C. Fang  
**Journal:** *PLOS ONE*  
**Year:** 2013

The text is available in the folder containing the files supplied for the activity.

Your goal is to reduce the 500-word abstract to **exactly 250 words**.

**Deliverable**

- Place the revised abstract in `Question_2/`.
- Print the **word count** at the bottom of the document.
- You may check the word count using **bash**, **Python**, or another appropriate method.

**Tip:** it is often easier to read a Markdown file directly on GitHub than in `nano`.

---

## Task 3 — Analyze REM16 and FT1 expression

### Biological background

You are a team of computational biologists investigating the genetic control of sex in *Cannabis sativa*. Two genes, **REM16** (`LOC115699937`) and **FT1** (`LOC115696989`), are being considered as candidate markers for distinguishing male and female plants.

You have been provided with normalized gene-expression data from **138 plants**. The dataset contains more than **34,000 genes**.

### Your task

Using **R** or **Python**:

1. extract expression data for **REM16** (`LOC115699937`);
2. extract expression data for **FT1** (`LOC115696989`);
3. generate three figures:
   - a box plot of **REM16** expression grouped by plant sex;
   - a box plot of **FT1** expression grouped by plant sex;
   - a combined figure comparing expression of both genes, with sex groups clearly identified.

Use the **locus IDs** to identify the genes in the dataset, but use the names **REM16** and **FT1** in your figures. Choose axes, labels, scales, and units that make the figures easy to interpret.

If you encounter a genuine data-quality or data-structure problem, address it explicitly in your code.

**In-class deliverables**

- an R/Python script, RMarkdown document, or Jupyter notebook;
- the three required figures.

### Connection to Assignment 1

This task is the **starting point for Assignment 1**. After the in-class activity, you will develop this analysis into a reproducible tool in your personal GitHub repository. Assignment 1 will require, among other things, clear organization of code, data, and figures; reproducible execution instructions; biological interpretation; and a short video walkthrough.

See the **official Assignment 1 instructions and rubric** for the complete requirements and grading criteria.

---

## Task 4 — Design a high-throughput sexing protocol

Using the transcriptomic data analyzed in Task 3, propose a high-throughput method for determining the sex of cannabis plants using **REM16**, **FT1**, or both markers.

In your proposal, consider:

- the workflow for collecting and processing samples;
- the steps needed to determine plant sex using the markers;
- how the method could be scaled to a high-throughput setting.

**Deliverable**

- a proposal of **no more than 250 words** in `.txt` or `.md` format;
- place the file in `Question_4/` of your personal repository.

---

## Before you finish the oLLMpics

Check that:

- your work is stored in **your own GitHub repository**;
- `Question_1/`, `Question_2/`, and `Question_4/` are present and contain their deliverables;
- your initial Task 3 analysis has been saved and pushed to GitHub;
- your repository is ready to be developed further for **Assignment 1**.


## Copyright and use

© 2026 Adrian Monthony. All rights reserved.

These materials are provided for educational use by students enrolled in BVG-7003 and may be used, modified, and submitted as required for participation in the course.

Any reproduction, distribution, modification, or reuse of these materials by individuals or organizations outside BVG-7003 requires prior written permission from the author.
