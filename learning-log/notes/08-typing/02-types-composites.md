# Types composites

## Rôle du concept

Les types composites permettent de typer des collections comme les listes, dictionnaires ou tuples.

Ils rendent plus clair le contenu attendu dans une structure de données.

## Exemples

```python
names: list[str] = ["Alice", "Bob"]

scores: dict[str, int] = {
    "Alice": 10,
    "Bob": 8,
}

error: tuple[int, str, str] = (3, "email", "INVALID_EMAIL")
```

## Erreur typique

Typer seulement la collection sans préciser ce qu’elle contient.

```python
rows: list = []
```

C’est moins clair que :

```python
rows: list[dict[str, str]] = []
```

## Règle à retenir

Quand tu types une collection, indique aussi le type de ce qu’elle contient.

Mauvais :

```python
data: dict
```

Mieux :

```python
data: dict[str, str]
```

## Utilité en projet

Dans `data-contract-cli`, les types composites sont utiles pour représenter :

* plusieurs lignes CSV : `list[dict[str, str]]`;
* une ligne CSV : `dict[str, str]`;
* les erreurs de validation : `list[ValidationError]`;
* les valeurs déjà vues : `set[str]`.
