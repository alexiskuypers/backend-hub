# Pipes et redirections

## Objectif

Les pipes et redirections permettent de chaîner des commandes terminal et de contrôler où va la sortie d’une commande.

Un pipe `|` envoie la sortie d’une commande vers une autre commande.

Une redirection `>` ou `>>` envoie la sortie d’une commande vers un fichier.

## Pourquoi c’est important

C’est important car cela permet de filtrer des résultats, sauvegarder une sortie terminal dans un fichier, créer des rapports simples et inspecter plus facilement des logs ou des fichiers générés.

Dans un projet backend, cela peut servir à extraire les lignes d’erreur d’un fichier log, sauvegarder le résultat d’une commande ou produire un fichier temporaire d’analyse.

## Points clés

* `|` transmet la sortie d’une commande à une autre commande.
* `>` écrit la sortie dans un fichier en écrasant son contenu.
* `>>` ajoute la sortie à la fin d’un fichier.
* `grep` est souvent utilisé avec les pipes pour filtrer du texte.
* Une redirection ne modifie pas la commande elle-même, elle change seulement la destination de sa sortie.

## Commandes / exemples

Afficher uniquement les lignes contenant `ERROR` :

```bash
cat logs/app.log | grep "ERROR"
```

Faire la même chose plus directement :

```bash
grep "ERROR" logs/app.log
```

Enregistrer les erreurs dans un fichier :

```bash
grep "ERROR" logs/app.log > errors.txt
```

Ajouter une ligne à un fichier sans écraser le contenu :

```bash
echo "nouvelle ligne" >> notes.txt
```

Lister les fichiers et enregistrer le résultat :

```bash
ls -la > files.txt
```

Compter le nombre de fichiers Python trouvés :

```bash
find . -name "*.py" | wc -l
```

## Ce que ça veut dire

Une commande terminal produit souvent une sortie affichée à l’écran.

Avec `|`, je peux envoyer cette sortie vers une autre commande pour la filtrer ou la transformer.

Avec `>` ou `>>`, je peux envoyer cette sortie vers un fichier au lieu de l’afficher seulement dans le terminal.

## Erreurs à éviter

* Utiliser `>` au lieu de `>>` et écraser un fichier existant.
* Chaîner des commandes sans comprendre ce que la première commande envoie à la deuxième.
* Utiliser `cat fichier | grep texte` quand `grep texte fichier` suffit.

## Utilisé dans

* Projet : surtout utile dans les projets avec logs, fichiers générés ou sorties terminal.
* Situation concrète : filtrer un fichier log ou sauvegarder une sortie terminal.
* Exemple backend : extraire les lignes contenant `ERROR` depuis `logs/app.log` et les enregistrer dans `errors.txt`.

## Questions à savoir répondre

1. À quoi sert `|` dans le terminal ?
2. Quelle est la différence entre `>` et `>>` ?
3. Comment extraire les lignes contenant `ERROR` d’un fichier log ?
4. Comment sauvegarder le résultat d’une commande dans un fichier ?
