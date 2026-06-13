# README de base

## Objectif

Un `README.md` sert à expliquer rapidement ce qu’est un projet, comment l’installer, comment le lancer et comment le tester.

C’est le premier fichier qu’une personne voit en arrivant sur un repo GitHub.

## Pourquoi c’est important

Le README permet à quelqu’un d’autre de comprendre le projet sans devoir lire tout le code.

Dans un projet backend Python, il doit permettre de savoir :

* ce que fait le projet ;
* pourquoi il existe ;
* comment l’installer ;
* comment l’utiliser ;
* comment lancer les tests ;
* quelles compétences le projet montre ;
* quelles sont ses limites.

## Structure minimale

Un README de base peut contenir :

```md
# Nom du projet

Description courte du projet.

## Objectif

Explication du problème ou du but du projet.

## Fonctionnalités

- Fonctionnalité 1
- Fonctionnalité 2
- Fonctionnalité 3

## Installation

Commandes pour installer le projet.

## Utilisation

Commandes pour lancer le projet.

## Tests

Commandes pour lancer les tests.

## Compétences travaillées

- Python
- CLI
- Git
- Tests
- Logs

## Limites

Ce que le projet ne fait pas encore.
```

## Commandes / exemples

Installer un projet Python en mode développement :

```bash
pip install -e .
```

Afficher l’aide d’une CLI :

```bash
nom-du-projet --help
```

Lancer les tests :

```bash
pytest
```

Exemple d’utilisation dans un README :

```bash
mini-file-audit examples/sample-folder --recursive --csv-output output/report.csv
```

## Ce que ça veut dire

Un bon README ne doit pas seulement décrire le projet.

Il doit donner des commandes concrètes pour qu’une autre personne puisse tester le projet elle-même.

Un README utile répond à trois questions :

* C’est quoi ?
* Comment je l’installe ?
* Comment je le lance ?

## Erreurs à éviter

* Avoir un repo sans README.
* Écrire une description trop vague.
* Ne pas donner de commandes d’installation.
* Ne pas donner de commande d’utilisation.
* Ne pas expliquer comment lancer les tests.
* Ne pas montrer d’exemple concret.
* Oublier d’indiquer les limites du projet.
* Mettre un README qui ne correspond plus au projet réel.

## Utilisé dans

* Projet : tous les projets publics.
* Situation concrète : publier un projet sur GitHub pour qu’il soit compréhensible et lançable.
* Exemple backend : documenter une CLI Python avec installation, utilisation, exemple de sortie et tests.

## Questions à savoir répondre

1. À quoi sert un README ?
2. Pourquoi le README est-il le premier fichier important d’un repo public ?
3. Quelles sections minimales doit contenir un README utile ?
4. Pourquoi faut-il mettre des commandes concrètes ?
5. Quelle différence entre décrire un projet et rendre un projet lançable ?

## Résumé personnel

Un README de base sert à rendre un projet compréhensible et utilisable.
Il doit expliquer le but du projet, les fonctionnalités, l’installation, l’utilisation, les tests et les limites.
