# Propagation

## Rôle du concept

La propagation consiste à laisser remonter une erreur quand la fonction actuelle ne sait pas la gérer correctement.

Une fonction ne doit pas capturer une erreur juste pour “éviter le crash”.

Si elle ne peut pas corriger, transformer ou enrichir l’erreur, elle doit la laisser remonter à un niveau plus adapté.

## Exemples

```python
def parse_decimal(raw_value: str) -> Decimal:
    return Decimal(raw_value)
```

Ici, la fonction ne capture pas forcément l’erreur.
Si la valeur est invalide, l’erreur peut remonter vers une couche qui saura créer un message utilisateur ou une erreur de validation.

Autre exemple :

```python
def validate_row(row: CsvRow, contract: DataContract) -> ValidatedRow:
    return apply_contract_rules(row, contract)
```

Si une règle échoue, l’erreur peut remonter vers la boucle de traitement qui décidera si la ligne doit être rejetée.

## Erreur typique

Capturer une erreur trop tôt et la masquer.

```python
try:
    value = Decimal(raw_value)
except Exception:
    return None
```

Ce code cache le vrai problème.
On ne sait plus si la valeur était vide, invalide, mal formatée ou si un bug est arrivé.

## Règle à retenir

On capture une erreur seulement si on sait quoi en faire.

Sinon, on la laisse remonter.

```text
fonction bas niveau → lève une erreur claire
fonction métier → ajoute du contexte si nécessaire
orchestration / CLI → transforme en message, log ou exit code
```

Une erreur non gérée vaut mieux qu’une erreur avalée silencieusement.

## Utilité en projet

Dans `data-contract-cli`, la propagation permet de garder les responsabilités propres.

Exemples :

* une fonction de parsing peut lever une erreur ;
* une fonction de validation peut transformer cette erreur en erreur applicative ;
* la boucle CSV peut décider de rejeter seulement la ligne concernée ;
* la CLI peut afficher un message clair et retourner le bon exit code.

Cela évite de cacher les bugs et permet de diagnostiquer précisément ce qui a échoué.
