# Lisibilité des contrats

## Rôle du concept

La lisibilité des contrats consiste à rendre les signatures de fonctions suffisamment claires pour comprendre ce qu’elles attendent et ce qu’elles retournent.

Une bonne signature évite de devoir lire tout le corps de la fonction pour comprendre son rôle.

## Exemples

Signature claire :

```python
def validate_email(raw_email: str) -> bool:
    ...
```

Signature encore plus claire :

```python
def normalize_email(raw_email: str) -> str:
    ...
```

Avec types composites :

```python
def validate_row(row: dict[str, str], contract: dict) -> list[str]:
    ...
```

## Erreur typique

Écrire des fonctions avec des noms vagues et sans types.

```python
def process(data):
    ...
```

On ne sait pas ce que `data` représente, ni ce que la fonction retourne.

## Règle à retenir

Une fonction doit être compréhensible par sa signature.

Un bon contrat de fonction indique :

* ce qu’elle reçoit ;
* ce qu’elle retourne ;
* son intention métier.

## Utilité en projet

Dans `data-contract-cli`, les signatures doivent rendre le moteur lisible.

Exemples :

```python
def load_contract(path: Path) -> DataContract:
    ...

def validate_row(row: CsvRow, contract: DataContract) -> list[ValidationError]:
    ...

def write_error_report(errors: list[ValidationError], output_path: Path) -> None:
    ...
```

Cela aide à séparer clairement lecture, validation, transformation et écriture.
