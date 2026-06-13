# Repo public propre

## Objectif

Un repo public propre est un projet publié sur GitHub de manière lisible, compréhensible et exécutable par quelqu’un d’autre.

L’objectif n’est pas seulement de mettre le code en ligne.
L’objectif est que quelqu’un puisse comprendre :

* ce que fait le projet ;
* comment l’installer ;
* comment le lancer ;
* comment le tester ;
* quelles compétences le projet démontre ;
* quelles sont ses limites.

## Pourquoi c’est important

C’est important parce qu’un recruteur, un développeur ou un mentor ne va pas deviner l’intention du projet.

Un repo public propre permet de montrer :

* ma capacité à organiser un projet ;
* ma capacité à documenter mon travail ;
* ma capacité à utiliser Git et GitHub proprement ;
* ma capacité à rendre un projet exécutable ;
* ma capacité à expliquer les choix et les limites.

Dans un projet backend Python, le repo doit permettre à une autre personne de cloner le projet, installer les dépendances, lancer l’application ou les tests, et comprendre rapidement ce qui a été fait.

## Points clés

* Le repo doit avoir un nom clair.
* Le projet doit contenir un `README.md` utile.
* Le README doit expliquer l’objectif du projet.
* Le README doit contenir des commandes d’installation et d’utilisation.
* Le projet doit être exécutable depuis le terminal.
* Le repo doit contenir un `.gitignore` adapté.
* Les fichiers inutiles ne doivent pas être commités.
* Les secrets ne doivent jamais être publiés.
* L’historique Git doit être compréhensible.
* Le repo doit montrer une progression logique du projet.
* Les limites du projet peuvent être indiquées clairement.

## Fichiers importants

Fichier principal de documentation :

```text
README.md
```

Fichier pour ignorer ce qui ne doit pas être versionné :

```text
.gitignore
```

Fichier de configuration Python si le projet est packagé :

```text
pyproject.toml
```

Dossier de tests si le projet contient des tests :

```text
tests/
```

Exemple de structure simple :

```text
mon-projet/
├── README.md
├── .gitignore
├── pyproject.toml
├── src/
│   └── mon_projet/
│       ├── __init__.py
│       └── cli.py
└── tests/
    └── test_cli.py
```

## Commandes / exemples

Cloner un repo :

```bash
git clone git@github.com:utilisateur/mon-projet.git
```

Entrer dans le projet :

```bash
cd mon-projet
```

Installer le projet en mode développement :

```bash
pip install -e .
```

Lancer le projet :

```bash
python -m mon_projet.cli
```

Ou si une commande CLI est configurée :

```bash
mon-projet --help
```

Lancer les tests :

```bash
pytest
```

Vérifier les fichiers avant commit :

```bash
git status
```

Vérifier les changements :

```bash
git diff
```

Voir l’historique :

```bash
git log --oneline
```

Pousser le repo sur GitHub :

```bash
git push origin main
```

## Ce que doit contenir un bon README

Un bon `README.md` doit au minimum contenir :

* le nom du projet ;
* une description courte ;
* le problème ou l’objectif ;
* les fonctionnalités principales ;
* les prérequis ;
* les étapes d’installation ;
* les commandes d’utilisation ;
* un exemple de sortie ;
* les commandes de test ;
* les compétences travaillées ;
* les limites connues.

Exemple de structure :

```md
# Nom du projet

Description courte du projet.

## Objectif

Pourquoi ce projet existe.

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

## Ce qu’il ne faut pas publier

Certains fichiers ne doivent pas être publiés dans un repo public :

* `.env` avec des secrets ;
* mots de passe ;
* clés API ;
* tokens ;
* `.venv/` ;
* `__pycache__/` ;
* fichiers de logs ;
* fichiers temporaires ;
* gros fichiers générés inutilement ;
* données personnelles.

Exemple de `.gitignore` simple pour Python :

```gitignore
.venv/
__pycache__/
*.pyc
.env
*.log
.pytest_cache/
output/
```

## Erreurs à éviter

* Publier un repo sans README.
* Avoir un README vague ou inutilisable.
* Ne pas donner de commande pour lancer le projet.
* Ne pas expliquer comment installer les dépendances.
* Commiter `.venv`.
* Commiter un fichier `.env`.
* Publier des logs ou fichiers générés inutiles.
* Avoir des noms de fichiers désordonnés.
* Laisser du code mort ou des fichiers de test inutiles.
* Faire un seul gros commit final.
* Ne pas expliquer les limites du projet.
* Croire qu’un repo propre signifie un projet parfait.

## Utilisé dans

* Projet : tous les projets publics sur GitHub.
* Situation concrète : publier un projet pour portfolio, mentor, recruteur ou auto-évaluation.
* Exemple backend : publier une CLI Python avec README, installation, utilisation, tests, `.gitignore`, historique Git lisible et commandes reproductibles.

Exemple :

```bash
git status
pytest
python -m mon_projet.cli --help
git add README.md .gitignore src/ tests/
git commit -m "prepare public repository"
git push origin main
```

## Questions à savoir répondre

1. À quoi sert un repo public propre ?
2. Pourquoi le README est-il important ?
3. Quelles sections doivent apparaître dans un README utile ?
4. Pourquoi ne faut-il pas publier `.env` ?
5. Quel est le rôle du `.gitignore` ?
6. Quels fichiers Python doivent souvent être ignorés ?
7. Pourquoi faut-il donner des commandes d’installation et d’utilisation ?
8. Pourquoi indiquer les limites du projet est une bonne pratique ?
9. Quelle commande permet de vérifier les fichiers avant commit ?
10. Quelle différence entre un projet publié et un projet réellement exécutable ?

## Résumé personnel

Un repo public propre est un projet que quelqu’un d’autre peut comprendre, installer, lancer et évaluer.
Il doit contenir un README clair, une structure lisible, un `.gitignore` correct, des commandes reproductibles et aucun fichier sensible ou inutile.
