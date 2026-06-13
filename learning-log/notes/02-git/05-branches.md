# Branches Git

## Objectif

Une branche Git permet de créer une ligne de travail séparée dans l’historique du projet.

Elle permet de développer une fonctionnalité, corriger un bug ou tester une modification sans intégrer directement ces changements dans la branche principale `main`.

## Pourquoi c’est important

Les branches permettent de travailler proprement sur un projet sans mélanger tous les changements.

Dans un projet backend, je peux créer une branche pour :

* ajouter une nouvelle fonctionnalité ;
* corriger un bug ;
* modifier une structure de fichiers ;
* tester une idée ;
* préparer une pull request.

Cela évite de modifier directement `main`, qui doit rester une version stable ou validée du projet.

## Points clés

* Une branche est une ligne de travail séparée dans l’historique Git.
* `main` est souvent la branche principale.
* Les commits sont ajoutés sur la branche active.
* `git branch` affiche les branches locales.
* `git switch -c nom-branche` crée une nouvelle branche et bascule dessus.
* `git switch nom-branche` permet de changer de branche.
* `git branch -d nom-branche` supprime une branche locale déjà fusionnée.
* Avant de changer de branche, il vaut mieux vérifier l’état du projet avec `git status`.

## Commandes / exemples

Afficher les branches locales :

```bash
git branch
```

Créer une branche et aller dessus :

```bash
git switch -c add-cli-parser
```

Changer de branche :

```bash
git switch main
```

Revenir sur une branche de travail :

```bash
git switch add-cli-parser
```

Supprimer une branche locale déjà fusionnée :

```bash
git branch -d add-cli-parser
```

Vérifier la branche actuelle et l’état du projet :

```bash
git status
```

## Ce que ça veut dire

Quand je crée une branche, je crée une ligne de travail séparée.

Si je fais des commits sur cette branche, ils ne sont pas encore dans `main`. Ils pourront être intégrés plus tard avec un merge ou une pull request.

Une branche ne crée pas un deuxième dossier du projet. Elle change simplement la ligne d’historique Git sur laquelle je travaille.

## Erreurs à éviter

* Travailler directement sur `main` pour une nouvelle fonctionnalité.
* Créer des branches avec des noms vagues comme `test`, `modif` ou `new`.
* Oublier de vérifier la branche active avant de modifier des fichiers.
* Changer de branche avec des modifications non commitées sans comprendre ce qui va se passer.
* Garder trop de vieilles branches inutiles.
* Croire qu’une branche isole tout l’environnement Python ou les fichiers générés.

## Utilisé dans

* Projet : tous les projets versionnés avec Git quand il y a plusieurs évolutions à gérer.
* Situation concrète : créer une branche pour développer une fonctionnalité sans toucher directement à `main`.
* Exemple backend : créer une branche pour ajouter une commande CLI à `ops-file-audit`.

Exemple :

```bash
git switch -c add-output-option
```

Puis après les modifications :

```bash
git add src/cli.py
git commit -m "add output option to CLI"
```

## Questions à savoir répondre

1. À quoi sert une branche Git ?
2. Quelle est la différence entre `main` et une branche de travail ?
3. Quelle commande permet de créer une branche et de basculer dessus ?
4. Comment savoir sur quelle branche je suis ?
5. Pourquoi éviter de travailler directement sur `main` ?
6. Est-ce qu’une branche crée un deuxième dossier du projet ?
7. Pourquoi faut-il faire `git status` avant de changer de branche ?
