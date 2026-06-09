# Inspection de fichiers

## Objectif

L’inspection de fichiers permet d’afficher, parcourir et filtrer le contenu d’un fichier depuis le terminal.

Elle sert à lire rapidement un fichier, vérifier son contenu, afficher seulement une partie ou rechercher une information précise.

## Pourquoi c’est important

C’est important car dans un projet backend, on doit souvent inspecter des fichiers sans passer par l’IDE :

* lire un fichier de configuration ;
* vérifier un fichier généré ;
* consulter un log ;
* chercher une erreur ;
* afficher le début ou la fin d’un fichier ;
* filtrer les lignes utiles.

## Points clés

* `cat` affiche tout le contenu d’un fichier.
* `less` permet de lire un fichier long page par page.
* `head` affiche le début d’un fichier.
* `tail` affiche la fin d’un fichier.
* `grep` cherche du texte dans un fichier.
* `find` cherche des fichiers ou dossiers dans une arborescence.
* Pour les gros fichiers, `less`, `tail` et `grep` sont souvent plus adaptés que `cat`.

## Commandes / exemples

Afficher tout le fichier :

```bash
cat fichier.txt
```

Lire un long fichier page par page :

```bash
less fichier.txt
```

Afficher les 5 premières lignes :

```bash
head -n 5 fichier.txt
```

Afficher les 10 dernières lignes :

```bash
tail -n 10 fichier.txt
```

Suivre un fichier log en direct :

```bash
tail -f logs/app.log
```

Chercher les lignes contenant `error` :

```bash
grep "error" fichier.txt
```

Chercher sans tenir compte des majuscules/minuscules :

```bash
grep -i "error" fichier.txt
```

Afficher aussi les numéros de ligne :

```bash
grep -n "error" fichier.txt
```

Chercher tous les fichiers Python dans le projet :

```bash
find . -name "*.py"
```

## Ce que ça veut dire

Inspecter un fichier, ce n’est pas forcément le modifier.
C’est surtout savoir lire son contenu, chercher une information précise ou vérifier une sortie générée par un programme.

Par exemple, si mon programme crée un fichier log, je peux utiliser `tail` pour voir les dernières lignes ou `grep` pour extraire seulement les erreurs.

## Erreurs à éviter

* Utiliser `cat` sur un très gros fichier au lieu de `less`, `head`, `tail` ou `grep`.
* Confondre `grep` et `find`.
* Croire que `grep` cherche des fichiers : il cherche du texte dans les fichiers.
* Croire que `find` cherche du texte : il cherche des fichiers ou dossiers.
* Ne pas inspecter les logs quand une commande échoue.
* Oublier que `head` affiche le début et `tail` affiche la fin.

## Utilisé dans

* Projet : surtout utile dans les projets avec logs, fichiers générés, fichiers de configuration ou rapports.
* Situation concrète : filtrer le contenu d’un long fichier, afficher les premières lignes d’un CSV, lire les dernières lignes d’un log.
* Exemple backend : chercher les erreurs dans un fichier log.

```bash
grep -i "error" logs/app.log
```

Autre exemple : vérifier les premières lignes d’un rapport CSV.

```bash
head -n 5 output/report.csv
```

## Questions à savoir répondre

1. Quelle est la différence entre `cat` et `less` ?
2. Quelle est la différence entre `head` et `tail` ?
3. Quelle est la différence entre `grep` et `find` ?
4. Quelle commande permet de voir les dernières lignes d’un fichier log ?
5. Quelle commande permet de chercher le mot `ERROR` dans un fichier ?
6. Pourquoi `cat` n’est pas idéal pour un très gros fichier ?
