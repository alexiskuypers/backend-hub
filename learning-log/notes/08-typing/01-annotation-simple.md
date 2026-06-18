# Annotations simples

## Rôle du concept

Les annotations simples permettent d’indiquer le type attendu pour les paramètres d’une fonction et le type retourné.

Elles ne forcent pas Python à respecter le type, mais elles rendent le code plus lisible et plus facile à vérifier.

## Exemples

```python
def normalize_email(raw_email: str) -> str:
    return raw_email.strip().lower()
```

```python
def is_valid_amount(amount: float) -> bool:
    return amount >= 0
```

## Erreur typique

Croire que les annotations bloquent automatiquement les mauvais types.

```python
def double(value: int) -> int:
    return value * 2

double("a")  # Python l’accepte, résultat : "aa"
```

## Règle à retenir

Le typing décrit le contrat attendu, mais ne remplace pas la validation.

Une annotation aide le développeur, l’IDE, les tests et les outils d’analyse.

## Utilité en projet

Dans `data-contract-cli`, les annotations simples permettent de comprendre rapidement ce qu’une fonction attend et retourne.

Exemples :

* `parse_decimal(raw_value: str) -> Decimal`
* `normalize_email(raw_email: str) -> str`
* `validate_required(value: str) -> bool`

---

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

---

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

---

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

---

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
