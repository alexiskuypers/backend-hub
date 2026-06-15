# Types

## Rôle du concept

Python manipule des objets. Chaque objet a un type, et chaque type possède ses propres règles, opérations et méthodes.

## Exemples

```python
name = "abc"                                # str
age = 5                                     # int
price = 12.50                               # float
active = True                               # bool
value = None                                # absence de valeur
items = ["a", "b"]                          # list
user = {"name": "Alex"}                     # dict
file_path = Path("data/input.csv")          # chemin de fichier
today = date(2026, 6, 15)                   # date simple
created_at = datetime(2026, 6, 15, 14, 30)  # date + heure
amount = Decimal("1200.50")                 # montant précis
```

## Erreur typique

Appliquer une méthode ou une opération au mauvais type.
Autre erreur fréquente : oublier que les données externes arrivent souvent sous forme de texte.

## Règle à retenir

Le type d’une valeur détermine ce qu’on peut faire avec elle.

Parser une valeur = transformer du texte brut en type exploitable.

```python
raw_date = "2026-06-15"
parsed_date = datetime.strptime(raw_date, "%Y-%m-%d").date()
```

`None` signifie “pas de valeur”.
`False` signifie “valeur booléenne fausse”.
`0` signifie “nombre zéro”.
`""` signifie “texte vide”.

## Utilité en projet

Dans `data-contract-cli`, tous les champs CSV arrivent d’abord comme du texte. Le rôle du programme est de parser, convertir, valider et normaliser ces textes vers les bons types métier : `string`, `integer`, `decimal`, `date`, `email`, `boolean`.

### Falsy en Python

| Valeur      | Sens              |
| ----------- | ----------------- |
| `None`      | absence de valeur |
| `False`     | booléen faux      |
| `0` / `0.0` | nombre zéro       |
| `""`        | chaîne vide       |
| `[]`        | liste vide        |
| `{}`        | dictionnaire vide |
| `set()`     | ensemble vide     |
| `()`        | tuple vide        |

Règle : dans une condition, toutes ces valeurs se comportent comme `False`.
