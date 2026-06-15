# Boucles et conditions

## Rôle du concept

Les conditions permettent de choisir quoi faire selon une situation.

Les boucles permettent de répéter une action sur plusieurs éléments.

Ensemble, elles servent à parcourir des données et appliquer une règle seulement quand c’est nécessaire.

## Exemples

```python
orders = [
    {"id": "ORD-001", "status": "paid"},
    {"id": "ORD-002", "status": "pending"},
    {"id": "ORD-003", "status": ""},
]

for order in orders:
    if order["status"] == "":
        print("missing status")
    elif order["status"] == "paid":
        print("order paid")
    else:
        print("other status")
```

## Erreurs typiques

Utiliser une condition trop vague.

```python
if order["status"]:
    continue
```

Cette condition veut seulement dire : “si le status est truthy”.
Elle ne dit pas si le status est valide, invalide, manquant ou interdit.

Autre erreur : accéder directement à une clé qui peut manquer.

```python
order["status"]  # KeyError si la clé n’existe pas
```

## Règles à retenir

Une condition doit tester une intention claire.

Mauvais :

```python
if value:
```

Mieux :

```python
if value is None:
if value == "":
if status not in allowed_statuses:
```

Dans une boucle, pense toujours :

1. quel élément je parcours ;
2. quelle règle je teste ;
3. qu’est-ce que je fais si c’est valide ;
4. qu’est-ce que je fais si c’est invalide.

## Utilité en projet

Dans `data-contract-cli`, les boucles et conditions servent à traiter le CSV ligne par ligne.

Pour chaque ligne :

* vérifier les colonnes obligatoires ;
* tester les valeurs vides ;
* valider les types ;
* appliquer les règles du contrat ;
* isoler les lignes invalides ;
* conserver les lignes valides.

C’est le cœur du moteur de validation.
