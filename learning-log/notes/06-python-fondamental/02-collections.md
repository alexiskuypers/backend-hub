# Collections

## Rôle du concept

Les collections sont des structures de données qui permettent de regrouper, organiser et manipuler plusieurs valeurs.

Chaque collection a un rôle différent : ordre, association clé/valeur, immutabilité ou unicité.

## Exemples

```python
names = ["Alice", "Bob"]                 # list : suite ordonnée de valeurs
user = {"name": "Alice", "age": 30}       # dict : associe une clé à une valeur
point = (10, 20)                          # tuple : groupe fixe et immuable
unique_ids = {"INV-001", "INV-002"}       # set : valeurs uniques
```

## Erreur typique

Choisir la mauvaise collection.

Exemples :

* utiliser une `list` pour vérifier des valeurs uniques ;
* utiliser un `dict` alors qu’il faut seulement une suite ordonnée ;
* modifier un `tuple` alors qu’il est immuable ;
* oublier qu’un `set` ne garde pas l’ordre comme une liste.

## Règle à retenir

Choisis la collection selon le besoin :

* ordre → `list`
* clé → valeur → `dict`
* groupe fixe → `tuple`
* unicité / déduplication → `set`

## Utilité en projet

Dans `data-contract-cli` :

* une ligne CSV peut être représentée par un `dict` ;
* plusieurs lignes CSV peuvent être stockées dans une `list` ;
* les valeurs déjà vues pour une colonne `unique` peuvent être stockées dans un `set` ;
* une erreur peut être représentée par un groupe fixe de données : ligne, colonne, code, message.
