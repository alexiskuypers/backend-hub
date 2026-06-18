# Séparation logique / I/O

## Rôle du concept

La séparation logique / I/O consiste à isoler la logique métier de tout ce qui communique avec l’extérieur du programme.

La logique métier valide, transforme, calcule ou décide.

L’I/O lit ou écrit des fichiers, affiche dans le terminal, appelle une API ou interagit avec une base de données.

## Exemples

```python
def normalize_email(raw_email: str) -> str:
    return raw_email.strip().lower()
```

Cette fonction est de la logique métier : elle reçoit une valeur, la transforme, puis retourne un résultat.

```python
from pathlib import Path

def read_csv(path: Path) -> list[dict[str, str]]:
    ...
```

Cette fonction est de l’I/O : elle lit un fichier depuis le disque.

## Erreur typique

Mélanger lecture de fichier, validation, transformation et écriture de rapport dans une seule fonction.

Exemples :

* lire un CSV dans une fonction censée seulement valider une ligne ;
* mettre un `print()` dans une fonction de validation ;
* écrire un fichier directement depuis une fonction métier ;
* rendre une fonction impossible à tester sans vrai fichier.

## Règle à retenir

La logique métier doit pouvoir être testée sans fichier, sans terminal, sans réseau et sans base de données.

Une fonction logique reçoit des données déjà chargées et retourne un résultat.

## Utilité en projet

Dans `data-contract-cli` :

* la lecture du CSV appartient à l’I/O ;
* la lecture du contrat YAML appartient à l’I/O ;
* la validation des colonnes appartient à la logique métier ;
* la validation des valeurs appartient à la logique métier ;
* la normalisation appartient à la logique métier ;
* l’écriture du CSV propre, du rapport d’erreurs et du résumé JSON appartient à l’I/O.

Cette séparation rend le moteur de validation testable, lisible et plus facile à faire évoluer.
