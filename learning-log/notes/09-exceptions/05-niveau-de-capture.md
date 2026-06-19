# Niveau de capture

## Rôle du concept

Le niveau de capture consiste à gérer une erreur à l’endroit le plus adapté.

Toutes les fonctions ne doivent pas capturer les erreurs.

Une fonction bas niveau peut lever une erreur.
Une fonction métier peut ajouter du contexte.
La CLI ou l’orchestration peut transformer l’erreur en message utilisateur, log et exit code.

## Exemples

```python
def parse_decimal(raw_value: str) -> Decimal:
    return Decimal(raw_value)
```

Cette fonction ne capture pas forcément l’erreur.
Elle laisse remonter si la valeur est invalide.

```python
def main() -> int:
    try:
        run_validation()
    except AppError as error:
        print(f"Error: {error}")
        return 1

    return 0
```

Ici, la CLI capture l’erreur au bon niveau pour produire une sortie propre.

## Erreur typique

Capturer l’erreur trop bas dans le code.

```python
def parse_decimal(raw_value: str) -> Decimal | None:
    try:
        return Decimal(raw_value)
    except Exception:
        return None
```

Ce code cache le problème et oblige les autres fonctions à deviner pourquoi la valeur est absente.

## Règle à retenir

Une erreur doit être capturée là où le programme sait quoi en faire.

Règle simple :

```text
bas niveau → détecte ou lève l’erreur
logique métier → ajoute du contexte
boucle batch → isole l’élément invalide
CLI / orchestration → affiche, log, exit code
```

Ne capture pas une erreur seulement pour empêcher le programme de s’arrêter.

## Utilité en projet

Dans `data-contract-cli`, le bon niveau de capture permet de garder le traitement propre.

Exemples :

* parsing invalide → erreur levée ;
* ligne CSV invalide → erreur collectée dans le rapport ;
* contrat YAML invalide → message clair et exit code `2` ;
* fichier introuvable → message clair et exit code `3` ;
* bug inattendu → log d’erreur et exit code `4`.

Cela évite de masquer les bugs tout en donnant une sortie exploitable à l’utilisateur.
