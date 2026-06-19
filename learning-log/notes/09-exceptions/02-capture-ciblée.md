# Capture ciblée

## Rôle du concept

La capture ciblée consiste à capturer uniquement les erreurs que le programme sait gérer.

Elle permet de traiter les erreurs attendues sans masquer les vrais bugs.

Une erreur attendue est une erreur que le projet peut transformer en message clair, en log utile ou en exit code propre.

## Exemples

```python
try:
    contract = load_contract(path)
except FileNotFoundError:
    raise ContractFileError(f"Contract file not found: {path}")
except PermissionError:
    raise ContractFileError(f"Permission denied while reading contract: {path}")
```

Ici, le code capture seulement les erreurs connues liées au fichier.

Mauvais exemple :

```python
try:
    contract = load_contract(path)
except Exception:
    pass
```

Ce code masque tout : fichier absent, bug dans le code, erreur de parsing, variable mal nommée, etc.

## Erreur typique

Capturer `Exception` trop tôt ou trop largement.

Exemples :

* utiliser `except Exception: pass` ;
* capturer toutes les erreurs dans une fonction métier ;
* cacher une erreur au lieu de la remonter ;
* afficher seulement `"error"` sans contexte ;
* transformer un bug de programmation en simple warning.

Le risque est grave : le programme peut continuer avec des données incorrectes.

## Règle à retenir

Il faut capturer une erreur seulement si on sait quoi faire avec.

Sinon, il vaut mieux la laisser remonter.

Bonne logique :

erreur attendue → capture ciblée → message clair / log / exit code
erreur inattendue → propagation → correction du bug

La capture doit être placée au bon niveau.

Une fonction métier ne doit pas toujours gérer l’erreur elle-même.
Souvent, elle doit lever une exception claire, et la CLI décide comment l’afficher.

## Points stratégiques à couvrir

Les endroits stratégiques à couvrir
* Les frontières avec le monde extérieur

C’est là que les erreurs sont normales.

- lecture fichier
- écriture fichier
- appel API
- connexion DB
- input utilisateur
- arguments CLI
- variables d’environnement
- JSON / CSV / YAML


* Les conversions de données brutes

Très important.


* Les validations métier bloquantes

Exemple :

def calculate_price(quantity: int, unit_price: float) -> float:
    if quantity < 0:
        raise ValueError(f"invalid quantity: {quantity}")

    return quantity * unit_price

Ici, pas besoin de try. Tu testes explicitement la règle.


* Le niveau orchestration / entrée du programme

Dans une CLI :

def main() -> int:
    try:
        run()
    except AppError as error:
        print(f"Error: {error}")
        return 1

    return 0

Ce niveau transforme les erreurs prévues en :

message utilisateur
exit code
log


* Les boucles de traitement batch

Si tu traites 1000 lignes, tu peux attraper l’erreur par ligne :

valid_rows = []
error_rows = []

for row in rows:
    try:
        valid_row = validate_row(row)
    except InvalidRowError as error:
        error_rows.append(str(error))
    else:
        valid_rows.append(valid_row)

Ici, attraper l’erreur est stratégique : une ligne mauvaise ne doit pas forcément arrêter tout le fichier.

## Utilité en projet

Dans `data-contract-cli`, la capture ciblée est essentielle.

Exemples :

* fichier CSV absent ;
* contrat YAML absent ;
* contrat YAML invalide ;
* encodage incorrect ;
* permission refusée ;
* type inconnu dans le contrat ;
* erreur de parsing de date ;
* erreur de parsing decimal.

Ces erreurs ne doivent pas produire une traceback brute.

Elles doivent être transformées en message clair.

Exemple :

```text
Invalid contract: column 'amount' uses unknown type 'moneyy'
```

Ou :

```text
Input file error: unable to read 'data/invoices.csv'
```

La CLI peut ensuite retourner le bon exit code :

* `2` pour contrat invalide ;
* `3` pour erreur de fichier ;
* `4` pour erreur inattendue.

Cette approche rend l’outil plus robuste, plus professionnel et plus facile à diagnostiquer.
