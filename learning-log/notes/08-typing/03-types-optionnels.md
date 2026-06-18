# Types optionnels

## Rôle du concept

Les types optionnels servent à représenter une valeur qui peut être présente ou absente.

En Python, l’absence de valeur est représentée par `None`.

## Exemples

```python
def parse_date(raw_date: str) -> date | None:
    if raw_date == "":
        return None

    return datetime.strptime(raw_date, "%Y-%m-%d").date()
```

Autre exemple :

```python
def find_column(columns: list[str], name: str) -> str | None:
    if name in columns:
        return name

    return None
```

## Erreur typique

Oublier qu’une fonction peut retourner `None`.

```python
parsed_date = parse_date("")
print(parsed_date.year)  # erreur si parsed_date vaut None
```

## Règle à retenir

Si une valeur peut être absente, le type doit le montrer.

```python
date | None
str | None
int | None
```

Et le code qui utilise cette valeur doit traiter le cas `None`.

## Utilité en projet

Dans `data-contract-cli`, les types optionnels sont utiles pour gérer les valeurs absentes du CSV.

Exemples :

* cellule vide ;
* valeur `"NULL"`;
* valeur `"N/A"`;
* colonne optionnelle absente ;
* date non renseignée si `nullable: true`.
