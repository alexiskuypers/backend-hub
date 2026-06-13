# Suivi des changements

## Objectif

Le suivi des changements permet de voir ce qui a été créé, modifié ou supprimé dans un projet depuis le dernier commit.

Git organise le travail en trois zones principales :

* le `working directory` : l’espace où je modifie les fichiers du projet ;
* la `staging area` : la zone où je prépare les changements pour le prochain commit ;
* l’historique Git : l’ensemble des commits déjà enregistrés.

## Pourquoi c’est important

C’est important car cela permet de contrôler l’évolution d’un projet avant d’enregistrer une nouvelle version.

Dans un projet backend, je dois pouvoir voir précisément ce que j’ai modifié avant de faire un commit : ajout d’un fichier, correction d’un bug, modification d’un README, ajout de logs, changement de configuration, etc.

Cela évite de committer des fichiers inutiles, des erreurs ou des changements mélangés.

## Points clés

* `git status` montre l’état actuel du projet.
* `git diff` montre les modifications non encore ajoutées à la staging area.
* `git add` prépare des fichiers pour le prochain commit.
* `git commit` enregistre les changements préparés dans l’historique.
* Un fichier nouveau est souvent affiché comme `untracked`.
* Un fichier déjà suivi et modifié est affiché comme `modified`.
* Un fichier ajouté avec `git add` devient `staged`.
* Git suit les fichiers, pas les dossiers vides.

## Commandes / exemples

Voir l’état du projet :

```bash
git status
```

Voir les modifications exactes non staged :

```bash
git diff
```

Ajouter un fichier à la staging area :

```bash
git add README.md
```

Ajouter tous les changements du dossier courant :

```bash
git add .
```

Voir ce qui est prêt à être commit :

```bash
git status
```

Enregistrer les changements préparés :

```bash
git commit -m "add project README"
```

Voir les changements déjà staged :

```bash
git diff --staged
```

## Ce que ça veut dire

Quand je modifie un fichier, Git peut détecter que le projet a changé.

Avec `git status`, je vois quels fichiers sont nouveaux, modifiés, supprimés ou prêts à être commit.

Avec `git diff`, je peux voir exactement quelles lignes ont été changées.

Avec `git add`, je sélectionne les changements que je veux mettre dans le prochain commit.

Avec `git commit`, j’enregistre officiellement ces changements dans l’historique Git.

## Erreurs à éviter

* Faire un commit sans regarder `git status`.
* Ajouter tous les fichiers avec `git add .` sans vérifier ce qui va être inclus.
* Confondre `git add` et `git commit`.
* Croire que `git add` sauvegarde définitivement les changements.
* Commiter plusieurs sujets différents dans le même commit.
* Ajouter des fichiers inutiles comme `.venv`, logs, caches ou fichiers générés.
* Oublier de lire `git diff` avant un commit important.

## Utilisé dans

* Projet : tous les projets versionnés avec Git.
* Situation concrète : vérifier les fichiers modifiés avant de faire un commit.
* Exemple backend : ajouter des logs dans un outil CLI, vérifier les changements avec `git diff`, puis préparer seulement les bons fichiers avec `git add`.

## Questions à savoir répondre

1. À quoi sert `git status` ?
2. Quelle est la différence entre `working directory`, `staging area` et historique Git ?
3. Quelle est la différence entre `git add` et `git commit` ?
4. À quoi sert `git diff` ?
5. Que signifie `untracked` ?
6. Pourquoi faut-il éviter `git add .` sans vérifier ?
7. Pourquoi Git ne suit-il pas les dossiers vides ?
