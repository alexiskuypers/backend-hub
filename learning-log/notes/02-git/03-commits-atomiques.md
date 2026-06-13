# Commits atomiques

## Objectif

Un commit enregistre une version du projet à un moment précis dans l’historique Git.

Un commit atomique est un commit qui contient un seul changement logique.

Exemples :

* créer l’architecture initiale du projet ;
* ajouter une commande CLI ;
* corriger un bug précis ;
* mettre à jour le README ;
* ajouter des tests pour une fonctionnalité.

Chaque commit possède un identifiant unique appelé hash et un message qui décrit le changement enregistré.

## Pourquoi c’est important

Les commits atomiques permettent de garder un historique clair et exploitable.

Dans un projet backend, cela permet de :

* comprendre l’évolution du projet étape par étape ;
* retrouver facilement quand une modification a été faite ;
* isoler une correction de bug ;
* revenir plus facilement à un état précédent ;
* faciliter la relecture du code en collaboration ;
* éviter de mélanger plusieurs sujets dans un même commit.

Un bon historique Git rend le projet plus professionnel et plus facile à maintenir.

## Points clés

* Un commit enregistre les changements préparés dans la staging area.
* Un commit atomique contient un seul changement logique.
* Le message de commit doit être court, clair et utile.
* Avant de committer, je dois vérifier l’état du projet avec `git status`.
* Avant un commit important, je dois vérifier les modifications avec `git diff`.
* Un historique propre permet de comprendre la construction du projet.
* Un mauvais commit mélange plusieurs changements sans logique claire.

## Commandes / exemples

Voir l’état du projet :

```bash
git status
```

Voir les changements avant de les préparer :

```bash
git diff
```

Ajouter un fichier précis :

```bash
git add README.md
```

Créer un commit :

```bash
git commit -m "add project README"
```

Lire l’historique de manière courte :

```bash
git log --oneline
```

Exemples de bons messages :

```bash
git commit -m "add initial project structure"
git commit -m "add CLI argument parsing"
git commit -m "fix missing output directory handling"
git commit -m "update README usage examples"
```

Exemples de mauvais messages :

```bash
git commit -m "update"
git commit -m "fix"
git commit -m "final"
git commit -m "test"
```

## Ce que ça veut dire

Un commit atomique sert à enregistrer une étape claire du projet.

Je ne dois pas mettre dans le même commit une correction de bug, une modification du README, un renommage de fichiers et une nouvelle fonctionnalité si ces changements ne forment pas un seul sujet cohérent.

L’objectif est que quelqu’un puisse lire l’historique et comprendre rapidement ce qui a été fait, pourquoi, et dans quel ordre.

## Erreurs à éviter

* Faire un énorme commit avec plusieurs sujets mélangés.
* Utiliser des messages vagues comme `update`, `fix`, `test` ou `final`.
* Faire un commit sans vérifier `git status`.
* Faire un commit sans regarder `git diff` quand les changements sont importants.
* Ajouter tous les fichiers avec `git add .` sans vérifier.
* Commiter des fichiers inutiles comme `.venv`, caches, logs ou fichiers générés.
* Attendre trop longtemps avant de committer.

## Utilisé dans

* Projet : tous les projets versionnés avec Git.
* Situation concrète : enregistrer une étape propre du projet.
* Exemple backend : créer l’architecture du projet puis faire un commit dédié.

Exemple :

```bash
git add pyproject.toml README.md src/
git commit -m "add initial project structure"
```

Autre exemple :

```bash
git add src/cli.py
git commit -m "add CLI argument parsing"
```

## Questions à savoir répondre

1. Qu’est-ce qu’un commit ?
2. Qu’est-ce qu’un commit atomique ?
3. Pourquoi faut-il éviter les commits énormes ?
4. Pourquoi `update` est un mauvais message de commit ?
5. Quelle commande permet de lire l’historique des commits ?
6. Pourquoi faut-il faire `git status` avant de committer ?
7. Quelle est la différence entre `git add` et `git commit` ?
