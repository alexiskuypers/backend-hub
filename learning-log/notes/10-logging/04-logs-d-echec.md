# Logs d’échec

## Rôle du concept

Les logs d’échec indiquent ce qui n’a pas fonctionné et donnent assez de contexte pour savoir quoi corriger ou relancer.

Ils doivent préciser l’opération, la donnée concernée et la cause connue de l’échec.

## Exemples

```python
logger.error(
    "Contract validation failed: file=%s reason=%s",
    contract_path.name,
    error,
)
```

Dans un bloc `except`, lorsqu’une traceback est utile :

```python
try:
    rows = read_csv(input_path)
except OSError:
    logger.exception("CSV reading failed: file=%s", input_path)
    raise
```

## Erreur typique

Écrire un log trop vague :

```python
logger.error("Processing failed")
```

Ce message ne permet pas de savoir :

* quelle étape a échoué ;
* quel fichier est concerné ;
* quelle erreur s’est produite ;
* si le traitement peut être relancé.

Il faut aussi éviter de logger plusieurs fois la même erreur à chaque niveau du programme.

## Règle à retenir

Un bon log d’échec doit préciser :

* ce qui a échoué ;
* où l’échec s’est produit ;
* quelle donnée est concernée ;
* la cause connue ;
* l’action possible si elle est identifiable.

Utiliser `logger.error()` pour une erreur connue et `logger.exception()` dans un bloc `except` lorsqu’une traceback est nécessaire.

## Utilité en projet

Dans `data-contract-cli`, les logs d’échec peuvent indiquer :

* contrat YAML invalide ;
* fichier CSV inaccessible ;
* erreur d’encodage ;
* échec d’écriture d’un rapport ;
* traitement interrompu avant la fin.

Exemple :

```text
Error report writing failed: file=reports/invoices_errors.csv reason=permission denied
```

Ce log permet de savoir que la validation peut être relancée après correction des permissions.
