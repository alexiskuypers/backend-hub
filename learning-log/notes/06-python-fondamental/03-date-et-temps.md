# Dates et temps

## Rôle du concept

Les dates permettent de transformer une valeur texte en objet Python manipulable : comparer, trier, formater ou valider une date.

Parser une date = convertir une chaîne de caractères en `date` ou `datetime`.

## Exemples

```python
from datetime import datetime

raw_date = "07-06-2026"

parsed_date = datetime.strptime(raw_date, "%d-%m-%Y").date()

print(parsed_date)  # 2026-06-07
```

Autre format :

```python
raw_date = "2026-06-07"

parsed_date = datetime.strptime(raw_date, "%Y-%m-%d").date()
```

## Erreur typique

Garder une date sous forme de `str` et croire qu’elle se comporte comme une vraie date.

Autre erreur fréquente : utiliser le mauvais format de parsing.

```python
"07-06-2026"  # format : "%d-%m-%Y"
"2026-06-07"  # format : "%Y-%m-%d"
```

## Règle à retenir

Une date venant d’un fichier CSV arrive comme du texte.

Il faut d’abord la parser, puis seulement la comparer, la normaliser ou l’exporter.

`date` = jour précis.
`datetime` = jour + heure.

## Utilité en projet

Dans `data-contract-cli`, les dates CSV doivent être validées selon les formats acceptés dans le contrat YAML.

Exemple :

```yaml
input_formats:
  - "%d/%m/%Y"
  - "%Y-%m-%d"

output_format: "%Y-%m-%d"
```

L’objectif : transformer `"07/06/2026"` ou `"2026-06-07"` en sortie normalisée `"2026-06-07"`.
