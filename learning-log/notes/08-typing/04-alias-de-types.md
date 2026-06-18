# Alias de types

## Rôle du concept

Un alias de type permet de donner un nom clair à une structure de type complexe.

Il rend les signatures plus lisibles et plus proches du métier.

## Exemples

Sans alias :

```python
def validate_rows(rows: list[dict[str, str]]) -> list[dict[str, str]]:
    ...
```

Avec alias :

```python
CsvRow = dict[str, str]
CsvRows = list[CsvRow]

def validate_rows(rows: CsvRows) -> CsvRows:
    ...
```

Autre exemple :

```python
ColumnName = str
RawValue = str
```

## Erreur typique

Créer trop d’alias inutiles pour des types simples.

```python
Name = str
Age = int
```

Ce n’est utile que si ça clarifie vraiment le métier.

## Règle à retenir

Un alias de type doit améliorer la lecture.

Il est utile quand une structure revient souvent ou quand le nom métier aide à comprendre le code.

## Utilité en projet

Dans `data-contract-cli`, les alias peuvent clarifier les structures centrales.

Exemples :

```python
CsvRow = dict[str, str]
CsvRows = list[CsvRow]
ColumnName = str
RawValue = str
```

Cela rend le code plus lisible quand le moteur de validation grandit.
