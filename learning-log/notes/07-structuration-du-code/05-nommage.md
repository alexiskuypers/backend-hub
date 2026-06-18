# Nommage

## Rôle du concept

Le nommage consiste à choisir des noms de variables, fonctions, modules et fichiers qui décrivent clairement leur rôle métier.

Un bon nom permet de comprendre le code sans devoir lire toute l’implémentation.

## Exemples

```python
def normalize_email(raw_email: str) -> str:
    return raw_email.strip().lower()
```

Le nom indique clairement que la fonction normalise un email.

```python
valid_rows = []
invalid_rows = []
contract_rules = {}
```

Ces noms expliquent directement ce que les données représentent.

Mauvais exemple :

```python
def process(x):
    return x.strip().lower()
```

`process` et `x` sont trop vagues.

## Erreur typique

Utiliser des noms trop génériques.

Exemples :

* `data`;
* `result`;
* `process`;
* `check`;
* `value`;
* `tmp`;
* `thing`.

Ces noms peuvent être acceptables localement, mais ils deviennent dangereux quand le projet grandit.

## Règle à retenir

Un nom doit dire ce que représente la donnée ou ce que fait la fonction.

Pour une fonction, utilise souvent un verbe :

* `validate_row`;
* `normalize_email`;
* `parse_date`;
* `load_contract`;
* `write_error_report`.

Pour une donnée, utilise un nom métier :

* `raw_value`;
* `parsed_date`;
* `contract_column`;
* `validation_error`;
* `invalid_rows`.

## Utilité en projet

Dans `data-contract-cli`, le nommage est essentiel pour rendre le moteur compréhensible.

Exemples utiles :

* `load_contract` → charge le contrat YAML ;
* `validate_contract` → vérifie que le contrat est valide ;
* `validate_row` → valide une ligne CSV ;
* `apply_transforms` → applique les transformations ;
* `write_clean_csv` → écrit le CSV propre ;
* `write_error_report` → écrit le rapport d’erreurs.

Un bon nommage rend le projet plus lisible, plus testable et plus facile à défendre à l’oral.
