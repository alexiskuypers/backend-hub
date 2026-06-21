# Contexte utile

## Rôle du concept

Le contexte d’un log permet de savoir précisément où et pendant quelle opération un événement s’est produit.

Un message doit contenir les informations nécessaires pour retrouver le problème : fichier, étape, ligne, colonne ou identifiant de job.

## Exemples

```python
logger.info(
    "Validation started: file=%s job_id=%s",
    input_path,
    job_id,
)
```

```python
logger.warning(
    "Invalid value: file=%s row=%d column=%s value=%r",
    input_path.name,
    row_number,
    column_name,
    raw_value,
)
```

## Erreur typique

Écrire un message sans contexte :

```python
logger.error("Validation failed")
```

On ne sait pas quel fichier, quelle ligne ou quelle étape a échoué.

## Règle à retenir

Un log utile doit permettre de répondre rapidement à ces questions :

* quel traitement ?
* quel fichier ou job ?
* quelle étape ?
* quelle ligne ou donnée ?

Ne pas logger de mots de passe, tokens ou autres données sensibles.

## Utilité en projet

Dans `data-contract-cli`, les logs peuvent inclure :

* le nom du CSV et du contrat ;
* l’identifiant du traitement ;
* l’étape en cours ;
* le numéro de ligne et la colonne concernée ;
* le nombre de lignes valides et invalides.

Exemple :

```text
Invalid decimal: file=invoices.csv row=12 column=amount value='abc'
```

Ce contexte permet de diagnostiquer le problème sans devoir relancer le programme au hasard.
