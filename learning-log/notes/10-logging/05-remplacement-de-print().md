# Remplacement de `print()`

## Rôle du concept

Pour un traitement sérieux, `logging` remplace `print()` afin de garder une trace structurée de l’exécution.

Les logs peuvent être filtrés par niveau, enregistrés dans un fichier et enrichis avec du contexte.

## Exemples

Mauvais usage :

```python
print("Validation started")
print("File not found")
```

Usage adapté :

```python
import logging

logger = logging.getLogger(__name__)

logger.info("Validation started: file=%s", input_path)
logger.error("Input file not found: file=%s", input_path)
```

## Erreur typique

Utiliser `print()` pour suivre l’exécution ou signaler des erreurs.

`print()` :

* ne distingue pas les niveaux de gravité ;
* n’ajoute pas automatiquement la date ou le module ;
* est difficile à filtrer ;
* ne produit pas facilement un historique exploitable.

## Règle à retenir

Utiliser :

* `print()` pour une sortie directement destinée à l’utilisateur ;
* `logging` pour suivre, diagnostiquer et conserver l’exécution du programme.

Il ne faut pas remplacer aveuglément tous les `print()`. Une CLI peut encore afficher son résultat final dans le terminal.

## Utilité en projet

Dans `data-contract-cli` :

* la CLI affiche un résumé court à l’utilisateur ;
* les logs enregistrent le fichier traité, les étapes, les résultats et les échecs ;
* les fonctions métier ne doivent pas contenir de `print()`.

Exemple :

```python
logger.info(
    "Validation completed: total_rows=%d valid_rows=%d invalid_rows=%d",
    total_rows,
    valid_rows,
    invalid_rows,
)
```

Cela rend le traitement observable et facilite le diagnostic.
