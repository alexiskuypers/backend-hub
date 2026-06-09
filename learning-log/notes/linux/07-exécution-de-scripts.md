# Exécution de scripts Python

## Objectif

L’exécution de scripts Python permet de lancer un programme Python depuis le terminal, de lui passer des arguments et de lire les erreurs affichées dans le terminal.

## Pourquoi c’est important

C’est important car un projet backend ou un outil CLI ne doit pas dépendre uniquement de l’IDE.

Je dois être capable de lancer un script depuis le terminal, comprendre si la commande a réussi ou échoué, identifier les arguments attendus et lire les erreurs pour diagnostiquer le problème.

Dans un projet Python, cela sert à :

* lancer un fichier Python ;
* lancer un module Python ;
* passer un chemin de dossier ou de fichier en argument ;
* tester une commande CLI ;
* comprendre une erreur Python affichée dans le terminal.

## Points clés

* `python fichier.py` lance un fichier Python.
* `python fichier.py argument` lance un fichier Python avec un argument.
* `python -m module` lance un module Python.
* Les arguments sont des informations données au programme depuis la ligne de commande.
* Une erreur terminal donne souvent le fichier, la ligne et le type d’erreur.
* Il faut lancer la commande depuis le bon dossier ou utiliser le bon chemin.
* Un script peut réussir ou échouer avec un code de sortie.

## Commandes / exemples

Lancer un script Python simple :

```bash
python main.py
```

Lancer un script avec un argument :

```bash
python main.py example/
```

Lancer un module Python :

```bash
python -m mini_file_audit.cli
```

Lancer un module avec des arguments :

```bash
python -m mini_file_audit.cli example/ --recursive
```

Afficher l’aide d’une commande CLI :

```bash
python -m mini_file_audit.cli --help
```

Exemple avec un chemin de sortie :

```bash
python -m mini_file_audit.cli example/ --output output/report.csv
```

## Ce que ça veut dire

Exécuter un script Python depuis le terminal signifie demander au système de lancer Python avec un fichier ou un module précis.

Exemple :

```bash
python main.py example/
```

Ici :

* `python` lance l’interpréteur Python ;
* `main.py` est le fichier exécuté ;
* `example/` est un argument passé au programme.

Dans un outil CLI, les arguments permettent de donner des informations au programme, par exemple :

* quel dossier analyser ;
* quel fichier produire ;
* quelle option activer ;
* quel mode utiliser.

## Lire les erreurs terminal

Quand une commande échoue, le terminal affiche souvent une traceback.

Exemple simplifié :

```text
File "main.py", line 12, in <module>
    open("missing.txt")
FileNotFoundError: [Errno 2] No such file or directory: 'missing.txt'
```

Je dois repérer :

* le fichier concerné ;
* la ligne concernée ;
* le type d’erreur ;
* le message d’erreur ;
* la cause probable.

Ici, l’erreur signifie que le programme essaie d’ouvrir un fichier qui n’existe pas.

## Erreurs à éviter

* Lancer le script depuis le mauvais dossier.
* Confondre fichier Python et module Python.
* Oublier un argument obligatoire.
* Ne pas lire la traceback.
* Copier une commande sans comprendre chaque morceau.
* Penser que “ça ne marche pas” suffit comme diagnostic.
* Utiliser le mauvais Python ou le mauvais environnement virtuel.
* Confondre une erreur de chemin, une erreur de permission et une erreur Python.

## Utilisé dans

* Projet : surtout utile dans les projets CLI, scripts Python, outils d’automatisation et backend local.
* Situation concrète : lancer un outil Python depuis le terminal et comprendre ses erreurs.
* Exemple projet : dans `ops-file-audit`, lancer la commande qui analyse un dossier et produit un rapport CSV.

Exemple :

```bash
python -m mini_file_audit.cli example/ --output output/report.csv
```

## Questions à savoir répondre

1. Quelle est la différence entre `python main.py` et `python -m module` ?
2. À quoi sert un argument en ligne de commande ?
3. Dans `python main.py example/`, que représente `example/` ?
4. Que dois-je regarder dans une traceback Python ?
5. Pourquoi le dossier courant est important quand je lance un script ?
6. Quelle commande permet d’afficher l’aide d’une CLI ?
7. Que peut signifier une erreur `FileNotFoundError` ?
8. Que peut signifier une erreur `Permission denied` ?

## Résumé personnel

Exécuter un script Python depuis le terminal permet de lancer un programme sans dépendre de l’IDE.
Je dois savoir passer des arguments, utiliser `--help`, vérifier le dossier courant et lire les erreurs pour comprendre ce qui bloque.
