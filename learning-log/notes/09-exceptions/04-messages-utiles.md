# Messages utiles

## Rôle du concept

Un message d’erreur utile explique clairement ce qui a échoué, à quel endroit, et avec quelle donnée.

Il doit aider à corriger le problème sans devoir lire toute la traceback.

## Exemples

Message vague :

```text
Invalid value
```

Message utile :

```text
Invalid decimal for column 'amount' at row 12: 'abc'
```

Autre exemple :

```python
raise InvalidDateError(
    f"Invalid date for column '{column_name}' at row {row_number}: {raw_value!r}"
)
```

## Erreur typique

Écrire des messages trop génériques.

Exemples :

* `"error"` ;
* `"invalid"` ;
* `"failed"` ;
* `"bad value"` ;
* `"something went wrong"`.

Ces messages ne disent pas quoi corriger.

## Règle à retenir

Un bon message d’erreur doit contenir :

* ce qui a échoué ;
* où ça a échoué ;
* quelle donnée a posé problème ;
* idéalement, ce qui était attendu.

Exemple :

```text
Invalid date for column 'invoice_date' at row 4: 'wrong-date'. Expected format: YYYY-MM-DD
```

## Utilité en projet

Dans `data-contract-cli`, les messages utiles sont essentiels pour le rapport d’erreurs, les logs et la CLI.

Exemples :

```text
Missing required column: 'customer_email'
```

```text
Unknown type in contract for column 'amount': 'moneyy'
```

```text
Invalid email at row 3, column 'customer_email': 'bad-email'
```

Cela permet à l’utilisateur de corriger directement le CSV ou le contrat YAML.
