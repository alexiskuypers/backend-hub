# Navigation dans le terminal, chemins absolus et relatifs

## Objectif

Savoir me déplacer dans l’arborescence des fichiers de mon système Linux depuis le terminal, et comprendre comment indiquer correctement l’emplacement d’un dossier ou d’un fichier.

## Pourquoi c’est important

Dans un projet backend, je dois pouvoir me placer au bon endroit avant de lancer une commande, inspecter les fichiers du projet, accéder aux dossiers importants et éviter les erreurs liées aux mauvais chemins.

## Points clés

* La navigation permet de se déplacer dans l’arborescence du système.
* `pwd` affiche le chemin absolu du dossier courant.
* `ls` liste le contenu d’un dossier.
* `cd` permet de changer de dossier.
* Un chemin absolu part de la racine `/`.
* Un chemin relatif dépend du dossier courant.
* `.` représente le dossier courant.
* `..` représente le dossier parent.
* `~` représente le dossier personnel de l’utilisateur.

## Commandes / exemples

```bash
pwd
ls
ls -a
ls -l
ls -la
ls -R
cd dossier
cd ..
cd ../..
cd ~
```

Exemple de chemin absolu :

```bash
/home/alex/dev/backend-hub
```

Exemple de chemin relatif :

```bash
src/main.py
```

## Ce que ça veut dire

Ces commandes permettent de savoir où je suis, de voir ce qu’il y a dans un dossier, et de me déplacer correctement dans un projet. Avant de lancer une commande importante, je dois toujours vérifier mon emplacement avec `pwd` et inspecter le contenu avec `ls`.

## Erreurs à éviter

* Agir sans savoir où je suis dans l’arborescence.
* Confondre chemin absolu et chemin relatif.
* Lancer une commande depuis le mauvais dossier.
* Croire que `cd` permet d’ouvrir un fichier alors qu’il sert à changer de dossier.
* Utiliser un chemin relatif sans comprendre qu’il dépend du dossier courant.

## Utilisé dans

* Projet : tous les projets.
* Situation concrète : se placer à la racine du projet avant de lancer une commande.
* Exemple backend : aller dans le dossier du projet, vérifier sa structure, puis lancer un script Python ou une commande Git.

## Questions à savoir répondre

1. Quelles commandes permettent de se repérer et de se déplacer dans l’arborescence ?
2. Quelle est la différence entre un chemin absolu et un chemin relatif ?
3. Que représentent `.`, `..`, `~` et `/` ?
4. Pourquoi faut-il vérifier le dossier courant avant de lancer une commande ?
