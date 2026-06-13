# Dépôt local Git

## Objectif

Un dépôt local Git permet de versionner un projet sur ma machine.

Quand j’initialise un dépôt avec `git init`, Git crée un dossier caché `.git` qui contient les informations nécessaires pour suivre l’historique du projet.

## Pourquoi c’est important

C’est important car un projet backend doit évoluer proprement.

Avec un dépôt local, je peux :

* suivre les changements dans le projet ;
* enregistrer des versions avec des commits ;
* revenir à un état précédent ;
* travailler plus proprement avant de partager le projet sur GitHub ;
* préparer le travail avec branches, merge et pull requests.

Le dépôt local est donc la base de tout le workflow Git.

## Points clés

* Git est un système de versionnement.
* Un dépôt local est un projet suivi par Git sur ma machine.
* `git init` initialise un dépôt Git dans le dossier courant.
* `.git` est le dossier caché qui contient les données du dépôt.
* `git status` permet de voir l’état du projet.
* Initialiser un dépôt ne suffit pas à enregistrer les fichiers : il faut ensuite utiliser `git add` puis `git commit`.
* Un dépôt local est différent d’un dépôt distant comme GitHub.

## Commandes / exemples

Initialiser un dépôt Git dans le dossier courant :

```bash
git init
```

Voir les fichiers cachés, dont `.git` :

```bash
ls -la
```

Voir l’état du dépôt :

```bash
git status
```

Exemple de démarrage d’un projet :

```bash
mkdir my-project
cd my-project
git init
git status
```

## Ce que ça veut dire

Quand je fais `git init`, je transforme le dossier courant en dépôt Git local.

Git peut alors observer les changements dans ce dossier, mais il ne les enregistre dans l’historique que lorsque je fais un commit.

Le dossier `.git` est essentiel : sans lui, le dossier redevient un dossier normal non versionné.

## Erreurs à éviter

* Initialiser Git dans le mauvais dossier.
* Croire que `git init` enregistre automatiquement tous les fichiers.
* Supprimer le dossier `.git` sans comprendre que cela supprime l’historique local Git.
* Confondre dépôt local et dépôt GitHub.
* Travailler longtemps sans faire de commits.
* Ne pas faire `git status` pour vérifier l’état du projet.

## Utilisé dans

* Projet : tous les projets que je veux versionner proprement.
* Situation concrète : démarrer un nouveau projet Python ou backend.
* Exemple backend : créer un projet `ops-file-audit`, initialiser Git à la racine du projet, puis suivre les changements avec des commits.

## Questions à savoir répondre

1. À quoi sert `git init` ?
2. Qu’est-ce que le dossier `.git` ?
3. Quelle est la différence entre un dépôt local et un dépôt distant ?
4. Pourquoi `git init` ne suffit pas à enregistrer les fichiers ?
5. Pourquoi faut-il lancer `git status` régulièrement ?
6. Que risque-t-il de se passer si j’initialise Git dans le mauvais dossier ?
