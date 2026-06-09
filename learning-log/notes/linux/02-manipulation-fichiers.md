# Manipulation de fichiers

## Objectif

La manipulation de fichiers permet de créer, copier, déplacer, renommer et supprimer des fichiers ou des dossiers depuis le terminal.

## Pourquoi c’est important

C’est nécessaire pour démarrer un projet, créer son architecture, organiser les fichiers et nettoyer ce qui n’est plus utile.

Dans un projet backend, cela sert par exemple à créer des dossiers comme `src/`, `tests/`, `docs/`, `logs/` ou `output/`.

## Points clés

* Créer un dossier ou un fichier.
* Copier un fichier ou un dossier.
* Déplacer un fichier ou un dossier.
* Renommer un fichier ou un dossier.
* Supprimer un fichier ou un dossier.
* Vérifier où je suis avant de supprimer quelque chose.

## Commandes / exemples

```bash
mkdir src
mkdir tests
touch README.md
touch main.py
cp main.py main_backup.py
cp -r src src_backup
mv main.py app.py
mv app.py src/
rm fichier.txt
rm -r dossier
```

Commande dangereuse :

```bash
rm -rf dossier
```

`rm -rf` supprime récursivement et force la suppression. Ne pas l’utiliser sans vérifier précisément où je suis et ce que cela supprime.

## Ce que ça veut dire

Ces commandes permettent d’organiser les fichiers d’un projet directement depuis le terminal.
`mkdir` crée un dossier.
`touch` crée un fichier vide.
`cp` copie.
`mv` déplace ou renomme.
`rm` supprime.

Avant une suppression, il faut vérifier mon emplacement avec `pwd` et le contenu du dossier avec `ls`.

## Erreurs à éviter

* Utiliser `rm -rf` par réflexe.
* Supprimer un dossier sans vérifier le dossier courant.
* Confondre déplacement et copie.
* Oublier que `mv` peut servir à renommer ou déplacer.
* Copier un dossier sans `-r`.

## Utilisé dans

* Projet : tous les projets, notamment `ops-file-audit`.
* Situation concrète : créer l’architecture d’un projet.
* Exemple backend : créer `src/`, `logs/`, `output/`, `README.md`, puis déplacer les fichiers au bon endroit.

## Questions à savoir répondre

1. Quelle est la différence entre `cp` et `mv` ?
2. Pourquoi `rm -rf` est dangereux ?
3. Quelle commande permet de créer un dossier ?
4. Quelle commande permet de créer un fichier vide ?
