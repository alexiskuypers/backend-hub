# Validation ligne par ligne

## Rôle du concept

La validation ligne par ligne consiste à contrôler chaque ligne indépendamment.

Une ligne invalide est isolée dans le rapport d’erreurs, tandis que les autres lignes continuent d’être traitées.

## Exemples

```python
valid_rows = []
validation_errors = []

for row_number, row in enumerate(reader, start=2):
    try:
        valid_row = validate_row(row, contract)
    except InvalidRowError as error:
        validation_errors.append(
            {
                "row_number": row_number,
                "column": error.column,
                "error_code": error.code,
                "message": str(error),
            }
        )
    else:
        valid_rows.append(valid_row)
```

La ligne invalide est rejetée, mais elle n’arrête pas tout l’import.

## Erreur typique

Arrêter le traitement dès la première ligne incorrecte.

```python
for row in rows:
    validate_row(row, contract)
```

Si `validate_row()` lève une exception, toutes les lignes suivantes sont ignorées.

Autres erreurs fréquentes :

* perdre le numéro de ligne d’origine ;
* mélanger lignes valides et invalides ;
* ignorer silencieusement les erreurs ;
* écrire une ligne partiellement transformée dans le CSV propre.

## Règle à retenir

Chaque ligne doit produire l’un de ces deux résultats :

```text
ligne valide → normalisée et conservée
ligne invalide → rejetée et documentée
```

Une erreur globale de structure, comme une colonne obligatoire absente, peut arrêter le traitement.

Une erreur locale de valeur ne doit normalement bloquer que la ligne concernée.

## Utilité en projet

Dans `data-contract-cli`, la validation ligne par ligne permet de :

* conserver les lignes valides ;
* isoler les lignes invalides ;
* collecter plusieurs erreurs dans un même traitement ;
* produire un CSV propre ;
* produire un rapport d’erreurs exploitable ;
* éviter qu’une seule mauvaise ligne bloque tout le fichier.

C’est une règle centrale : les erreurs globales arrêtent le traitement, les erreurs locales sont collectées ligne par ligne.
