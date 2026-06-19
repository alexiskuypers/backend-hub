# Erreurs applicatives

## Rôle du concept

Une erreur applicative est une exception créée pour représenter un problème propre au projet.

Elle permet de distinguer une erreur métier attendue d’un bug technique imprévu.
Une erreur attendue vient souvent de l’extérieur, Un bug vient d’une contradiction dans ton propre code.

Exemples de problèmes applicatifs :

* contrat YAML invalide ;
* colonne obligatoire absente ;
* type inconnu dans le contrat ;
* fichier CSV impossible à lire ;
* règle de validation inconnue.

## Exemples

```python
class DataContractError(Exception):
    pass


class InvalidContractError(DataContractError):
    pass


class CsvValidationError(DataContractError):
    pass
```

Utilisation :

```python
def validate_column_type(column_name: str, column_type: str) -> None:
    allowed_types = {"string", "integer", "decimal", "date", "email", "boolean"}

    if column_type not in allowed_types:
        raise InvalidContractError(
            f"Column '{column_name}' uses unknown type '{column_type}'"
        )
```

## Erreur typique

Utiliser uniquement des exceptions générales partout.

```python
raise Exception("Invalid contract")
```

Ou pire :

```python
try:
    ...
except Exception:
    pass
```

Ces erreurs sont trop vagues. Elles rendent le programme difficile à comprendre, tester et diagnostiquer.

## Règle à retenir

Une erreur applicative doit représenter un problème clair du domaine du projet.

Elle doit avoir :

* un nom précis ;
* un message utile ;
* une cause compréhensible ;
* un niveau de capture adapté.

Ne crée pas une exception pour chaque petit détail, mais crée des exceptions pour les grandes familles d’erreurs du projet.

## Utilité en projet

Dans `data-contract-cli`, les erreurs applicatives peuvent représenter :

* `InvalidContractError` → contrat YAML invalide ;
* `UnknownColumnTypeError` → type inconnu dans le contrat ;
* `MissingRequiredColumnError` → colonne obligatoire absente ;
* `CsvFileError` → problème de lecture du CSV ;
* `ValidationRuleError` → règle de validation invalide.

Cela permet à la CLI de réagir proprement :

* afficher un message clair ;
* écrire un log utile ;
* éviter une traceback brute ;
* retourner le bon exit code.

Exemple :

```text
Invalid contract: column 'amount' uses unknown type 'moneyy'
```

Au lieu de laisser Python afficher une erreur technique confuse.
