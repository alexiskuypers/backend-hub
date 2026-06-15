# Modules

## Rôle du concept

Un module est un fichier Python qui regroupe du code cohérent autour d’une responsabilité.

Il permet d’éviter le gros script unique et d’organiser le projet en parties compréhensibles.

## Exemples

```text
data_contract/
  cli.py
  contract_loader.py
  contract_validator.py
  csv_reader.py
  validators.py
  transforms.py
  reports.py
```

Exemple mental :

```text
cli.py                → reçoit la commande utilisateur
contract_loader.py    → lit le YAML
contract_validator.py → valide le contrat
validators.py         → valide les valeurs
reports.py            → écrit les sorties
```

## Erreurs typiques

Mettre toute la logique dans `main.py`.

Autre erreur : créer trop de fichiers trop tôt, sans vraie responsabilité claire.

Un module doit représenter une responsabilité, pas juste contenir du code au hasard.

## Règles à retenir

Un module = une zone de responsabilité.

Si deux fonctions changent pour la même raison, elles peuvent probablement vivre dans le même module.

Si un fichier devient trop long ou mélange plusieurs sujets, il faut le découper.

## Utilité en projet

Dans `data-contract-cli`, les modules permettent de séparer :

* CLI ;
* lecture des fichiers ;
* validation du contrat ;
* validation des lignes CSV ;
* transformations ;
* génération des rapports ;
* gestion des erreurs.

C’est ce qui rendra le projet lisible, testable et défendable à l’oral.
